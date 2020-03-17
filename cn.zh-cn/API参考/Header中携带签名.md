# Header中携带签名<a name="obs_04_0010"></a>

OBS的所有API接口都可以通过在header中携带签名方式来进行身份认证，也是最常用的身份认证方式。

在Header中携带签名是指将通过HTTP消息中Authorization header头域携带签名信息，消息头域的格式为：

```
Authorization: OBS AccessKeyID:signature
```

签名的计算过程如下：

1、构造请求字符串\(StringToSign\)。

2、对第一步的结果进行UTF-8编码。

3、使用SK对第二步的结果进行HMAC-SHA1签名计算。

4、对第三步的结果进行Base64编码，得到签名。

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
<tr id="row14909112213405"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p132581298408"><a name="p132581298408"></a><a name="p132581298408"></a>Content-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p102601629204016"><a name="p102601629204016"></a><a name="p102601629204016"></a>按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串，具体请参见<a href="#table12510133817416">表6</a>以及表下方的计算方法示例。</p>
</td>
</tr>
<tr id="row1824493"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p13566274"><a name="p13566274"></a><a name="p13566274"></a>Content-Type</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p25126432"><a name="p25126432"></a><a name="p25126432"></a>内容类型，用于指定 消息类型，例如： text/plain。</p>
<p id="p24811297"><a name="p24811297"></a><a name="p24811297"></a>当请求中不带该头域时，该参数按照空字符串处理，见<a href="#table14775325212511">表2</a>。</p>
</td>
</tr>
<tr id="row63558046"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p28804613404"><a name="p28804613404"></a><a name="p28804613404"></a>Date</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p10901346204019"><a name="p10901346204019"></a><a name="p10901346204019"></a>生成请求的时间，该时间格式遵循RFC 1123；</p>
<p id="p792134614016"><a name="p792134614016"></a><a name="p792134614016"></a>当有自定义字段x-obs-date时，该参数按照空字符串处理；见<a href="#table12510133817416">表6</a>。</p>
<p id="p99420463401"><a name="p99420463401"></a><a name="p99420463401"></a>如果进行临时授权方式操作（如临时授权方式获取对象内容等操作）时，该参数不需要。</p>
</td>
</tr>
<tr id="row42990474"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p59676394"><a name="p59676394"></a><a name="p59676394"></a>CanonicalizedHeaders</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p1949763"><a name="p1949763"></a><a name="p1949763"></a>HTTP请求头域中的OBS请求头字段，即以“x-obs-”作为前辍的头域，如“x-obs-date，x-obs-acl，x-obs-meta-*”。</p>
<a name="ol145715617477"></a><a name="ol145715617477"></a><ol id="ol145715617477"><li>请求头字段中关键字的的所有字符要转为小写，需要添加多个字段时，要将所有字段按照关键字的字典序从小到大进行排序。</li><li>在添加请求头字段时，如果有重名的字段，则需要进行合并。如：x-obs-meta-name:name1和x-obs-meta-name:name2，则需要先将重名字段的值（这里是name1和name2）按照字典序从小到大排序后再以逗号分隔，合并成x-obs-meta-name:name1,name2。</li><li>头域中的请求头字段中的关键字不允许含有非ASCII码或不可识别字符；请求头字段中的值也不建议使用非ASCII码或不可识别字符，如果一定要使用非ASCII码或不可识别字符，需要客户端自行做编解码处理，可以采用URL编码或者Base64编码，服务端不会做解码处理。</li><li>当请求头字段中含有无意义空格或table键时，需要摒弃。例如：x-obs-meta-name: name（name前带有一个无意义空格），需要转换为：x-obs-meta-name:name</li><li>每一个请求头字段最后都需要另起新行，见<a href="#table46456687212511">表4</a></li></ol>
</td>
</tr>
<tr id="row7450793"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p66643399"><a name="p66643399"></a><a name="p66643399"></a>CanonicalizedResource</p>
</td>
<td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p29406249"><a name="p29406249"></a><a name="p29406249"></a>表示HTTP请求所指定的OBS资源，构造方式如下：</p>
<p id="p63329656"><a name="p63329656"></a><a name="p63329656"></a>&lt;桶名+对象名&gt;+[子资源1] + [子资源2] + ...</p>
<a name="ol135483613475"></a><a name="ol135483613475"></a><ol id="ol135483613475"><li>桶名和对象名。<a name="ul157841072717"></a><a name="ul157841072717"></a><ul id="ul157841072717"><li>通过桶绑定的自定义域名访问OBS，桶名由自定义域名表示，则为"/obs.ccc.com/object"，其中“obs.ccc.com”为桶绑定的自定义域名。如果没有对象名，如列举桶，则为"/obs.ccc.com/"；</li><li>不是通过桶绑定的自定义域名访问OBS的场景，则为"/bucket/object"，如果没有对象名，如列举桶，则为"/bucket/"。如果桶名也没有，则为“/”。</li></ul>
</li><li>如果有子资源，则将子资源添加进来，例如?acl，?logging。<p id="p1193056145515"><a name="p1193056145515"></a><a name="p1193056145515"></a>OBS支持各种子资源，包括：CDNNotifyConfiguration, acl, append, attname, backtosource, cors, customdomain, delete, deletebucket, directcoldaccess, encryption, inventory, length, lifecycle, location, logging, metadata, modify, name, notification, orchestration, partNumber, policy, position, quota, rename, replication, requestPayment, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, restore, select,  storageClass, storagePolicy, storageinfo, tagging, torrent, truncate, uploadId, uploads, versionId, versioning, versions, website, x-image-process, x-image-save-bucket, x-image-save-object, x-obs-security-token。</p>
</li><li>如果有多个子资源，在包含这些子资源时，需要首先将这些子资源按照其关键字的字典序从小到大排列，并使用<strong id="b1580113415404"><a name="b1580113415404"></a><a name="b1580113415404"></a>“&amp;”</strong>拼接。</li></ol>
<div class="note" id="note1239815267372"><a name="note1239815267372"></a><a name="note1239815267372"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul116221356133916"></a><a name="ul116221356133916"></a><ul id="ul116221356133916"><li>子资源通常是唯一的，不建议请求的URL包含多个相同关键字的子资源（例如，key=value1&amp;key=value2），如果存在这种情况，OBS服务端签名时只会计算第一个子资源且也只有第一个子资源的值会对实际业务产生作用；</li><li>以获取对象（GetObject）接口为例，假设桶名为bucket-test，对象名为object-test，对象的版本号为xxx，获取时需要重写Content-Type为text/plain，那么签名计算出的CanonicalizedResource为：/bucket-test/object-test?response-content-type=text/plain&amp;versionId=xxx。</li></ul>
</div></div>
</td>
</tr>
</tbody>
</table>

