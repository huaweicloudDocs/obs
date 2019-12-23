# PUT上传<a name="ZH-CN_TOPIC_0100846775"></a>

## 功能介绍<a name="section5584184924715"></a>

上传对象操作是指在指定的桶内增加一个对象，执行该操作需要用户拥有桶的写权限。

>![](public_sys-resources/icon-note.gif) **说明：**   
>同一个桶中存储的对象名是唯一的，在桶未开启多版本的情况下，重复上传同名对象，前一次上传的对象将被后一次上传的对象覆盖。  

如果在指定的桶内已经有相同的对象键值的对象，用户上传的新对象会覆盖原来的对象；为了确保数据在传输过程中没有遭到破坏，用户可以在请求消息头中加入Content-MD5参数。在这种情况下，OBS收到上传的对象后，会对对象进行MD5校验，如果不一致则返回出错信息。

用户还可以在上传对象时指定x-obs-acl参数，设置对象的权限控制策略。如果匿名用户在上传对象时未指定x-obs-acl参数，则该对象默认可以被所有OBS用户访问。

该操作支持服务端加密功能。

用户在OBS系统中创建了桶之后，可以采用PUT操作的方式将对象上传到桶中。

单次上传对象大小范围是\[0, 5GB\]，如果需要上传超过5GB的大文件，需要通过[多段操作](多段操作.md)来分段上传。

## 与POST上传的区别<a name="section9125142514612"></a>

PUT上传中参数通过请求头域传递；POST上传则作为消息体中的表单域传递。

PUT上传需在URL中指定对象名；POST上传提交的URL为桶域名，无需指定对象名。两者的请求行分别为：

```
PUT /ObjectName HTTP/1.1
```

```
POST / HTTP/1.1
```

关于POST上传的更多详细信息，请参考[POST上传](POST上传.md)。

## 多版本<a name="section27143284"></a>

如果桶的多版本状态是开启的，系统会自动为对象生成一个唯一的版本号，并且会在响应报头x-obs-version-id返回该版本号。如果桶的多版本状态是暂停的，则对象的版本号为**null**。关于桶的多版本状态，参见[设置桶的多版本状态](设置桶的多版本状态.md)。

## 请求消息样式<a name="section42962965"></a>

```
PUT /ObjectName HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Content-Type: application/xml 
Content-Length: length
Authorization: authorization
Date: date
<Optional Additional Header> 
<object Content>
```

## 请求消息参数<a name="section51122366"></a>

该请求消息中不使用参数。

## 请求消息头<a name="section57448112"></a>

