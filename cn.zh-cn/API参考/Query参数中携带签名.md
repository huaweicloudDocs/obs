# Query参数中携带签名<a name="ZH-CN_TOPIC_0100846724"></a>

Query参数中携带签名：OBS服务支持用户构造一个特定操作的URL，这个URL中会包含用户AK、签名、有效期、资源等信息，任何拿到这个URL的人均可执行这个操作，OBS服务收到这个请求后认为该请求就是签发URL用户自己在执行操作。例如构造一个携带签名信息的下载对象的URL，拿到相应URL的人能下载这个对象，但该URL只在Expires指定的失效时间内有效。Query参数中携带签名的URL主要用于在不提供给其他人Secret Access Key的情况下，让其他人能用预签发的URL来进行身份认证，并执行预定义的操作。

Query参数中携带签名请求的消息格式如下：

```
GET /ObjectKey?AccessKeyId=AccessKeyID&Expires=ExpiresValue&Signature=signature HTTP/1.1
Host: bucketname.obs.cn-north-1.myhuaweicloud.com
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
<td class="cellrowborder" valign="top" width="58.160000000000004%" headers="mcps1.2.4.1.2 "><p id="p29130856"><a name="p29130856"></a><a name="p29130856"></a>临时授权失效的时间；临时授权失效的时间为24小时，非临时的授权时间可设置的最长时间为1年，但是如果含有了临时的AK，其授权失效时间最大值也只能为24小时；UTC时间，1970年1月1日零时之后的指定的Expires时间内有效（以秒为单位）。</p>
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
</tbody>
</table>

Query参数中携带对的签名计算方法

```
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) ) );  其中，StringToSign = 
     HTTP-Verb + "\n" +   
     Content-MD5 + "\n" +   
     Content-Type + "\n" +   
     Expires + "\n" +   
     CanonicalizedHeaders +   CanonicalizedResource; 
```

各个参数的含义如[表2](#table34479832212511)所示：

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
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p29516273427"><a name="p29516273427"></a><a name="p29516273427"></a>按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串。</p>
</td>
</tr>
<tr id="row1824493"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p13566274"><a name="p13566274"></a><a name="p13566274"></a>Content-Type</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p25126432"><a name="p25126432"></a><a name="p25126432"></a>内容类型，用于指定 消息类型，例如： text/plain。</p>
<p id="p24811297"><a name="p24811297"></a><a name="p24811297"></a>当请求中不带该头域时，该参数按照空字符串处理。</p>
</td>
</tr>
<tr id="row42990474"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p59676394"><a name="p59676394"></a><a name="p59676394"></a>CanonicalizedHeaders</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p1949763"><a name="p1949763"></a><a name="p1949763"></a>HTTP请求头字段，以“x-obs-”作为前辍的消息头，如“x-obs-date，x-obs-acl”。</p>
<a name="ol145715617477"></a><a name="ol145715617477"></a><ol id="ol145715617477"><li>自定义字段中的所有字符要转为小写，需要添加多个字段时，要将所有字段按照字典序进行排序。</li><li>在添加自定义字段时，如果有重名的字段，则需要进行合并。如：x-obs-meta-name:name1和x-obs-meta-name:name2，则需要合并成x-obs-meta-name:name1,name2。</li><li>当自定义字段中，含有非ASCII码或不可识别字符时，需进行Base64编码</li><li>当自定义字段中含有无意义空格或table键时，需要摒弃。例如：x-obs-meta-name: name（name前带有一个无意义空格），需要转换为：x-obs-meta-name:name</li><li>每一个自定义字段最后都需要另起新行。</li></ol>
</td>
</tr>
<tr id="row7450793"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p66643399"><a name="p66643399"></a><a name="p66643399"></a>CanonicalizedResource</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p29406249"><a name="p29406249"></a><a name="p29406249"></a>表示HTTP请求所指定的OBS资源，构造方式如下：</p>
<p id="p63329656"><a name="p63329656"></a><a name="p63329656"></a>&lt;桶名+对象名&gt;+[子资源]+[查询字符串]</p>
<a name="ol135483613475"></a><a name="ol135483613475"></a><ol id="ol135483613475"><li>桶名和对象名，例如：/bucket/object. 如果没有对象名，如列举桶。则为"/bucket/",如桶名也没有，则为“/”</li><li>如果有子资源，则将子资源添加进来，例如?acl，?logging。子资源包括acl, append, backtosource, cors, delete,deletebucket, lifecycle, location, logging, notification, partNumber, policy, position, quota, replication, requestPayment, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, restore, storageClass, storagePolicy, storageinfo, tagging, uploadId, uploads, versionId, versioning, versions, website,  x-image-process, x-obs-security-token, x-oss-process。</li><li>如有查询字符串那么将这些查询字符串及其请求值按照字典序从小到大排列。</li></ol>
</td>
</tr>
</tbody>
</table>

Query参数中的Signature计算方法和Header中携带的Authorization签名计算方法有两处不同：

-   Query参数中签名在Base64编码后还要经过URL编码。
-   StringToSign中的Expires和原来Authorization消息中的消息头Date对应。

```
StringToSign = HTTP-Verb + "\n" + Content-MD5 + "\n" + Content-Type + "\n" + Expire + "\n" + CanonicalizedHeaders + CanonicalizedResource
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) ) )
```

使用Query参数携带签名方式为浏览器生成预定义的URL实例：

**表 3**  下载对象在Query参数中携带签名的请求及StringToSign

<a name="table47748300"></a>
<table><thead align="left"><tr id="row66793295"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p41547828"><a name="p41547828"></a><a name="p41547828"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p9930893"><a name="p9930893"></a><a name="p9930893"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row66204867"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1769863585110"><a name="p1769863585110"></a><a name="p1769863585110"></a>GET /objectkey?AccessKeyId=AccessKeyID&amp;Expires=1532779451&amp;Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D  HTTP/1.1</p>
<p id="p16698113565110"><a name="p16698113565110"></a><a name="p16698113565110"></a>Host: examplebucket.obs.cn-north-1.myhuaweicloud.com</p>
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

根据签名计算规则

```
Signature = URL-Encode( Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) ) )
```

计算出签名，然后将Host作为URL的前缀，可以生成预定义的URL:

http\(s\)://examplebucket.obs.cn-north-1.myhuaweicloud.com/objectkey?AccessKeyId=AccessKeyID&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D

在浏览器中直接输入该地址则可以下载examplebucket桶中的objectkey对象。这个链接的有效期是1532779451\(Sat Jul 28 20:04:11 CST 2018\)。

>![](public_sys-resources/icon-note.gif) **说明：**   
>如果想要在浏览器中使用Query参数中携带签名生成的预定于URL，则计算签名时不要使用“Content-MD5”、“Content-Type”、“CanonicalizedHeaders”计算签名，否则浏览器不能携带这些参数，请求发送到服务端之后，会提示签名错误。  