下面的几张表提供了一些生成StringToSign的例子。

**表 2**  获取对象

<a name="table14775325212511"></a>
<table><thead align="left"><tr id="row48189141"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p11006326"><a name="p11006326"></a><a name="p11006326"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p19097245"><a name="p19097245"></a><a name="p19097245"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row3372975"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p4775574"><a name="p4775574"></a><a name="p4775574"></a>GET /object.txt HTTP/1.1</p>
<p id="p42980173"><a name="p42980173"></a><a name="p42980173"></a>Host: bucket.obs.cn-north-4.myhuaweicloud.com</p>
<p id="p51277242"><a name="p51277242"></a><a name="p51277242"></a>Date: Sat, 12 Oct 2015 08:12:38 GMT</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p59815938"><a name="p59815938"></a><a name="p59815938"></a>GET \n</p>
<p id="p164481243202215"><a name="p164481243202215"></a><a name="p164481243202215"></a>\n</p>
<p id="p1472535"><a name="p1472535"></a><a name="p1472535"></a>\n</p>
<p id="p13252823"><a name="p13252823"></a><a name="p13252823"></a>Sat, 12 Oct 2015 08:12:38 GMT\n</p>
<p id="p52166545"><a name="p52166545"></a><a name="p52166545"></a>/bucket/object.txt</p>
</td>
</tr>
</tbody>
</table>

