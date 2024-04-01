# Header中携带签名<a name="obs_04_0010"></a>

OBS的所有API接口都可以通过在header中携带签名方式来进行身份认证，也是最常用的身份认证方式。

在Header中携带签名是指将通过HTTP消息中Authorization header头域携带签名信息，消息头域的格式为：

```
Authorization: OBS AccessKeyID:signature
```

其中Authorization是标识符，可以理解为key，标识符值，即value值，由服务简称、AK值和signature组成，服务简称与AK值用空格分隔，AK值与signature用英文冒号分隔。

签名的计算过程如下：

1.  构造请求字符串\(StringToSign\)。
2.  对第一步的结果进行UTF-8编码。
3.  使用SK对第二步的结果进行HMAC-SHA1签名计算。
4.  对第三步的结果进行Base64编码，得到签名。

请求字符串\(StringToSign\)按照如下规则进行构造，各个参数的含义如[表1](#table34479832212511)所示。

```
StringToSign = 
    HTTP-Verb + "\n" + 
    Content-MD5 + "\n" + 
    Content-Type + "\n" + 
    Date + "\n" + 
    CanonicalizedHeaders + CanonicalizedResource
```

**表 1**  构造StringToSign所需参数说明

|参数|描述|
|--|--|
|HTTP-Verb|指接口操作的方法，对REST接口而言，即为http请求操作的VERB，如："PUT"，"GET"，"DELETE"等字符串。|
|Content-MD5|按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串，可以为空。具体请参见表6以及表下方的计算方法示例。|
|Content-Type|内容类型，用于指定消息类型，例如： text/plain。当请求中不带该头域时，该参数按照空字符串处理，见表2。|
|Date|生成请求的时间，该时间格式遵循RFC 1123；该时间与当前服务器的时间超过15分钟时服务端返回403。当有自定义字段x-obs-date时，该参数按照空字符串处理；见表6。如果进行临时授权方式操作（如临时授权方式获取对象内容等操作）时，该参数不需要。|
|CanonicalizedHeaders|HTTP请求头域中的OBS请求头字段，即以“x-obs-”作为前辍的头域，如“x-obs-date，x-obs-acl，x-obs-meta-*”。用户在调用API时，请根据自身需求，从调用的API支持的头域中选取。请求头字段中关键字的所有字符要转为小写（但内容值需要区分大小写，如“x-obs-storage-class:STANDARD”），需要添加多个字段时，要将所有字段按照关键字的字典序从小到大进行排序。在添加请求头字段时，如果有重名的字段，则需要进行合并。如：x-obs-meta-name:name1和x-obs-meta-name:name2，则需要先将重名字段的值（这里是name1和name2）以逗号分隔，合并成x-obs-meta-name:name1,name2。头域中的请求头字段中的关键字不允许含有非ASCII码或不可识别字符；请求头字段中的值也不建议使用非ASCII码或不可识别字符，如果一定要使用非ASCII码或不可识别字符，需要客户端自行做编解码处理，可以采用URL编码或者Base64编码，服务端不会做解码处理。当请求头字段中含有无意义空格或Tab键时，需要摒弃。例如：x-obs-meta-name: name（name前带有一个无意义空格），需要转换为：x-obs-meta-name:name上传对象和上传段支持携带x-obs-content-sha256头域，该头域值为请求消息体256-bit SHA256值转十六进制值，计算方式为Hex(SHA256Hash(<payload>)，服务端会对携带此头域的请求计算其消息体的sha256值做校验（性能会有部分下降，在安全上推荐该算法）。每一个请求头字段最后都需要另起新行，见表4|
|CanonicalizedResource|表示HTTP请求所指定的OBS资源，构造方式如下：<桶名+对象名>+[子资源1] + [子资源2] + ...桶名和对象名。通过桶绑定的自定义域名访问OBS，桶名由自定义域名表示，则为"/obs.ccc.com/object"，其中“obs.ccc.com”为桶绑定的自定义域名。如果没有对象名，如列举桶，则为"/obs.ccc.com/"；不是通过桶绑定的自定义域名访问OBS的场景，则为"/bucket/object"，如果没有对象名，如列举桶，则为"/bucket/"。如果桶名也没有，则为“/”。如果有子资源，则将子资源添加进来，例如?acl，?logging。OBS支持各种子资源，包括：CDNNotifyConfiguration, acl, append, attname, backtosource, cors, customdomain, delete, deletebucket, directcoldaccess, encryption, inventory, length, lifecycle, location, logging, metadata, modify, name, notification, partNumber, policy, position, quota, rename, replication, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, restore, storageClass, storagePolicy, storageinfo, tagging, torrent, truncate, uploadId, uploads, versionId, versioning, versions, website, x-image-process, x-image-save-bucket, x-image-save-object, x-obs-security-token, object-lock, retention。如果有多个子资源，在包含这些子资源时，需要首先将这些子资源按照其关键字的字典序从小到大排列，并使用**“&”**拼接。子资源通常是唯一的，不建议请求的URL包含多个相同关键字的子资源（例如，key=value1&key=value2），如果存在这种情况，OBS服务端签名时只会计算第一个子资源且也只有第一个子资源的值会对实际业务产生作用；以获取对象（GetObject）接口为例，假设桶名为bucket-test，对象名为object-test，对象的版本号为xxx，获取时需要重写Content-Type为text/plain，那么签名计算出的CanonicalizedResource为：/bucket-test/object-test?response-content-type=text/plain&versionId=xxx。|


下面的几张表提供了一些生成StringToSign的例子。

**表 2**  获取对象

|请求消息头|StringToSign|
|--|--|
|GET /object.txt HTTP/1.1Host: bucket.obs.cn-north-4.myhuaweicloud.comDate: Sat, 12 Oct 2015 08:12:38 GMT|GET \n\n\nSat, 12 Oct 2015 08:12:38 GMT\n/bucket/object.txt|


**表 3**  使用临时AK/SK和securitytoken上传对象

|请求消息头|StringToSign|
|--|--|
|PUT /object.txt HTTP/1.1User-Agent: curl/7.15.5Host: bucket.obs.cn-north-4.myhuaweicloud.comx-obs-date:Tue, 15 Oct 2015 07:20:09 GMTx-obs-security-token: YwkaRTbdY8g7q....content-type: text/plainContent-Length: 5913339|PUT\n\ntext/plain\n\nx-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\nx-obs-security-token:YwkaRTbdY8g7q....\n/bucket/object.txt|


**表 4**  带请求头字段上传对象

|请求消息头|StringToSign|
|--|--|
|PUT /object.txt HTTP/1.1User-Agent: curl/7.15.5Host: bucket.obs.cn-north-4.myhuaweicloud.comDate: Mon, 14 Oct 2015 12:08:34 GMTx-obs-acl: public-readcontent-type: text/plainContent-Length: 5913339|PUT\n\ntext/plain\nMon, 14 Oct 2015 12:08:34 GMT\nx-obs-acl:public-read\n/bucket/object.txt|


**表 5**  获取对象ACL

|请求消息头|StringToSign|
|--|--|
|GET /object.txt?acl HTTP/1.1Host: bucket.obs.cn-north-4.myhuaweicloud.comDate: Sat, 12 Oct 2015 08:12:38 GMT|GET \n\n\nSat, 12 Oct 2015 08:12:38 GMT\n/bucket/object.txt?acl|


**表 6**  上传对象且携带Content-MD5头域

|请求消息头|StringToSign|
|--|--|
|PUT /object.txt HTTP/1.1Host: bucket.obs.cn-north-4.myhuaweicloud.comx-obs-date:Tue, 15 Oct 2015 07:20:09 GMTContent-MD5: I5pU0r4+sgO9Emgl1KMQUg==Content-Length: 5913339|PUT\nI5pU0r4+sgO9Emgl1KMQUg==\n\n\nx-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\n/bucket/object.txt|


**表 7**  使用自定义域名方式上传对象

|请求消息头|StringToSign|
|--|--|
|PUT /object.txt HTTP/1.1Host: obs.ccc.comx-obs-date:Tue, 15 Oct 2015 07:20:09 GMTContent-MD5: I5pU0r4+sgO9Emgl1KMQUg==Content-Length: 5913339|PUT\nI5pU0r4+sgO9Emgl1KMQUg==\n\n\nx-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\n/obs.ccc.com/object.txt|


## Java中Content-MD5的计算方法示例<a name="section1255031191518"></a>

```
import java.security.MessageDigest;
import sun.misc.BASE64Encoder;
import java.io.UnsupportedEncodingException;
import java.security.NoSuchAlgorithmException;

public class Md5{
     public static void main(String[] args) {
          try {
                 String exampleString = "blog";
                 MessageDigest messageDigest = MessageDigest.getInstance("MD5"); 
                 BASE64Encoder encoder = new BASE64Encoder(); 
                 String contentMd5 = encoder.encode(messageDigest.digest(exampleString.getBytes("utf-8")));
                 System.out.println("Content-MD5：" + contentMd5);    
          } catch (NoSuchAlgorithmException | UnsupportedEncodingException e) 
          {
                 e.printStackTrace();
          }
     }
}
```

根据请求字符串\(StringToSign\)和用户SK使用如下算法生成Signature，生成过程使用HMAC算法\(hash-based authentication code algorithm\)。

```
Signature = Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) )
```

例如在华北-北京四区域创建桶名为newbucketname2的私有桶，客户端请求格式为：

```
PUT / HTTP/1.1 
Host: newbucketname2.obs.cn-north-4.myhuaweicloud.com
Content-Length: length
Date: Fri, 06 Jul 2018 03:45:51 GMT
x-obs-acl:private
x-obs-storage-class:STANDARD
Authorization: OBS UDSIAMSTUBTEST000254:ydH8ffpcbS6YpeOMcEZfn0wE90c=
<CreateBucketConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/"> 
    <Location>cn-north-4</Location>
</CreateBucketConfiguration>
```

## Java中签名的计算方法<a name="section131611926171613"></a>

```
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Base64;
import java.util.Collections;
import java.util.HashMap;
import java.util.List;
import java.util.Locale;
import java.util.Map;
import java.util.TreeMap;

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

public class SignDemo {
	
    private static final String SIGN_SEP = "\n";
	
    private static final String OBS_PREFIX = "x-obs-";
 
    private static final String DEFAULT_ENCODING = "UTF-8";
 
    private static final List<String> SUB_RESOURCES = Collections.unmodifiableList(Arrays.asList(
        "CDNNotifyConfiguration", "acl", "append", "attname", "backtosource", "cors", "customdomain", "delete",
   	"deletebucket", "directcoldaccess", "encryption", "inventory", "length", "lifecycle", "location", "logging",
   	"metadata", "mirrorBackToSource", "modify", "name", "notification", "obscompresspolicy",  "orchestration", 
   	"partNumber", "policy", "position", "quota","rename", "replication", "response-cache-control", 
   	"response-content-disposition","response-content-encoding", "response-content-language", "response-content-type", 
   	"response-expires","restore", "storageClass", "storagePolicy", "storageinfo", "tagging", "torrent", "truncate",
   	"uploadId", "uploads", "versionId", "versioning", "versions", "website", "x-image-process",
  	 "x-image-save-bucket", "x-image-save-object", "x-obs-security-token", "object-lock", "retention"));
 
    private String ak;
 
    private String sk;
 
     public String urlEncode(String input) throws UnsupportedEncodingException {
        return URLEncoder.encode(input, DEFAULT_ENCODING)
            .replaceAll("%7E", "~") //for browser
            .replaceAll("%2F", "/")
            .replaceAll("%20", "+");
    }
 
    private String join(List<?> items, String delimiter) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < items.size(); i++) {
            String item = items.get(i).toString();
            sb.append(item);
            if (i < items.size() - 1) {
                sb.append(delimiter);
            }
        }
        return sb.toString();
    }
	
    private boolean isValid(String input) {
        return input != null && !input.equals("");
    }
	
    public String hmacSha1(String input) throws NoSuchAlgorithmException, InvalidKeyException, UnsupportedEncodingException {
        SecretKeySpec signingKey = new SecretKeySpec(this.sk.getBytes(DEFAULT_ENCODING), "HmacSHA1");
        Mac mac = Mac.getInstance("HmacSHA1");
        mac.init(signingKey);
        return Base64.getEncoder().encodeToString(mac.doFinal(input.getBytes(DEFAULT_ENCODING)));
    }
	
    private String stringToSign(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
        String bucketName, String objectName) throws Exception{
        String contentMd5 = "";
        String contentType = "";
        String date = "";
		
        TreeMap<String, String> canonicalizedHeaders = new TreeMap<String, String>();
		
        String key;
        List<String> temp = new ArrayList<String>();
        for(Map.Entry<String, String[]> entry : headers.entrySet()) {
            key = entry.getKey();
            if(key == null || entry.getValue() == null || entry.getValue().length == 0) {
                continue;
            }
			
            key = key.trim().toLowerCase(Locale.ENGLISH);
            if(key.equals("content-md5")) {
                contentMd5 = entry.getValue()[0];
                continue;
            }
			
            if(key.equals("content-type")) {
                contentType = entry.getValue()[0];
                continue;
            }
			
            if(key.equals("date")) {
                date = entry.getValue()[0];
                continue;
            }
			
            if(key.startsWith(OBS_PREFIX)) {				
                for(String value : entry.getValue()) {
                    if(value != null) {
                        temp.add(value.trim());
                    }
                }
                canonicalizedHeaders.put(key, this.join(temp, ","));
                temp.clear();
            }
        }
		
        if(canonicalizedHeaders.containsKey("x-obs-date")) {
            date = "";
        }	
		
        // handle method/content-md5/content-type/date
        StringBuilder stringToSign = new StringBuilder();
        stringToSign.append(httpMethod).append(SIGN_SEP)
            .append(contentMd5).append(SIGN_SEP)
            .append(contentType).append(SIGN_SEP)
            .append(date).append(SIGN_SEP);
			
        // handle canonicalizedHeaders
        for(Map.Entry<String, String> entry : canonicalizedHeaders.entrySet()) {
            stringToSign.append(entry.getKey()).append(":").append(entry.getValue()).append(SIGN_SEP);
        }
		
        // handle CanonicalizedResource
        stringToSign.append("/");
        if(this.isValid(bucketName)) {
            stringToSign.append(bucketName).append("/");
            if(this.isValid(objectName)) {
                stringToSign.append(this.urlEncode(objectName));
            }
        }
		
        TreeMap<String, String> canonicalizedResource = new TreeMap<String, String>();
        for(Map.Entry<String, String> entry : queries.entrySet()) {
            key = entry.getKey();
            if(key == null) {
                continue;
            }
			
            if(SUB_RESOURCES.contains(key)) {
                canonicalizedResource.put(key, entry.getValue());
            }
        }
		
        if(canonicalizedResource.size() > 0) {
            stringToSign.append("?");
            for(Map.Entry<String, String> entry : canonicalizedResource.entrySet()) {
                stringToSign.append(entry.getKey());
                if(this.isValid(entry.getValue())) {
                    stringToSign.append("=").append(entry.getValue());
                }
                stringToSign.append("&");
            }
            stringToSign.deleteCharAt(stringToSign.length()-1);
        }
		
        //    System.out.println(String.format("StringToSign:%s%s", SIGN_SEP, stringToSign.toString()));
		
        return stringToSign.toString();
    }
	
    public String headerSignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
        String bucketName, String objectName) throws Exception {

        //1. stringToSign
        String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName);
		
        //2. signature
        return String.format("OBS %s:%s", this.ak, this.hmacSha1(stringToSign));
    }
		
    public String querySignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
        String bucketName, String objectName, long expires) throws Exception {
        if(headers.containsKey("x-obs-date")) {
            headers.put("x-obs-date", new String[] {String.valueOf(expires)});
        } else {
            headers.put("date", new String[] {String.valueOf(expires)});
        }
        //1. stringToSign
        String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName);
		
        //2. signature
        return this.urlEncode(this.hmacSha1(stringToSign));
    }
	
    public static void main(String[] args) throws Exception {
        SignDemo demo = new SignDemo();

        /* 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；
        本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量HUAWEICLOUD_SDK_AK和HUAWEICLOUD_SDK_SK。*/
        demo.ak = System.getenv("HUAWEICLOUD_SDK_AK");
        demo.sk = System.getenv("HUAWEICLOUD_SDK_SK");
		
        String bucketName = "bucket-test";
        String objectName = "hello.jpg";
        Map<String, String[]> headers = new HashMap<String, String[]>();
        headers.put("date", new String[] {"Sat, 12 Oct 2015 08:12:38 GMT"});
        headers.put("x-obs-acl", new String[] {"public-read"});
        headers.put("x-obs-meta-key1", new String[] {"value1"});
        headers.put("x-obs-meta-key2", new String[] {"value2", "value3"});
        Map<String, String> queries = new HashMap<String, String>();
        queries.put("acl", null);
		
        System.out.println(demo.headerSignature("PUT", headers, queries, bucketName, objectName));
    }
	
}
```

签名计算的样例结果为（按照执行时间的不同变化）：ydH8ffpcbS6YpeOMcEZfn0wE90c=

## Python中签名的计算方法<a name="section1875724541612"></a>

```
import os
import sys
import hashlib
import hmac
import binascii
from datetime import datetime
IS_PYTHON2 = sys.version_info.major == 2 or sys.version < '3'

# 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；
# 本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量HUAWEICLOUD_SDK_AK和HUAWEICLOUD_SDK_SK。
yourSecretAccessKeyID = os.getenv('HUAWEICLOUD_SDK_SK')
httpMethod = "PUT"
contentType = "application/xml"
# "date" is the time when the request was actually generated
date = datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
canonicalizedHeaders = "x-obs-acl:private\n"
CanonicalizedResource = "/newbucketname2"
canonical_string = httpMethod + "\n" + "\n" + contentType + "\n" + date + "\n" + canonicalizedHeaders + CanonicalizedResource
if IS_PYTHON2:    
    hashed = hmac.new(yourSecretAccessKeyID, canonical_string, hashlib.sha1)    
    encode_canonical = binascii.b2a_base64(hashed.digest())[:-1]
else:    
    hashed = hmac.new(yourSecretAccessKeyID.encode('UTF-8'), canonical_string.encode('UTF-8'), hashlib.sha1)    
    encode_canonical = binascii.b2a_base64(hashed.digest())[:-1].decode('UTF-8')

print(encode_canonical)
```

签名计算的样例结果为（按照执行时间的不同变化）：ydH8ffpcbS6YpeOMcEZfn0wE90c=

## C语言中签名的计算方法<a name="section657820586554"></a>

请单击[此处](https://obs-community.obs.cn-north-1.myhuaweicloud.com/sign/signature_c.zip)，下载C语言签名计算代码样例，其中：

1.  计算签名的接口包含在sign.h头文件中。
2.  计算签名的示例代码在main.c文件中。

## 签名不匹配报错处理<a name="section1712513019265"></a>

如果调用OBS API报如下错误：

状态码：403 Forbidden

错误码：SignatureDoesNotMatch

错误信息：The request signature we calculated does not match the signature you provided. Check your key and signing method.

请参考以下案例进行排查处理：[签名不匹配（SignatureDoesNotMatch）如何处理](https://support.huaweicloud.com/obs_faq/obs_faq_0173.html)

