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

<a name="table5447121714296"></a>
<table><thead align="left"><tr id="row1072131"><th class="cellrowborder" valign="top" width="25.509999999999998%" id="mcps1.2.4.1.1"><p id="p19733807"><a name="p19733807"></a><a name="p19733807"></a><strong id="b43386543"><a name="b43386543"></a><a name="b43386543"></a>参数名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="58.160000000000004%" id="mcps1.2.4.1.2"><p id="p24649069"><a name="p24649069"></a><a name="p24649069"></a><strong id="b20515029"><a name="b20515029"></a><a name="b20515029"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="16.33%" id="mcps1.2.4.1.3"><p id="p51104671"><a name="p51104671"></a><a name="p51104671"></a><strong id="b57288858"><a name="b57288858"></a><a name="b57288858"></a>是否必选</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row9885913"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p62561513"><a name="p62561513"></a><a name="p62561513"></a>AccessKeyId</p>
</td>
<td class="cellrowborder" valign="top" width="58.160000000000004%" headers="mcps1.2.4.1.2 "><p id="p34317810"><a name="p34317810"></a><a name="p34317810"></a>签发者的AK信息。OBS根据AK确定签发者的身份，并认为URL就是签发者在访问。</p>
<p id="p40424835"><a name="p40424835"></a><a name="p40424835"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="16.33%" headers="mcps1.2.4.1.3 "><p id="p53186163"><a name="p53186163"></a><a name="p53186163"></a>是</p>
</td>
</tr>
<tr id="row8913420"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p50898414"><a name="p50898414"></a><a name="p50898414"></a>Expires</p>
</td>
<td class="cellrowborder" valign="top" width="58.160000000000004%" headers="mcps1.2.4.1.2 "><p id="p29130856"><a name="p29130856"></a><a name="p29130856"></a>临时授权失效的时间；临时授权失效的时间为24小时，但是如果含有了临时的AK，其授权失效时间最大值也只能为24小时；UTC时间，1970年1月1日零时之后的指定的Expires时间内有效（以秒为单位）。</p>
<p id="p60851118"><a name="p60851118"></a><a name="p60851118"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="16.33%" headers="mcps1.2.4.1.3 "><p id="p29993536"><a name="p29993536"></a><a name="p29993536"></a>是</p>
</td>
</tr>
<tr id="row1506375"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p54907514"><a name="p54907514"></a><a name="p54907514"></a>Signature</p>
</td>
<td class="cellrowborder" valign="top" width="58.160000000000004%" headers="mcps1.2.4.1.2 "><p id="p18323687"><a name="p18323687"></a><a name="p18323687"></a>根据用户SK、Expires等参数计算出的签名信息。</p>
<p id="p30695458"><a name="p30695458"></a><a name="p30695458"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="16.33%" headers="mcps1.2.4.1.3 "><p id="p3304150"><a name="p3304150"></a><a name="p3304150"></a>是</p>
</td>
</tr>
<tr id="row142296248158"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p1722982419150"><a name="p1722982419150"></a><a name="p1722982419150"></a><span>x-obs-security-token</span></p>
</td>
<td class="cellrowborder" valign="top" width="58.160000000000004%" headers="mcps1.2.4.1.2 "><p id="p1322942441515"><a name="p1322942441515"></a><a name="p1322942441515"></a><span>使用临时AK/SK鉴权时，临时AK/SK和securitytoken必须同时使用，请求头中需要添加“x-obs-security-token”字段</span>；</p>
<p id="p917413528398"><a name="p917413528398"></a><a name="p917413528398"></a>获取临时AK/SK和securitytoken参考<a href="https://support.huaweicloud.com/api-iam/iam_04_0002.html" target="_blank" rel="noopener noreferrer">获取临时AK/SK和securitytoken</a>。</p>
</td>
<td class="cellrowborder" valign="top" width="16.33%" headers="mcps1.2.4.1.3 "><p id="p192295249152"><a name="p192295249152"></a><a name="p192295249152"></a>否</p>
</td>
</tr>
</tbody>
</table>

签名的计算过程如下：

1、构造请求字符串\(StringToSign\)。

2、对第一步的结果进行UTF-8编码。

3、使用SK对第二步的结果进行HMAC-SHA1签名计算。

4、对第三步的结果进行Base64编码。

5、对第四步的结果进行URL编码，得到签名。

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