**表 3**  使用临时AK/SK和securitytoken上传对象

<a name="table25826370212511"></a>
<table><thead align="left"><tr id="row13863750"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p49222002"><a name="p49222002"></a><a name="p49222002"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p27559193"><a name="p27559193"></a><a name="p27559193"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row17702181"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1379614265212"><a name="p1379614265212"></a><a name="p1379614265212"></a>PUT /object.txt HTTP/1.1</p>
<p id="p19988723"><a name="p19988723"></a><a name="p19988723"></a>User-Agent: curl/7.15.5</p>
<p id="p11796122133515"><a name="p11796122133515"></a><a name="p11796122133515"></a>Host: bucket.obs.cn-north-4.myhuaweicloud.com</p>
<p id="p8473833"><a name="p8473833"></a><a name="p8473833"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT</p>
<p id="p15509910161817"><a name="p15509910161817"></a><a name="p15509910161817"></a><span>x-obs-security-token:</span> YwkaRTbdY8g7q....</p>
<p id="p9155637"><a name="p9155637"></a><a name="p9155637"></a>content-type: text/plain</p>
<p id="p15291872"><a name="p15291872"></a><a name="p15291872"></a>Content-Length: 5913339</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p30682111"><a name="p30682111"></a><a name="p30682111"></a>PUT\n</p>
<p id="p7703550"><a name="p7703550"></a><a name="p7703550"></a>\n</p>
<p id="p2223087"><a name="p2223087"></a><a name="p2223087"></a>text/plain\n</p>
<p id="p5775546153911"><a name="p5775546153911"></a><a name="p5775546153911"></a>\n</p>
<p id="p20007789"><a name="p20007789"></a><a name="p20007789"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\n</p>
<p id="p66077328189"><a name="p66077328189"></a><a name="p66077328189"></a><span>x-obs-security-token:</span>YwkaRTbdY8g7q....\n</p>
<p id="p45852376"><a name="p45852376"></a><a name="p45852376"></a>/bucket/object.txt</p>
<p id="p14535105184111"><a name="p14535105184111"></a><a name="p14535105184111"></a></p>
</td>
</tr>
</tbody>
</table>

**表 4**  带请求头字段上传对象

<a name="table46456687212511"></a>
<table><thead align="left"><tr id="row1033238"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p16583492"><a name="p16583492"></a><a name="p16583492"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p1085622"><a name="p1085622"></a><a name="p1085622"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row20826581"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p9231496"><a name="p9231496"></a><a name="p9231496"></a>PUT /object.txt HTTP/1.1</p>
<p id="p15974605"><a name="p15974605"></a><a name="p15974605"></a>User-Agent: curl/7.15.5</p>
<p id="p38071431163517"><a name="p38071431163517"></a><a name="p38071431163517"></a>Host: bucket.obs.cn-north-4.myhuaweicloud.com</p>
<p id="p18874618"><a name="p18874618"></a><a name="p18874618"></a>Date: Mon, 14 Oct 2015 12:08:34 GMT</p>
<p id="p35653836"><a name="p35653836"></a><a name="p35653836"></a>x-obs-acl: public-read</p>
<p id="p52449071"><a name="p52449071"></a><a name="p52449071"></a>content-type: text/plain</p>
<p id="p2279597"><a name="p2279597"></a><a name="p2279597"></a>Content-Length: 5913339</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p50429634"><a name="p50429634"></a><a name="p50429634"></a>PUT\n</p>
<p id="p51213523"><a name="p51213523"></a><a name="p51213523"></a>\n</p>
<p id="p58268531"><a name="p58268531"></a><a name="p58268531"></a>text/plain\n</p>
<p id="p54654738"><a name="p54654738"></a><a name="p54654738"></a>Mon, 14 Oct 2015 12:08:34 GMT\n</p>
<p id="p22130602"><a name="p22130602"></a><a name="p22130602"></a>x-obs-acl:public-read\n</p>
<p id="p64957690"><a name="p64957690"></a><a name="p64957690"></a>/bucket/object.txt</p>
</td>
</tr>
</tbody>
</table>

**表 5**  获取对象ACL

