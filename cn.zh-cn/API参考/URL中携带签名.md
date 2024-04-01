# URL中携带签名<a name="obs_04_0011"></a>

URL中携带签名：OBS服务支持用户构造一个特定操作的URL，这个URL中会包含用户AK、签名、有效期、资源等信息，任何拿到这个URL的人均可执行这个操作，OBS服务收到这个请求后认为该请求就是签发URL用户自己在执行操作。例如构造一个携带签名信息的下载对象的URL，拿到相应URL的人能下载这个对象，但该URL只在Expires指定的失效时间内有效。URL中携带签名主要用于在不提供给其他人Secret Access Key的情况下，让其他人能用预签发的URL来进行身份认证，并执行预定义的操作。

URL中携带签名请求的消息格式如下：

```
GET /ObjectKey?AccessKeyId=AccessKeyID&Expires=ExpiresValue&Signature=signature HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
```

URL中使用临时AK，SK和securitytoken下载对象消息格式如下：

```
GET /ObjectKey?AccessKeyId=AccessKeyID&Expires=ExpiresValue&Signature=signature&x-obs-security-token=securitytoken HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
```

参数具体意义如[表1](#table5447121714296)所示。

**表 1**  请求消息参数

|**参数名称**|**描述**|**是否必选**|
|--|--|--|
|AccessKeyId|签发者的AK信息。OBS根据AK确定签发者的身份，并认为URL就是签发者在访问。类型：String|是|
|Expires|临时授权失效的时间；UTC时间，1970年1月1日零时之后的指定的Expires时间内有效（以秒为单位）。类型：String|是|
|Signature|根据用户SK、Expires等参数计算出的签名信息。类型：String|是|
|x-obs-security-token|使用临时AK/SK鉴权时，临时AK/SK和securitytoken必须同时使用，请求头中需要添加“x-obs-security-token”字段；获取临时AK/SK和securitytoken参考获取临时AK/SK和securitytoken。|否|


签名的计算过程如下：

1.  构造请求字符串\(StringToSign\)。
2.  对第一步的结果进行UTF-8编码。
3.  使用SK对第二步的结果进行HMAC-SHA1签名计算。
4.  对第三步的结果进行Base64编码。
5.  对第四步的结果进行URL编码，得到签名。

请求字符串\(StringToSign\)按照如下规则进行构造，各个参数的含义如[表2](#table34479832212511)所示：

```
StringToSign = 
     HTTP-Verb + "\n" +   
     Content-MD5 + "\n" +   
     Content-Type + "\n" +   
     Expires + "\n" +   
     CanonicalizedHeaders +   CanonicalizedResource; 
```

**表 2**  构造StringToSign所需参数说明

|参数|描述|
|--|--|
|HTTP-Verb|指接口操作的方法，对REST接口而言，即为http请求操作的VERB，如："PUT"，"GET"，"DELETE"等字符串。|
|Content-MD5|按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串，可以为空。|
|Content-Type|内容类型，用于指定消息类型，例如： text/plain。当请求中不带该头域时，该参数按照空字符串处理。|
|Expires|临时授权的失效时间，即请求消息参数Expires的值ExpiresValue。|
|CanonicalizedHeaders|HTTP请求头域中的OBS请求头字段，即以“x-obs-”作为前辍的头域，如“x-obs-date，x-obs-acl，x-obs-meta-*”。请求头字段中关键字的所有字符要转为小写，需要添加多个字段时，要将所有字段按照关键字的字典序从小到大进行排序。在添加请求头字段时，如果有重名的字段，则需要进行合并。如：x-obs-meta-name:name1和x-obs-meta-name:name2，则需要先将重名字段的值（这里是name1和name2）以逗号分隔，合并成x-obs-meta-name:name1,name2。头域中的请求头字段中的关键字不允许含有非ASCII码或不可识别字符；请求头字段中的值也不建议使用非ASCII码或不可识别字符，如果一定要使用非ASCII码或不可识别字符，需要客户端自行做编解码处理，可以采用URL编码或者Base64编码，服务端不会做解码处理。当请求头字段中含有无意义空格或table键时，需要摒弃。例如：x-obs-meta-name: name（name前带有一个无意义空格），需要转换为：x-obs-meta-name:name每一个请求头字段最后都需要另起新行。|
|CanonicalizedResource|表示HTTP请求所指定的OBS资源，构造方式如下：<桶名+对象名>+[子资源]+ [子资源2] + ...桶名和对象名。通过桶绑定的自定义域名访问OBS，桶名由自定义域名表示，则为"/obs.ccc.com/object"，其中“obs.ccc.com”为桶绑定的自定义域名。如果没有对象名，如列举桶，则为"/obs.ccc.com/"；不是通过桶绑定的自定义域名访问OBS的场景，则为"/bucket/object"，如果没有对象名，如列举桶，则为"/bucket/"。如果桶名也没有，则为“/”。如果有子资源，则将子资源添加进来，例如?acl，?logging。OBS支持各种子资源，包括：CDNNotifyConfiguration, acl, append, attname, backtosource, cors, customdomain, delete, deletebucket, directcoldaccess, encryption, inventory, length, lifecycle, location, logging, metadata, modify, name, notification, partNumber, policy, position, quota, rename, replication, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, restore, storageClass, storagePolicy, storageinfo, tagging, torrent, truncate, uploadId, uploads, versionId, versioning, versions, website, x-image-process, x-image-save-bucket, x-image-save-object, x-obs-security-token, object-lock, retention。如果有多个子资源，在包含这些子资源时，需要首先将这些子资源按照其关键字的字典序从小到大排列，并使用**“&”**拼接。子资源通常是唯一的，不建议请求的URL包含多个相同关键字的子资源（例如，key=value1&key=value2），如果存在这种情况，OBS服务端签名时只会计算第一个子资源且也只有第一个子资源的值会对实际业务产生作用；以获取对象（GetObject）接口为例，假设桶名为bucket-test，对象名为object-test，对象的版本号为xxx，获取时需要重写Content-Type为text/plain，那么签名计算出的CanonicalizedResource为：/bucket-test/object-test?response-content-type=text/plain&versionId=xxx。|


根据请求字符串\(StringToSign\)和用户SK使用如下算法生成Signature，生成过程使用HMAC算法\(hash-based authentication code algorithm\)。

```
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) ) )
```

URL中的Signature计算方法和Header中携带的Authorization签名计算方法有两处不同：

-   URL中签名在Base64编码后还要经过URL编码。
-   StringToSign中的Expires和原来Authorization消息中的消息头Date对应。

使用URL携带签名方式为浏览器生成预定义的URL实例：

**表 3**  下载对象在URL中携带签名的请求及StringToSign

|请求消息头|StringToSign|
|--|--|
|GET /objectkey?AccessKeyId=MFyfvK41ba2giqM7Uio6PznpdUKGpownRZlmVmHc&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D HTTP/1.1Host: examplebucket.obs.cn-north-4.myhuaweicloud.com|GET \n\n\n1532779451\n/examplebucket/objectkey|


**表 4**  在URL中使用临时AK/SK和securitytoken下载对象请求及StringToSign

|请求消息头|StringToSign|
|--|--|
|GET /objectkey?AccessKeyId=MFyfvK41ba2giqM7Uio6PznpdUKGpownRZlmVmHc&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D&x-obs-security-token=YwkaRTbdY8g7q....  HTTP/1.1Host: examplebucket.obs.cn-north-4.myhuaweicloud.com|GET \n\n\n1532779451\n/examplebucket/objectkey?x-obs-security-token=YwkaRTbdY8g7q....|


根据签名计算规则

```
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) ) )
```

计算出签名，然后将Host作为URL的前缀，可以生成预定义的URL:

http\(s\)://examplebucket.obs.cn-north-4.myhuaweicloud.com/objectkey?AccessKeyId=AccessKeyID&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D

在浏览器中直接输入该地址则可以下载examplebucket桶中的objectkey对象。这个链接的有效期是1532779451\(Sat Jul 28 20:04:11 CST 2018\)。

在Linux环境上使用curl命令访问注意&字符需要\\转义，如下命令将对象objectkey下载到output文件中：

curl  http\(s\)://examplebucket.obs.cn-north-4.myhuaweicloud.com/objectkey?AccessKeyId=AccessKeyID\\&Expires=1532779451\\&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D  -X GET -o output

>![](public_sys-resources/icon-note.gif) **说明：** 
>如果想要在浏览器中使用URL中携带签名生成的预定义URL，则计算签名时不要使用只能携带在头域部分的“Content-MD5”、“Content-Type”、“CanonicalizedHeaders”来计算签名。否则浏览器不能携带这些参数，请求发送到服务端之后，会提示签名错误。

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
import java.util.regex.Pattern;

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

    private boolean isBucketNameValid(String bucketName) {
        if (bucketName == null || bucketName.length() > 63 || bucketName.length() < 3) {
            return false;
        }

        if (!Pattern.matches("^[a-z0-9][a-z0-9.-]+$", bucketName)) {
            return false;
        }

        if (Pattern.matches("(\\d{1,3}\\.){3}\\d{1,3}", bucketName)) {
            return false;
        }

        String[] fragments = bucketName.split("\\.");
        for (int i = 0; i < fragments.length; i++) {
            if (Pattern.matches("^-.*", fragments[i]) || Pattern.matches(".*-$", fragments[i])
                    || Pattern.matches("^$", fragments[i])) {
                return false;
            }
        }

        return true;
    }

    public String encodeUrlString(String path) throws UnsupportedEncodingException {
        return URLEncoder.encode(path, DEFAULT_ENCODING)
                .replaceAll("\\+", "%20")
                .replaceAll("\\*", "%2A")
                .replaceAll("%7E", "~");
    }

    public String encodeObjectName(String objectName) throws UnsupportedEncodingException {
        StringBuilder result = new StringBuilder();
        String[] tokens = objectName.split("/");
        for (int i = 0; i < tokens.length; i++) {
            result.append(this.encodeUrlString(tokens[i]));
            if (i < tokens.length - 1) {
                result.append("/");
            }
        }
        return result.toString();
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
                                String bucketName, String objectName, long expires) throws Exception { 
        String contentMd5 = ""; 
        String contentType = "";  
        TreeMap<String, String> canonicalizedHeaders = new TreeMap<String, String>(); 
        String key; 
        List<String> temp = new ArrayList<String>(); 
        for (Map.Entry<String, String[]> entry : headers.entrySet()) { 
            key = entry.getKey(); 
            if (key == null || entry.getValue() == null || entry.getValue().length == 0) { 
                continue; 
            } 
            key = key.trim().toLowerCase(Locale.ENGLISH); 
            if (key.equals("content-md5")) { 
                contentMd5 = entry.getValue()[0]; 
                continue; 
            } 
            if (key.equals("content-type")) { 
                contentType = entry.getValue()[0]; 
                continue; 
            } 
            if (key.startsWith(OBS_PREFIX)) { 
                for (String value : entry.getValue()) { 
                    if (value != null) { 
                        temp.add(value.trim()); 
                    } 
                } 
                canonicalizedHeaders.put(key, this.join(temp, ",")); 
                temp.clear(); 
            } 
        } 
        // handle method/content-md5/content-type
        StringBuilder stringToSign = new StringBuilder();
        stringToSign.append(httpMethod).append(SIGN_SEP)
                .append(contentMd5).append(SIGN_SEP)
                .append(contentType).append(SIGN_SEP)
                .append(expires).append(SIGN_SEP);


        // handle canonicalizedHeaders
        for (Map.Entry<String, String> entry : canonicalizedHeaders.entrySet()) {
            stringToSign.append(entry.getKey()).append(":").append(entry.getValue()).append(SIGN_SEP);
        }


        // handle CanonicalizedResource
        stringToSign.append("/");
        if (this.isValid(bucketName)) {
            stringToSign.append(bucketName).append("/");
            if (this.isValid(objectName)) {
                stringToSign.append(this.encodeObjectName(objectName));
            }
        }

        TreeMap<String, String> canonicalizedResource = new TreeMap<String, String>();
        for (Map.Entry<String, String> entry : queries.entrySet()) {
            key = entry.getKey();
            if (key == null) {
                continue;
            }

            if (SUB_RESOURCES.contains(key)) {
                canonicalizedResource.put(key, entry.getValue());
            }
        }

        if (canonicalizedResource.size() > 0) {
            stringToSign.append("?");
            for (Map.Entry<String, String> entry : canonicalizedResource.entrySet()) {
                stringToSign.append(entry.getKey());
                if (this.isValid(entry.getValue())) {
                    stringToSign.append("=").append(entry.getValue());
                }
                stringToSign.append("&");
            }
            stringToSign.deleteCharAt(stringToSign.length() - 1);
        }
        //		System.out.println(String.format("StringToSign:%s%s", SIGN_SEP, stringToSign.toString()));

        return stringToSign.toString();
    }

    public String querySignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries, 
                                  String bucketName, String objectName, long expires) throws Exception { 
         if (!isBucketNameValid(bucketName)) { 
             throw new IllegalArgumentException("the bucketName is illegal"); 
         } 
         //1. stringToSign 
         String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName, expires); 
  
         //2. signature 
         return this.encodeUrlString(this.hmacSha1(stringToSign)); 
     } 

    public String getURL(String endpoint, Map<String, String> queries,
                         String bucketName, String objectName, String signature, long expires) throws UnsupportedEncodingException {
        StringBuilder URL = new StringBuilder();
        URL.append("https://").append(bucketName).append(".").append(endpoint).append("/").
                append(this.encodeObjectName(objectName)).append("?");
        String key;
        for (Map.Entry<String, String> entry : queries.entrySet()) {
            key = entry.getKey();
            if (key == null) {
                continue;
            }
            if (SUB_RESOURCES.contains(key)) {
                String value = entry.getValue();
                URL.append(key);
                if (value != null) {
                    URL.append("=").append(value).append("&");
                } else {
                    URL.append("&");
                }
            }
        }
        URL.append("AccessKeyId=").append(this.ak).append("&Expires=").append(expires).
                append("&Signature=").append(signature);
        return URL.toString();
    }

    public static void main(String[] args) throws Exception {
        SignDemo demo = new SignDemo();

        /* 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；
        本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量HUAWEICLOUD_SDK_AK和HUAWEICLOUD_SDK_SK。*/
	demo.ak = System.getenv("HUAWEICLOUD_SDK_AK");
	demo.sk = System.getenv("HUAWEICLOUD_SDK_SK");
        String endpoint = "<your-endpoint>";

        String bucketName = "bucket-test";
        String objectName = "hello.jpg";

        // 如果直接使用URL在浏览器地址栏中访问，无法带上头域，此处headers加入头域会导致签名不匹配，使用headers需要客户端处理
        Map<String, String[]> headers = new HashMap<String, String[]>();
        Map<String, String> queries = new HashMap<String, String>();

        // 请求消息参数Expires，设置24小时后失效
        long expires = (System.currentTimeMillis() + 86400000L) / 1000;
        String signature = demo.querySignature("GET", headers, queries, bucketName, objectName, expires);
        System.out.println(signature);
        String URL = demo.getURL(endpoint, queries, bucketName, objectName, signature, expires);
        System.out.println(URL);
    }
}
```

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