<a name="table34479832212511"></a>
<table><thead align="left"><tr id="row42478738"><th class="cellrowborder" valign="top" width="18%" id="mcps1.2.3.1.1"><p id="p18225769"><a name="p18225769"></a><a name="p18225769"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="82%" id="mcps1.2.3.1.2"><p id="p67001213"><a name="p67001213"></a><a name="p67001213"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row58389173"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p31902586"><a name="p31902586"></a><a name="p31902586"></a>HTTP-Verb</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p33972659"><a name="p33972659"></a><a name="p33972659"></a>指接口操作的方法，对REST接口而言，即为http请求操作的VERB，如："PUT"，"GET"，"DELETE"等字符串。</p>
</td>
</tr>
<tr id="row101952243422"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p595111278426"><a name="p595111278426"></a><a name="p595111278426"></a>Content-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p29516273427"><a name="p29516273427"></a><a name="p29516273427"></a>按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串，可以为空。</p>
</td>
</tr>
<tr id="row1824493"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p13566274"><a name="p13566274"></a><a name="p13566274"></a>Content-Type</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p25126432"><a name="p25126432"></a><a name="p25126432"></a>内容类型，用于指定消息类型，例如： text/plain。</p>
<p id="p24811297"><a name="p24811297"></a><a name="p24811297"></a>当请求中不带该头域时，该参数按照空字符串处理。</p>
</td>
</tr>
<tr id="row106651047155213"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p4666144765219"><a name="p4666144765219"></a><a name="p4666144765219"></a>Expires</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p106661347145210"><a name="p106661347145210"></a><a name="p106661347145210"></a>临时授权的失效时间，即请求消息参数Expires的值ExpiresValue。</p>
</td>
</tr>
<tr id="row42990474"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p59676394"><a name="p59676394"></a><a name="p59676394"></a>CanonicalizedHeaders</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p1949763"><a name="p1949763"></a><a name="p1949763"></a>HTTP请求头域中的OBS请求头字段，即以“x-obs-”作为前辍的头域，如“x-obs-date，x-obs-acl，x-obs-meta-*”。</p>
<a name="ol145715617477"></a><a name="ol145715617477"></a><ol id="ol145715617477"><li>请求头字段中关键字的所有字符要转为小写，需要添加多个字段时，要将所有字段按照关键字的字典序从小到大进行排序。</li><li>在添加请求头字段时，如果有重名的字段，则需要进行合并。如：x-obs-meta-name:name1和x-obs-meta-name:name2，则需要先将重名字段的值（这里是name1和name2）以逗号分隔，合并成x-obs-meta-name:name1,name2。</li><li>头域中的请求头字段中的关键字不允许含有非ASCII码或不可识别字符；请求头字段中的值也不建议使用非ASCII码或不可识别字符，如果一定要使用非ASCII码或不可识别字符，需要客户端自行做编解码处理，可以采用URL编码或者Base64编码，服务端不会做解码处理。</li><li>当请求头字段中含有无意义空格或table键时，需要摒弃。例如：x-obs-meta-name: name（name前带有一个无意义空格），需要转换为：x-obs-meta-name:name</li><li>每一个请求头字段最后都需要另起新行。</li></ol>
</td>
</tr>
<tr id="row7450793"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p66643399"><a name="p66643399"></a><a name="p66643399"></a>CanonicalizedResource</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p29406249"><a name="p29406249"></a><a name="p29406249"></a>表示HTTP请求所指定的OBS资源，构造方式如下：</p>
<p id="p63329656"><a name="p63329656"></a><a name="p63329656"></a>&lt;桶名+对象名&gt;+[子资源]+ [子资源2] + ...</p>
<a name="ol135483613475"></a><a name="ol135483613475"></a><ol id="ol135483613475"><li>桶名和对象名。<a name="ul157841072717"></a><a name="ul157841072717"></a><ul id="ul157841072717"><li>通过桶绑定的自定义域名访问OBS，桶名由自定义域名表示，则为"/obs.ccc.com/object"，其中“obs.ccc.com”为桶绑定的自定义域名。如果没有对象名，如列举桶，则为"/obs.ccc.com/"；</li><li>不是通过桶绑定的自定义域名访问OBS的场景，则为"/bucket/object"，如果没有对象名，如列举桶，则为"/bucket/"。如果桶名也没有，则为“/”。</li></ul>
</li><li>如果有子资源，则将子资源添加进来，例如?acl，?logging。<p id="p167755915411"><a name="p167755915411"></a><a name="p167755915411"></a>OBS支持各种子资源，包括：CDNNotifyConfiguration, acl, append, attname, backtosource, cors, customdomain, delete, deletebucket, directcoldaccess, encryption, inventory, length, lifecycle, location, logging, metadata, modify, name, notification, partNumber, policy, position, quota, rename, replication, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, restore, storageClass, storagePolicy, storageinfo, tagging, torrent, truncate, uploadId, uploads, versionId, versioning, versions, website, x-image-process, x-image-save-bucket, x-image-save-object, x-obs-security-token。</p>
</li><li>如果有多个子资源，在包含这些子资源时，需要首先将这些子资源按照其关键字的字典序从小到大排列，并使用<strong id="b1580113415404"><a name="b1580113415404"></a><a name="b1580113415404"></a>“&amp;”</strong>拼接。</li></ol>
<div class="note" id="note196756717914"><a name="note196756717914"></a><a name="note196756717914"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul116221356133916"></a><a name="ul116221356133916"></a><ul id="ul116221356133916"><li>子资源通常是唯一的，不建议请求的URL包含多个相同关键字的子资源（例如，key=value1&amp;key=value2），如果存在这种情况，OBS服务端签名时只会计算第一个子资源且也只有第一个子资源的值会对实际业务产生作用；</li><li>以获取对象（GetObject）接口为例，假设桶名为bucket-test，对象名为object-test，对象的版本号为xxx，获取时需要重写Content-Type为text/plain，那么签名计算出的CanonicalizedResource为：/bucket-test/object-test?response-content-type=text/plain&amp;versionId=xxx。</li></ul>
</div></div>
</td>
</tr>
</tbody>
</table>