<a name="table47748300"></a>
<table><thead align="left"><tr id="row66793295"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p41547828"><a name="p41547828"></a><a name="p41547828"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p9930893"><a name="p9930893"></a><a name="p9930893"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row66204867"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p60993981"><a name="p60993981"></a><a name="p60993981"></a>GET /object.txt?acl HTTP/1.1</p>
<p id="p844914343518"><a name="p844914343518"></a><a name="p844914343518"></a>Host: bucket.obs.cn-north-4.myhuaweicloud.com</p>
<p id="p41565411"><a name="p41565411"></a><a name="p41565411"></a>Date: Sat, 12 Oct 2015 08:12:38 GMT</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p11355167"><a name="p11355167"></a><a name="p11355167"></a>GET \n</p>
<p id="p35087639"><a name="p35087639"></a><a name="p35087639"></a>\n</p>
<p id="p1478816075319"><a name="p1478816075319"></a><a name="p1478816075319"></a>\n</p>
<p id="p47353302"><a name="p47353302"></a><a name="p47353302"></a>Sat, 12 Oct 2015 08:12:38 GMT\n</p>
<p id="p23526540"><a name="p23526540"></a><a name="p23526540"></a>/bucket/object.txt?acl</p>
</td>
</tr>
</tbody>
</table>

**表 6**  上传对象且携带Content-MD5头域

<a name="table12510133817416"></a>
<table><thead align="left"><tr id="row45100381645"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p115720411659"><a name="p115720411659"></a><a name="p115720411659"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p457234112512"><a name="p457234112512"></a><a name="p457234112512"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row651113384416"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p35721411659"><a name="p35721411659"></a><a name="p35721411659"></a>PUT /object.txt HTTP/1.1</p>
<p id="p19311511115318"><a name="p19311511115318"></a><a name="p19311511115318"></a>Host: bucket.obs.cn-north-4.myhuaweicloud.com</p>
<p id="p657313411653"><a name="p657313411653"></a><a name="p657313411653"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT</p>
<p id="p75734411054"><a name="p75734411054"></a><a name="p75734411054"></a>Content-MD5: I5pU0r4+sgO9Emgl1KMQUg==</p>
<p id="p1757310411519"><a name="p1757310411519"></a><a name="p1757310411519"></a>Content-Length: 5913339</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1957316411258"><a name="p1957316411258"></a><a name="p1957316411258"></a>PUT\n</p>
<p id="p357324118513"><a name="p357324118513"></a><a name="p357324118513"></a>I5pU0r4+sgO9Emgl1KMQUg==\n</p>
<p id="p19573134115512"><a name="p19573134115512"></a><a name="p19573134115512"></a>\n</p>
<p id="p19713125114013"><a name="p19713125114013"></a><a name="p19713125114013"></a>\n</p>
<p id="p1657364111516"><a name="p1657364111516"></a><a name="p1657364111516"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\n</p>
<p id="p12573141352"><a name="p12573141352"></a><a name="p12573141352"></a>/bucket/object.txt</p>
</td>
</tr>
</tbody>
</table>

**表 7**  使用自定义域名方式上传对象

<a name="table83121210163615"></a>
<table><thead align="left"><tr id="row63121210133615"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p13312171014366"><a name="p13312171014366"></a><a name="p13312171014366"></a>请求消息头</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p3313210133612"><a name="p3313210133612"></a><a name="p3313210133612"></a>StringToSign</p>
</th>
</tr>
</thead>
<tbody><tr id="row53131810193615"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p19313101015361"><a name="p19313101015361"></a><a name="p19313101015361"></a>PUT /object.txt HTTP/1.1</p>
<p id="p429395923715"><a name="p429395923715"></a><a name="p429395923715"></a>Host: obs.ccc.com</p>
<p id="p15313210153615"><a name="p15313210153615"></a><a name="p15313210153615"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT</p>
<p id="p031311013362"><a name="p031311013362"></a><a name="p031311013362"></a>Content-MD5: I5pU0r4+sgO9Emgl1KMQUg==</p>
<p id="p93131010173616"><a name="p93131010173616"></a><a name="p93131010173616"></a>Content-Length: 5913339</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p131311023610"><a name="p131311023610"></a><a name="p131311023610"></a>PUT\n</p>
<p id="p16313131053619"><a name="p16313131053619"></a><a name="p16313131053619"></a>I5pU0r4+sgO9Emgl1KMQUg==\n</p>
<p id="p331314108369"><a name="p331314108369"></a><a name="p331314108369"></a>\n</p>
<p id="p2313161033613"><a name="p2313161033613"></a><a name="p2313161033613"></a>\n</p>
<p id="p83131310153620"><a name="p83131310153620"></a><a name="p83131310153620"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\n</p>
<p id="p0313121093620"><a name="p0313121093620"></a><a name="p0313121093620"></a>/obs.ccc.com/object.txt</p>
</td>
</tr>
</tbody>
</table>

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