该请求可以使用附加的消息头，具体如[表1](#table21799862)所示。

**表 1**  请求消息头

<a name="table21799862"></a>
<table><thead align="left"><tr id="row34347226"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.1"><p id="p30661915"><a name="p30661915"></a><a name="p30661915"></a><strong id="b7521779"><a name="b7521779"></a><a name="b7521779"></a>消息头名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="66%" id="mcps1.2.4.1.2"><p id="p5284369"><a name="p5284369"></a><a name="p5284369"></a><strong id="b47559329"><a name="b47559329"></a><a name="b47559329"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="9%" id="mcps1.2.4.1.3"><p id="p27100472"><a name="p27100472"></a><a name="p27100472"></a><strong id="b42577656"><a name="b42577656"></a><a name="b42577656"></a>是否必选</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row26238096"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p44911008"><a name="p44911008"></a><a name="p44911008"></a>Content-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p13913041"><a name="p13913041"></a><a name="p13913041"></a>按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串。</p>
<p id="p58108509"><a name="p58108509"></a><a name="p58108509"></a>类型：字符串</p>
<p id="p53214538"><a name="p53214538"></a><a name="p53214538"></a>示例：n58IG6hfM7vqI4K0vnWpog==。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p15410356"><a name="p15410356"></a><a name="p15410356"></a>否</p>
</td>
</tr>
<tr id="row4475483"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p26969841"><a name="p26969841"></a><a name="p26969841"></a>x-obs-acl</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p37073483"><a name="p37073483"></a><a name="p37073483"></a>创建对象时，可以加上此消息头设置对象的权限控制策略，使用的策略为预定义的常用策略，包括：private；public-read；public-read-write（各策略详细说明见<a href="https://support.huaweicloud.com/devg-obs/zh-cn_topic_0101104050.html" target="_blank" rel="noopener noreferrer">使用头域设置ACL</a>）。</p>
<p id="p50162129"><a name="p50162129"></a><a name="p50162129"></a>类型：字符串</p>
<p id="p48805985"><a name="p48805985"></a><a name="p48805985"></a>说明：字符串形式的预定义策略。</p>
<p id="p331411337426"><a name="p331411337426"></a><a name="p331411337426"></a>实例x-obs-acl: public-read。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p60970709"><a name="p60970709"></a><a name="p60970709"></a>否</p>
</td>
</tr>
<tr id="row176201754161817"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p54102201376"><a name="p54102201376"></a><a name="p54102201376"></a>x-obs-grant-read</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p1041152010375"><a name="p1041152010375"></a><a name="p1041152010375"></a>创建对象时，使用此头域授权租户下所有用户有读对象和获取对象元数据的权限。</p>
<p id="p036992924111"><a name="p036992924111"></a><a name="p036992924111"></a>类型：字符串。</p>
<p id="p1245415214403"><a name="p1245415214403"></a><a name="p1245415214403"></a>实例x-obs-grant-read: id=domainID。如果授权给多个租户，需要通过','分割。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p341182017372"><a name="p341182017372"></a><a name="p341182017372"></a>否</p>
</td>
</tr>
<tr id="row1852810319198"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p2784192993712"><a name="p2784192993712"></a><a name="p2784192993712"></a>x-obs-grant-read-acp</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p6913194219811"><a name="p6913194219811"></a><a name="p6913194219811"></a>创建对象时，使用此头域授权租户下所有用户有获取对象ACL的权限。</p>
<p id="p49151332194119"><a name="p49151332194119"></a><a name="p49151332194119"></a>类型：字符串。</p>
<p id="p19223133034117"><a name="p19223133034117"></a><a name="p19223133034117"></a>实例x-obs-grant-read-acp: id=domainID。如果授权给多个租户，需要通过','分割。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p9785429153711"><a name="p9785429153711"></a><a name="p9785429153711"></a>否</p>
</td>
</tr>
<tr id="row1337219031911"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p4151526163710"><a name="p4151526163710"></a><a name="p4151526163710"></a>x-obs-grant-write-acp</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p94031856283"><a name="p94031856283"></a><a name="p94031856283"></a>创建对象时，使用此头域授权domain下所有用户有写对象ACL的权限。</p>
<p id="p79212366417"><a name="p79212366417"></a><a name="p79212366417"></a>类型：字符串。</p>
<p id="p95921443104120"><a name="p95921443104120"></a><a name="p95921443104120"></a>实例x-obs-grant-write-acp: id=domainID。如果授权给多个租户，需要通过','分割。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p1316182618370"><a name="p1316182618370"></a><a name="p1316182618370"></a>否</p>
</td>
</tr>
<tr id="row10662185731812"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p3389132314376"><a name="p3389132314376"></a><a name="p3389132314376"></a>x-obs-grant-full-control</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p1914315101898"><a name="p1914315101898"></a><a name="p1914315101898"></a>创建对象时，使用此头域授权domain下所有用户有读对象、获取对象元数据、获取对象ACL、写对象ACL的权限。</p>
<p id="p1284513399419"><a name="p1284513399419"></a><a name="p1284513399419"></a>类型：字符串。</p>
<p id="p428421618431"><a name="p428421618431"></a><a name="p428421618431"></a>实例x-obs-grant-full-control: id=domainID。如果授权给多个租户，需要通过','分割。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p12389102314371"><a name="p12389102314371"></a><a name="p12389102314371"></a>否</p>
</td>
</tr>
<tr id="row11865476"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p21579520"><a name="p21579520"></a><a name="p21579520"></a>x-obs-storage-class</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p3110729"><a name="p3110729"></a><a name="p3110729"></a>创建对象时，可以加上此头域设置对象的存储类型。如果未设置此头域，则以桶的默认存储类型作为对象的存储类型。</p>
<p id="p27996566"><a name="p27996566"></a><a name="p27996566"></a>类型：字符串</p>
<p id="p50642502"><a name="p50642502"></a><a name="p50642502"></a>说明：存储类型有3种：STANDARD（标准存储）、WARM（低频访问存储）、COLD（归档存储）。因此这里可配置的值有：STANDARD、WARM和COLD，注意大小写敏感。</p>
<p id="p53129340"><a name="p53129340"></a><a name="p53129340"></a>示例：x-obs-storage-class: STANDARD</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p8509283"><a name="p8509283"></a><a name="p8509283"></a>否</p>
</td>
</tr>
<tr id="row9474686"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p29252105"><a name="p29252105"></a><a name="p29252105"></a>x-obs-meta-*</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p20610280"><a name="p20610280"></a><a name="p20610280"></a>创建对象时，可以在HTTP请求中加入以“x-obs-meta-”开头的消息头，用来加入自定义的元数据，以便对对象进行自定义管理。当用户获取此对象或查询此对象元数据时，加入的自定义元数据将会在返回消息的头中出现。HTTP请求不包含消息体，长度不能超过8KB。</p>
<p id="p51274795"><a name="p51274795"></a><a name="p51274795"></a>类型：字符串</p>
<p id="p58819972"><a name="p58819972"></a><a name="p58819972"></a>示例：x-obs-meta-test: test metadata</p>
<p id="p7651164516420"><a name="p7651164516420"></a><a name="p7651164516420"></a>约束：请求头字段中的关键字不允许含有非ASCII码或不可识别字符，如果一定要使用非ASCII码或不可识别字符，需要客户端自行做编解码处理，可以采用URL编码或者Base64编码，服务端不会做解码处理。例如“中文”是非ASCII码，可以做URL编码为“%E4%B8%AD%E6%96%87”，头域x-obs-meta-%E4%B8%AD%E6%96%87: test%E4%B8%AD%E6%96%87。自定义元数据就是x-obs-meta-%E4%B8%AD%E6%96%87，服务端只会作为字符串处理，不会做解码。</p>
<p id="p101413441643"><a name="p101413441643"></a><a name="p101413441643"></a>说明：请求头支持大小写字母，服务端会把请求消息头的key转换成小写，value不变。例如：x-obs-meta-Test1: Test Meta1，设置成功之后，下载对象返回的消息头是：x-obs-meta-test1: Test Meta1。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p66797252"><a name="p66797252"></a><a name="p66797252"></a>否</p>
</td>
</tr>
<tr id="row64304357"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p41270423"><a name="p41270423"></a><a name="p41270423"></a>x-obs-website-redirect-location</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p54569953"><a name="p54569953"></a><a name="p54569953"></a>当桶设置了Website配置，可以将获取这个对象的请求重定向到桶内另一个对象或一个外部的URL，OBS将这个值从头域中取出，保存在对象的元数据中。</p>
<p id="p21367535"><a name="p21367535"></a><a name="p21367535"></a>例如，重定向请求到桶内另一对象：</p>
<p id="p58090092"><a name="p58090092"></a><a name="p58090092"></a>x-obs-website-redirect-location:/anotherPage.html</p>
<p id="p53048785"><a name="p53048785"></a><a name="p53048785"></a>或重定向请求到一个外部URL：</p>
<p id="p7677024"><a name="p7677024"></a><a name="p7677024"></a>x-obs-website-redirect-location:http://www.example.com/</p>
<p id="p1984352"><a name="p1984352"></a><a name="p1984352"></a>类型：字符串</p>
<p id="p17859171"><a name="p17859171"></a><a name="p17859171"></a>默认值：无</p>
<p id="p26514819"><a name="p26514819"></a><a name="p26514819"></a>约束：必须以“/”、“http://”或“https://”开头，长度不超过2KB。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p216739"><a name="p216739"></a><a name="p216739"></a>否</p>
</td>
</tr>
<tr id="row1950653"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p23785186"><a name="p23785186"></a><a name="p23785186"></a>x-obs-server-side-encryption</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p47551928"><a name="p47551928"></a><a name="p47551928"></a>使用该头域表示服务端加密是SSE-KMS方式。</p>
<p id="p25314173"><a name="p25314173"></a><a name="p25314173"></a>类型：字符串</p>
<p id="p26500966"><a name="p26500966"></a><a name="p26500966"></a>示例：x-obs-server-side-encryption：kms</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p66203541"><a name="p66203541"></a><a name="p66203541"></a>否。当使用SSE-KMS方式时，必选。</p>
</td>
</tr>
<tr id="row58960965"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p11108823"><a name="p11108823"></a><a name="p11108823"></a>x-obs-server-side-encryption-kms-key-id</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p27399486"><a name="p27399486"></a><a name="p27399486"></a>SSE-KMS方式下使用该头域，该头域表示主密钥，如果用户没有提供该头域，那么默认的主密钥将会被使用。</p>
<p id="p45268789"><a name="p45268789"></a><a name="p45268789"></a>类型：字符串</p>
<p id="p6679135313114"><a name="p6679135313114"></a><a name="p6679135313114"></a>支持两种格式的描述方式：</p>
<p id="p17964154220128"><a name="p17964154220128"></a><a name="p17964154220128"></a>1. regionID:domainID(租户ID):key/key_id 或者</p>
<p id="p090816596123"><a name="p090816596123"></a><a name="p090816596123"></a>2.key_id</p>
<p id="p558627121315"><a name="p558627121315"></a><a name="p558627121315"></a>其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是从<span>数据加密服务</span>创建的密钥ID。</p>
<p id="p17830152818144"><a name="p17830152818144"></a><a name="p17830152818144"></a>示例：</p>
<p id="p4765922"><a name="p4765922"></a><a name="p4765922"></a>1. x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0  或者</p>
<p id="p9607740151414"><a name="p9607740151414"></a><a name="p9607740151414"></a>2. x-obs-server-side-encryption-kms-key-id：4f1cd4de-ab64-4807-920a-47fc42e7f0d0</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p50495402"><a name="p50495402"></a><a name="p50495402"></a>否</p>
</td>
</tr>
<tr id="row51805439"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p35491065"><a name="p35491065"></a><a name="p35491065"></a>x-obs-server-side-encryption-customer-algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p56204044"><a name="p56204044"></a><a name="p56204044"></a>SSE-C方式下使用该头域，该头域表示加密使用的算法。</p>
<p id="p36074350"><a name="p36074350"></a><a name="p36074350"></a>类型：字符串</p>
<p id="p56233695"><a name="p56233695"></a><a name="p56233695"></a>示例：x-obs-server-side-encryption-customer-algorithm：AES256</p>
<p id="p36341208"><a name="p36341208"></a><a name="p36341208"></a>约束：需要和x-obs-server-side-encryption-customer-key， x-obs-server-side-encryption-customer-key-MD5一起使用。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p57956718"><a name="p57956718"></a><a name="p57956718"></a>否。当使用SSE-C方式时，必选</p>
</td>
</tr>
<tr id="row51848422"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p38972650"><a name="p38972650"></a><a name="p38972650"></a>x-obs-server-side-encryption-customer-key</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p2668111"><a name="p2668111"></a><a name="p2668111"></a>SSE-C方式下使用该头域，该头域表示加密使用的密钥。该密钥用于加密对象。</p>
<p id="p24013005"><a name="p24013005"></a><a name="p24013005"></a>类型：字符串</p>
<p id="p14790461"><a name="p14790461"></a><a name="p14790461"></a>示例：x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=</p>
<p id="p66005286"><a name="p66005286"></a><a name="p66005286"></a>约束：该头域由256-bit的密钥经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key-MD5一起使用。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p44827955"><a name="p44827955"></a><a name="p44827955"></a>否。当使用SSE-C方式时，必选。</p>
</td>
</tr>
<tr id="row798417"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p64671816"><a name="p64671816"></a><a name="p64671816"></a>x-obs-server-side-encryption-customer-key-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p3925735"><a name="p3925735"></a><a name="p3925735"></a>SSE-C方式下使用该头域，该头域表示加密使用的密钥的MD5值。MD5值用于验证密钥传输过程中没有出错。</p>
<p id="p35331622"><a name="p35331622"></a><a name="p35331622"></a>类型：字符串</p>
<p id="p49549143"><a name="p49549143"></a><a name="p49549143"></a>示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==</p>
<p id="p43289109"><a name="p43289109"></a><a name="p43289109"></a>约束: 该头域由密钥的128-bit MD5值经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key一起使用。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p16756929"><a name="p16756929"></a><a name="p16756929"></a>否。当使用SSE-C方式时，必选。</p>
</td>
</tr>
<tr id="row849053217272"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p16490173217273"><a name="p16490173217273"></a><a name="p16490173217273"></a>success-action-redirect</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p28747278"><a name="p28747278"></a><a name="p28747278"></a>此参数的值是一个URL，用于指定当此次请求操作成功响应后的重定向的地址。</p>
<a name="ul57398910"></a><a name="ul57398910"></a><ul id="ul57398910"><li>如果此参数值有效且操作成功，响应码为303，Location头域由此参数以及桶名、对象名、对象的ETag组成。</li><li>如果此参数值无效，则OBS忽略此参数的作用，响应码为204，Location头域为对象地址。</li></ul>
<p id="p34983438"><a name="p34983438"></a><a name="p34983438"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p134912032112711"><a name="p134912032112711"></a><a name="p134912032112711"></a>否</p>
</td>
</tr>
<tr id="row121411077571"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.1 "><p id="p1514215711573"><a name="p1514215711573"></a><a name="p1514215711573"></a>x-obs-expires</p>
</td>
<td class="cellrowborder" valign="top" width="66%" headers="mcps1.2.4.1.2 "><p id="p038312375711"><a name="p038312375711"></a><a name="p038312375711"></a>表示对象的过期时间，单位是天。过期之后对象会被自动删除。（从对象最后修改时间开始计算）</p>
<p id="p133831235577"><a name="p133831235577"></a><a name="p133831235577"></a>类型：整型。</p>
<p id="p638302312574"><a name="p638302312574"></a><a name="p638302312574"></a>示例：x-obs-expires:3</p>
</td>
<td class="cellrowborder" valign="top" width="9%" headers="mcps1.2.4.1.3 "><p id="p1014357105719"><a name="p1014357105719"></a><a name="p1014357105719"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 请求消息元素<a name="section47270964"></a>

该请求消息中不使用消息元素，在消息体中带的是对象的数据。

## 响应消息样式<a name="section22785500"></a>

```
HTTP/1.1 status_code
Content-Length: length
Content-Type: type
```

## 响应消息头<a name="section3742912"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

除公共响应消息头之外，还可能使用如[表2](#table24122936102344)中的消息头。

**表 2**  附加响应消息头

<a name="table24122936102344"></a>
<table><thead align="left"><tr id="row36471658"><th class="cellrowborder" valign="top" width="40.400000000000006%" id="mcps1.2.3.1.1"><p id="p1414299"><a name="p1414299"></a><a name="p1414299"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="59.599999999999994%" id="mcps1.2.3.1.2"><p id="p47449426"><a name="p47449426"></a><a name="p47449426"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row18198260"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p64772971"><a name="p64772971"></a><a name="p64772971"></a>x-obs-version-id</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p12119327"><a name="p12119327"></a><a name="p12119327"></a>对象的版本号。如果桶的多版本状态为开启，则会返回对象的版本号。</p>
<p id="p41965083"><a name="p41965083"></a><a name="p41965083"></a>类型：字符串</p>
</td>
</tr>
<tr id="row42141431"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p58012764"><a name="p58012764"></a><a name="p58012764"></a>x-obs-server-side-encryption</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p1413429"><a name="p1413429"></a><a name="p1413429"></a>如果服务端加密是SSE-KMS方式，响应包含该头域。</p>
<p id="p12720865"><a name="p12720865"></a><a name="p12720865"></a>类型：字符串</p>
<p id="p47378923"><a name="p47378923"></a><a name="p47378923"></a>示例：x-obs-server-side-encryption：kms</p>
</td>
</tr>
<tr id="row23757124"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p45278863"><a name="p45278863"></a><a name="p45278863"></a>x-obs-server-side-encryption-kms-key-id</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p43709291"><a name="p43709291"></a><a name="p43709291"></a>如果服务端加密是SSE-KMS方式，响应包含该头域，该头域表示主密钥。</p>
<p id="p119654525336"><a name="p119654525336"></a><a name="p119654525336"></a>类型：字符串</p>
<p id="p1399473215337"><a name="p1399473215337"></a><a name="p1399473215337"></a>格式为： regionID:domainID(租户ID):key/key_id. 其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是本次加密使用的密钥ID。</p>
<p id="p199941432173317"><a name="p199941432173317"></a><a name="p199941432173317"></a>示例： x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0</p>
</td>
</tr>
<tr id="row50791679"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p20485364"><a name="p20485364"></a><a name="p20485364"></a>x-obs-server-side-encryption-customer-algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p48701810"><a name="p48701810"></a><a name="p48701810"></a>如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的算法。</p>
<p id="p35663107"><a name="p35663107"></a><a name="p35663107"></a>类型：字符串</p>
<p id="p52532512"><a name="p52532512"></a><a name="p52532512"></a>示例：x-obs-server-side-encryption-customer-algorithm：AES256</p>
</td>
</tr>
<tr id="row3030560"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p44148826"><a name="p44148826"></a><a name="p44148826"></a>x-obs-server-side-encryption-customer-key-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p19285144"><a name="p19285144"></a><a name="p19285144"></a>如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的密钥的MD5值。</p>
<p id="p39348572"><a name="p39348572"></a><a name="p39348572"></a>类型：字符串</p>
<p id="p18592835"><a name="p18592835"></a><a name="p18592835"></a>示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==</p>
</td>
</tr>
<tr id="row33117788"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p65295189"><a name="p65295189"></a><a name="p65295189"></a>x-obs-storage-class</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p54418926"><a name="p54418926"></a><a name="p54418926"></a>对象为非标准存储对象时，会返回此头域，可取值为：WARM或者COLD</p>
<p id="p20008286"><a name="p20008286"></a><a name="p20008286"></a>类型：字符串</p>
</td>
</tr>
</tbody>
</table>

## 响应消息元素<a name="section33686208"></a>

该请求的响应消息不带消息元素。

## 错误响应消息<a name="section34740423"></a>

该请求的返回无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例1<a name="section14482163815396"></a>

**上传对象**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:11:15 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例1<a name="section11653102613112"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF2600000164364C10805D385E1E3C67
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: 32AAAWJAMAABAAAQAAEAABAAAQAAEAABCTzu4Jp2lquWuXsjnLyPPiT3cfGhqPoY
Date: WED, 01 Jul 2015 04:11:15 GMT
Content-Length: 0
```

## 请求示例2<a name="section9978114711117"></a>

**上传对象的同时设置ACL**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:13:55 GMT
x-obs-grant-read:id=52f24s3593as5730ea4f722483579ai7,id=a93fcas852f24s3596ea8366794f7224
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例2<a name="section17245101261216"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164845759E4F3B39ABEE55E
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSReVRNuas0knI+Y96iXrZA7BLUgj06Z
Date: WED, 01 Jul 2015 04:13:55 GMT
Content-Length: 0
```

## 请求示例3<a name="section74231427201219"></a>

**上传指定存储类型的对象**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:15:07 GMT
x-obs-storage-class: WARM
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例3<a name="section1526805513128"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164846A2112F98BF970AA7E
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: a39E0UgAIAABAAAQAAEAABAAAQAAEAABCTPOUJu5XlNyU32fvKjM/92MQZK2gtoB
Date: WED, 01 Jul 2015 04:15:07 GMT
Content-Length: 0
```

## 请求示例4<a name="section18923277137"></a>

**桶开启多版本时上传对象**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-storage-class: WARM
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例4<a name="section16530173215133"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
ETag: "d41d8cd98f00b204e9800998ecf8427e"
X-OBS-ID-2: GcVgfeOJHx8JZHTHrRqkPsbKdB583fYbr3RBbHT6mMrBstReVILBZbMAdLiBYy1l
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
Content-Length: 0
```

## 请求示例5<a name="section17724204519133"></a>

**上传对象时携带MD5**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:17:50 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10
Content-MD5: 6Afx/PgtEy+bsBjKZzihnw==
Expect: 100-continue

1234567890
```

## 响应示例5<a name="section3283216161415"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164B165971F91D82217D105
X-OBS-ID-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSEKhBpS4BB3dSMNqMtuNxQDD9XvOw5h
ETag: "1072e1b96b47d7ec859710068aa70d57"
Date: WED, 01 Jul 2015 04:17:50 GMT
Content-Length: 0
```

## 请求示例6<a name="section2272113211413"></a>

**桶设置了Website配置，上传对象时设置下载对象时重定向**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-website-redirect-location: http://www.example.com/
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例6<a name="section632052520159"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTmxB5ufMj/7/GzP8TFwTbp33u0xhn2Z
ETag: "1072e1b96b47d7ec859710068aa70d57"
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
Content-Length: 0
```

## 请求示例7<a name="section9838237181513"></a>

**在URL中携带签名并上传对象**

```
PUT /object02?AccessKeyId=H4IPJX0TQTHTHEBQQCEC&Expires=1532688887&Signature=EQmDuOhWLUrzrzRNZxwS72CXeXM%3D HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Content-Length: 1024

[1024 Byte data content]
```

## 响应示例7<a name="section96529021618"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTmxB5ufMj/7/GzP8TFwTbp33u0xhn2Z
ETag: "1072e1b96b47d7ec859710068aa70d57"
Date: Fri, 27 Jul 2018 10:52:31 GMT
x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
Content-Length: 0
```