根据请求字符串\(StringToSign\)和用户SK使用如下算法生成Signature，生成过程使用HMAC算法\(hash-based authentication code algorithm\)。

```
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) ) )
```

URL中的Signature计算方法和Header中携带的Authorization签名计算方法有两处不同：

-   URL中签名在Base64编码后还要经过URL编码。
-   StringToSign中的Expires和原来Authorization消息中的消息头Date对应。

使用URL携带签名方式为浏览器生成预定义的URL实例：

**表 3**  下载对象在URL中携带签名的请求及StringToSign

<a name="table47748300"></a>
<table><thead align="left"><tr id="row66793295"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p41547828"><a name="p41547828"></a><a name="p41547828"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p9930893"><a name="p9930893"></a><a name="p9930893"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row66204867"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p422518916476"><a name="p422518916476"></a><a name="p422518916476"></a>GET /objectkey?AccessKeyId=<span>MFyfvK41ba2giqM7Uio6PznpdUKGpownRZlmVmHc</span>&amp;Expires=1532779451&amp;Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D HTTP/1.1</p>
<p id="p16698113565110"><a name="p16698113565110"></a><a name="p16698113565110"></a>Host: examplebucket.obs.cn-north-4.myhuaweicloud.com</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p11355167"><a name="p11355167"></a><a name="p11355167"></a>GET \n</p>
<p id="p35087639"><a name="p35087639"></a><a name="p35087639"></a>\n</p>
<p id="p15827441520"><a name="p15827441520"></a><a name="p15827441520"></a>\n</p>
<p id="p47353302"><a name="p47353302"></a><a name="p47353302"></a>1532779451\n</p>
<p id="p23526540"><a name="p23526540"></a><a name="p23526540"></a>/examplebucket/objectkey</p>
</td>
</tr>
</tbody>
</table>

**表 4**  在URL中使用临时AK/SK和securitytoken下载对象请求及StringToSign