import org.omg.CosNaming.IstringHelper;


public class SignDemo {
	
	private static final String SIGN_SEP = "\n";
	
	private static final String OBS_PREFIX = "x-obs-";
	
	private static final String DEFAULT_ENCODING = "UTF-8";
	
	private static final List<String> SUB_RESOURCES = Collections.unmodifiableList(Arrays.asList(
			"CDNNotifyConfiguration", "acl", "append", "attname", "backtosource", "cors", "customdomain", "delete",
			"deletebucket", "directcoldaccess", "encryption", "inventory", "length", "lifecycle", "location", "logging",
			"metadata", "modify", "name", "notification", "orchestration", "partNumber", "policy", "position", "quota",
			"rename", "replication", "requestPayment", "response-cache-control", "response-content-disposition",
			"response-content-encoding", "response-content-language", "response-content-type", "response-expires",
			"restore", "select", " storageClass", "storagePolicy", "storageinfo", "tagging", "torrent", "truncate",
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
				stringToSign.append(this.urlEncode(entry.getKey()));
				if(this.isValid(entry.getValue())) {
					stringToSign.append("=").append(this.urlEncode(entry.getValue()));
				}
			}
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
	
	public static void main(String[] args) throws Exception {
		
		SignDemo demo = new SignDemo();
		demo.ak = "<your-access-key-id>";
		demo.sk = "<your-securet-key-id>";
		
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
import sys
import hashlib
import hmac
import binascii
from datetime import datetime
IS_PYTHON2 = sys.version_info.major == 2 or sys.version < '3'

yourSecretAccessKeyID = '275hSvB6EEOorBNsMDEfOaICQnilYaPZhXUaSK64'
httpMethod = "PUT"
contentType = "application/xml"
# "date" is the time when the request was actually generated
date = datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
canonicalizedHeaders = "x-obs-acl:private"
CanonicalizedResource = "/newbucketname2"
canonical_string = httpMethod + "\n" + "\n" + contentType + "\n" + date + "\n" + canonicalizedHeaders + CanonicalizedResource
if IS_PYTHON2:    
     hashed = hmac.new(yourSecretAccessKeyID, canonical_string, hashlib.sha1)    
     encode_canonical = binascii.b2a_base64(hashed.digest())[:-1]
else:    
     hashed = hmac.new(yourSecretAccessKeyID.encode('UTF-8'), canonical_string.encode('UTF-8'),hashlib.sha1)    
     encode_canonical = binascii.b2a_base64(hashed.digest())[:-1].decode('UTF-8')
print encode_canonical
```

签名计算的样例结果为（按照执行时间的不同变化）：ydH8ffpcbS6YpeOMcEZfn0wE90c=

## C语言中签名的计算方法<a name="section657820586554"></a>

请单击[此处](https://obs-community.obs.cn-north-1.myhuaweicloud.com/sign/signature_c.zip)，下载C语言签名计算代码样例，其中：

1.  计算签名的接口包含在sign.h头文件中。
2.  计算签名的示例代码在main.c文件中。

## 签名计算工具<a name="section19121175184814"></a>

OBS提供可视化签名工具，帮助您轻松完成签名计算，请单击[这里](https://bbs.huaweicloud.com/forum/thread-13219-1-1.html)获取。