<a name="table104365472404"></a>
<table><thead align="left"><tr id="row84376477405"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p643774764016"><a name="p643774764016"></a><a name="p643774764016"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p977482218417"><a name="p977482218417"></a><a name="p977482218417"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row19437547184013"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p131218290418"><a name="p131218290418"></a><a name="p131218290418"></a>GET /objectkey?AccessKeyId=<span>MFyfvK41ba2giqM7Uio6PznpdUKGpownRZlmVmHc</span>&amp;Expires=1532779451&amp;Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D&amp;<span>x-obs-security-token=</span>YwkaRTbdY8g7q....  HTTP/1.1</p>
<p id="p1612112915418"><a name="p1612112915418"></a><a name="p1612112915418"></a>Host: examplebucket.obs.cn-north-4.myhuaweicloud.com</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p12133293414"><a name="p12133293414"></a><a name="p12133293414"></a>GET \n</p>
<p id="p2137294411"><a name="p2137294411"></a><a name="p2137294411"></a>\n</p>
<p id="p181352954119"><a name="p181352954119"></a><a name="p181352954119"></a>\n</p>
<p id="p151392964112"><a name="p151392964112"></a><a name="p151392964112"></a>1532779451\n</p>
<p id="p31318296418"><a name="p31318296418"></a><a name="p31318296418"></a>/examplebucket/objectkey?<span>x-obs-security-token=</span>YwkaRTbdY8g7q....</p>
</td>
</tr>
</tbody>
</table>

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

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

import org.omg.CosNaming.IstringHelper;


public class SignDemo {
	
	private static final String SIGN_SEP = "\n";
	
	private static final String OBS_PREFIX = "x-obs-";
	
	private static final String DEFAULT_ENCODING = "UTF-8";
	
	private static final List<String> SUB_RESOURCES = Collections.unmodifiableList(Arrays.asList(
			"CDNNotifyConfiguration", "acl", "append", "attname", "backtosource", "cors", "customdomain", "delete",
			"deletebucket", "directcoldaccess", "encryption", "inventory", "length", "lifecycle", "location", "logging",
			"metadata", "modify", "name", "notification", "orchestration", "partNumber", "policy", "position", "quota",
			"rename", "replication", "response-cache-control", "response-content-disposition",
			"response-content-encoding", "response-content-language", "response-content-type", "response-expires",
			"restore", " storageClass", "storagePolicy", "storageinfo", "tagging", "torrent", "truncate",
			"uploadId", "uploads", "versionId", "versioning", "versions", "website", "x-image-process",
			"x-image-save-bucket", "x-image-save-object", "x-obs-security-token"));
	
	private String ak;
	
	private String sk;
	
	 public String urlEncode(String input) throws UnsupportedEncodingException
    {
		return URLEncoder.encode(input, DEFAULT_ENCODING)
        .replaceAll("%7E", "~") //for browser
        .replaceAll("%2F", "/");
    }
	
	private String join(List<?> items, String delimiter)
    {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < items.size(); i++)
        {
	String item = items.get(i).toString();
            sb.append(item);
            if (i < items.size() - 1)
            {
                sb.append(delimiter);
            }
        }
        return sb.toString();
    }
	
	private boolean isValid(String input) {
		return input != null && !input.equals("");
	}
	
	public String hamcSha1(String input) throws NoSuchAlgorithmException, InvalidKeyException, UnsupportedEncodingException {
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
		
//		System.out.println(String.format("StringToSign:%s%s", SIGN_SEP, stringToSign.toString()));
		
		return stringToSign.toString();
	}
	
	public String headerSignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
			String bucketName, String objectName) throws Exception {

		//1. stringToSign
		String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName);
		
		//2. signature
		return String.format("OBS %s:%s", this.ak, this.hamcSha1(stringToSign));
	}
	
	public String querySignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
			String bucketName, String objectName, long expires) throws Exception {
		if(headers.containsKey("x-obs-date")) {
			headers.put("x-obs-date", new String[] {String.valueOf(expires)});
		}else {
			headers.put("date", new String[] {String.valueOf(expires)});
		}
		//1. stringToSign
		String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName);
		
		//2. signature
		return this.urlEncode(this.hamcSha1(stringToSign));
	}

        public String getURL(String endpoint, Map<String, String> queries,
                String bucketName, String objectName, String signature, long expires) {
                StringBuilder URL = new StringBuilder();
                URL.append("https://").append(bucketName).append(".").append(endpoint).append("/").        
                    append(objectName).append("?");    
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
		demo.ak = "<your-access-key-id>";
		demo.sk = "<your-secret-key-id>";
                String endpoint = "<your-endpoint>";
		
		String bucketName = "bucket-test";
		String objectName = "hello.jpg";
                // 若直接使用URL在浏览器地址栏中访问，无法带上头域，此处headers加入头域会导致签名不匹配，使用headers需要客户端处理
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

## 签名计算工具<a name="section19121175184814"></a>

OBS提供[可视化签名工具](https://obs-community.obs.cn-north-1.myhuaweicloud.com/sign/query_signature.html)，帮助您轻松完成签名计算。

