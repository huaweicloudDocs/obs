# POST上传<a name="obs_04_0081"></a>

## 功能介绍<a name="section1534875573"></a>

上传对象操作是指在指定的桶内增加一个对象，执行该操作需要用户拥有桶的写权限。

>![](public_sys-resources/icon-note.gif) **说明：** 
>同一个桶中存储的对象名是唯一的。

在桶未开启多版本的情况下，如果在指定的桶内已经有相同的对象键值的对象，用户上传的新对象会覆盖原来的对象；为了确保数据在传输过程中没有遭到破坏，用户可以在表单域中加入Content-MD5参数。在这种情况下，OBS收到上传的对象后，会对对象进行MD5校验，如果不一致则返回出错信息。用户还可以在上传对象时指定x-obs-acl参数，设置对象的权限控制策略。

用户除了可以用PUT直接上传对象外，还可以使用POST上传对象。

单次上传对象大小范围是\[0, 5GB\]，如果需要上传超过5GB的大文件，需要通过[多段操作](多段操作.md)来分段上传。

该操作支持服务端加密功能。

## 与PUT上传的区别<a name="section9125142514612"></a>

PUT上传中参数通过请求头域传递；POST上传则作为消息体中的表单域传递。

PUT上传需在URL中指定对象名；POST上传提交的URL为桶域名，无需指定对象名。两者的请求行分别为：

```
PUT /ObjectName HTTP/1.1
```

```
POST / HTTP/1.1
```

关于PUT上传的更多详细信息，请参考[PUT上传](PUT上传.md)。

## 多版本<a name="section28789840"></a>

如果桶的多版本状态是开启的，系统会自动为对象生成一个唯一的版本号；如果桶的多版本状态是暂停的，则系统生成的对象版本号为**null**，并由响应报头x-obs-version-id返回该版本号。关于桶的多版本状态，参见[设置桶的多版本状态](设置桶的多版本状态.md)。

## 请求消息样式<a name="section57781973"></a>

```
POST / HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
User-Agent: browser_data
Accept: file_types
Accept-Language: Regions
Accept-Encoding: encoding
Accept-Charset: character_set
Keep-Alive: 300 
Connection: keep-alive 
Content-Type: multipart/form-data; boundary=9431149156168 
Content-Length: length


--9431149156168 
Content-Disposition: form-data; name="key" 

acl 
--9431149156168 
Content-Disposition: form-data; name="success_action_redirect"
 
success_redirect 
--9431149156168 
Content-Disposition: form-data; name="content-Type" 

content_type 
--9431149156168 
Content-Disposition: form-data; name="x-obs-meta-uuid" 

uuid 
--9431149156168 
Content-Disposition: form-data; name="x-obs-meta-tag" 

metadata 
--9431149156168 
Content-Disposition: form-data; name="AccessKeyId" 

access-key-id 
--9431149156168 
Content-Disposition: form-data; name="policy" 

encoded_policy 
--9431149156168 
Content-Disposition: form-data; name="signature" 

signature= 
--9431149156168 
Content-Disposition: form-data; name="file"; filename="MyFilename" 
Content-Type: image/jpeg 

file_content 
--9431149156168 
Content-Disposition: form-data; name="submit" 

Upload to OBS 
--9431149156168--
```

## 请求消息参数<a name="section50275709"></a>

该请求消息中不使用参数。

## 请求消息头<a name="section49828203"></a>

该请求使用公共的消息头，具体请参见[表3](构造请求.md#table25197309)。

如果想要获取CORS配置信息，则需要使用的消息头如下[表1](#table45572552212656)所示。

**表 1**  获取CORS配置的请求消息头

<a name="table45572552212656"></a>
<table><thead align="left"><tr id="row6497363"><th class="cellrowborder" valign="top" width="23.23%" id="mcps1.2.4.1.1"><p id="p56524405"><a name="p56524405"></a><a name="p56524405"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="55.559999999999995%" id="mcps1.2.4.1.2"><p id="p15074116"><a name="p15074116"></a><a name="p15074116"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="21.21%" id="mcps1.2.4.1.3"><p id="p13043879"><a name="p13043879"></a><a name="p13043879"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row49921287"><td class="cellrowborder" valign="top" width="23.23%" headers="mcps1.2.4.1.1 "><p id="p17092427"><a name="p17092427"></a><a name="p17092427"></a>Origin</p>
</td>
<td class="cellrowborder" valign="top" width="55.559999999999995%" headers="mcps1.2.4.1.2 "><p id="p42309340"><a name="p42309340"></a><a name="p42309340"></a>预请求指定的跨域请求Origin（通常为域名）。</p>
<p id="p45239740"><a name="p45239740"></a><a name="p45239740"></a>类型：String</p>
</td>
<td class="cellrowborder" valign="top" width="21.21%" headers="mcps1.2.4.1.3 "><p id="p40540330"><a name="p40540330"></a><a name="p40540330"></a>是</p>
</td>
</tr>
<tr id="row29318658"><td class="cellrowborder" valign="top" width="23.23%" headers="mcps1.2.4.1.1 "><p id="p26001129"><a name="p26001129"></a><a name="p26001129"></a>Access-Control-Request-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="55.559999999999995%" headers="mcps1.2.4.1.2 "><p id="p25716667"><a name="p25716667"></a><a name="p25716667"></a>实际请求可以带的HTTP头域，可以带多个头域。</p>
<p id="p30123417"><a name="p30123417"></a><a name="p30123417"></a>类型：String</p>
</td>
<td class="cellrowborder" valign="top" width="21.21%" headers="mcps1.2.4.1.3 "><p id="p24077689"><a name="p24077689"></a><a name="p24077689"></a>否</p>
</td>
</tr>
</tbody>
</table>

>![](public_sys-resources/icon-note.gif) **说明：** 
>配置后如果仍然提示跨域，请参考[为什么配置了跨域资源共享（CORS）仍然报错](https://support.huaweicloud.com/obs_faq/obs_faq_0163.html)处理。

## 请求消息元素<a name="section45800647"></a>

该请求消息的消息元素以表单形式组织，表单字段的具体含义如[表2](#table13225554)所示。

**表 2**  请求消息表单元素

<a name="table13225554"></a>
<table><thead align="left"><tr id="row41460348"><th class="cellrowborder" valign="top" width="29.592959295929592%" id="mcps1.2.4.1.1"><p id="p2845010"><a name="p2845010"></a><a name="p2845010"></a><strong id="b25605098"><a name="b25605098"></a><a name="b25605098"></a>参数名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="61.22612261226122%" id="mcps1.2.4.1.2"><p id="p60747054"><a name="p60747054"></a><a name="p60747054"></a><strong id="b9852581"><a name="b9852581"></a><a name="b9852581"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="9.180918091809183%" id="mcps1.2.4.1.3"><p id="p59861617"><a name="p59861617"></a><a name="p59861617"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row16952842"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p31002967"><a name="p31002967"></a><a name="p31002967"></a>file</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p28212417"><a name="p28212417"></a><a name="p28212417"></a>上传的对象的内容。</p>
<p id="p52585164"><a name="p52585164"></a><a name="p52585164"></a>类型：二进制或文本类型。</p>
<p id="p3504431"><a name="p3504431"></a><a name="p3504431"></a>约束条件：此参数必须为最后一个参数，否则此参数之后的参数会被丢弃；一个请求中只能含有一个file参数。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p15423498"><a name="p15423498"></a><a name="p15423498"></a>是</p>
</td>
</tr>
<tr id="row4593755"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p36549892"><a name="p36549892"></a><a name="p36549892"></a>key</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p7751245"><a name="p7751245"></a><a name="p7751245"></a>通过此请求创建的对象名称。</p>
<p id="p2652341"><a name="p2652341"></a><a name="p2652341"></a>类型：String</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p13513041"><a name="p13513041"></a><a name="p13513041"></a>是</p>
</td>
</tr>
<tr id="row54508512"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p53113338"><a name="p53113338"></a><a name="p53113338"></a>AccessKeyId</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p7213141"><a name="p7213141"></a><a name="p7213141"></a>用来指明请求发起者的Access Key。</p>
<p id="p64918274"><a name="p64918274"></a><a name="p64918274"></a>类型：String</p>
<p id="p47393561"><a name="p47393561"></a><a name="p47393561"></a>约束条件：如果该请求包括安全策略参数policy或signature时，则必须包括此参数。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p13673196"><a name="p13673196"></a><a name="p13673196"></a>是，有条件</p>
</td>
</tr>
<tr id="row55949908"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p35648708"><a name="p35648708"></a><a name="p35648708"></a>policy</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p1864216"><a name="p1864216"></a><a name="p1864216"></a>该请求的安全策略描述。policy格式请参考<a href="基于浏览器上传的表单中携带签名.md">基于浏览器上传的表单中携带签名</a>章节中policy格式</p>
<p id="p16777947"><a name="p16777947"></a><a name="p16777947"></a>类型：String</p>
<p id="p13921113310250"><a name="p13921113310250"></a><a name="p13921113310250"></a>限制：当Bucket提供了AccessKeyId(或signature)表单域时，则必须包括此参数。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p16836481"><a name="p16836481"></a><a name="p16836481"></a>是，有条件</p>
</td>
</tr>
<tr id="row026063319302"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p9260233123017"><a name="p9260233123017"></a><a name="p9260233123017"></a>signature</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p1526019339302"><a name="p1526019339302"></a><a name="p1526019339302"></a><span>根据StringToSign计算出的签名字符串。</span></p>
<p id="p106094963211"><a name="p106094963211"></a><a name="p106094963211"></a>类型：String</p>
<p id="p19452104992617"><a name="p19452104992617"></a><a name="p19452104992617"></a>限制：当Bucket提供了AccessKeyId(或policy)表单域时，则必须包括此参数。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p45121221183218"><a name="p45121221183218"></a><a name="p45121221183218"></a>是，有条件</p>
</td>
</tr>
<tr id="row1411464215313"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p191141242135310"><a name="p191141242135310"></a><a name="p191141242135310"></a>token</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p12955112314016"><a name="p12955112314016"></a><a name="p12955112314016"></a>用来统一指明请求发起者的Access Key，请求签名和请求的安全策略。token的优先级高于单独指定的Access Key，请求签名和请求的安全策略。</p>
<p id="p5114194213536"><a name="p5114194213536"></a><a name="p5114194213536"></a>类型：String</p>
<p id="p110131685015"><a name="p110131685015"></a><a name="p110131685015"></a>示例：</p>
<p id="p742117507500"><a name="p742117507500"></a><a name="p742117507500"></a>HTML中：&lt;input type="text" name="token" value="ak:signature:policy" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p9114242135313"><a name="p9114242135313"></a><a name="p9114242135313"></a>否</p>
</td>
</tr>
<tr id="row23452063"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p20568952"><a name="p20568952"></a><a name="p20568952"></a>x-obs-acl</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p55472450"><a name="p55472450"></a><a name="p55472450"></a>创建对象时，可以加上此消息头设置对象的权限控制策略，使用的策略为预定义的常用策略，包括：private；public-read；public-read-write；public-read-delivered ; public-read-write-delivered（各策略详细说明见<a href="https://support.huaweicloud.com/perms-cfg-obs/obs_40_0005.html" target="_blank" rel="noopener noreferrer">ACL</a>章节的“使用头域设置ACL”）。</p>
<p id="p64083493"><a name="p64083493"></a><a name="p64083493"></a>类型：String</p>
<p id="p39880527"><a name="p39880527"></a><a name="p39880527"></a>示例：</p>
<p id="p23380424"><a name="p23380424"></a><a name="p23380424"></a>POLICY中：{"acl": "public-read" },</p>
<p id="p9097225"><a name="p9097225"></a><a name="p9097225"></a>HTML中：&lt;input type="text" name="acl" value="public-read" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p65786607"><a name="p65786607"></a><a name="p65786607"></a>否</p>
</td>
</tr>
<tr id="row4410152019377"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p54102201376"><a name="p54102201376"></a><a name="p54102201376"></a>x-obs-grant-read</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p1041152010375"><a name="p1041152010375"></a><a name="p1041152010375"></a>创建对象时，使用此头域授权domain下所有用户有读对象和获取对象元数据的权限。</p>
<p id="p036992924111"><a name="p036992924111"></a><a name="p036992924111"></a>类型：String</p>
<p id="p20377112974111"><a name="p20377112974111"></a><a name="p20377112974111"></a>示例：</p>
<p id="p1638592915417"><a name="p1638592915417"></a><a name="p1638592915417"></a>POLICY中：{"grant-read": "id=domainId1" },</p>
<p id="p63921129194114"><a name="p63921129194114"></a><a name="p63921129194114"></a>HTML中：&lt;input type="text" name="grant-read" value="id=domainId1" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p341182017372"><a name="p341182017372"></a><a name="p341182017372"></a>否</p>
</td>
</tr>
<tr id="row97841629153720"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p2784192993712"><a name="p2784192993712"></a><a name="p2784192993712"></a>x-obs-grant-read-acp</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p6913194219811"><a name="p6913194219811"></a><a name="p6913194219811"></a>创建对象时，使用此头域授权domain下所有用户有获取对象ACL的权限。</p>
<p id="p49151332194119"><a name="p49151332194119"></a><a name="p49151332194119"></a>类型：String</p>
<p id="p1592233214412"><a name="p1592233214412"></a><a name="p1592233214412"></a>示例：</p>
<p id="p393093224115"><a name="p393093224115"></a><a name="p393093224115"></a>POLICY中：{"grant-read-acp": "id=domainId1" },</p>
<p id="p1293763284113"><a name="p1293763284113"></a><a name="p1293763284113"></a>HTML中：&lt;input type="text" name="grant-read-acp" value="id=domainId1" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p9785429153711"><a name="p9785429153711"></a><a name="p9785429153711"></a>否</p>
</td>
</tr>
<tr id="row8153268371"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p4151526163710"><a name="p4151526163710"></a><a name="p4151526163710"></a>x-obs-grant-write-acp</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p94031856283"><a name="p94031856283"></a><a name="p94031856283"></a>创建对象时，使用此头域授权domain下所有用户有写对象ACL的权限。</p>
<p id="p79212366417"><a name="p79212366417"></a><a name="p79212366417"></a>类型：String</p>
<p id="p1393019361411"><a name="p1393019361411"></a><a name="p1393019361411"></a>示例：</p>
<p id="p10939123614413"><a name="p10939123614413"></a><a name="p10939123614413"></a>POLICY中：{"grant-write-acp": "id=domainId1" },</p>
<p id="p59500366415"><a name="p59500366415"></a><a name="p59500366415"></a>HTML中：&lt;input type="text" name="grant-write-acp" value="id=domainId1" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p1316182618370"><a name="p1316182618370"></a><a name="p1316182618370"></a>否</p>
</td>
</tr>
<tr id="row9388182319372"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p3389132314376"><a name="p3389132314376"></a><a name="p3389132314376"></a>x-obs-grant-full-control</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p1914315101898"><a name="p1914315101898"></a><a name="p1914315101898"></a>创建对象时，使用此头域授权domain下所有用户有读对象、获取对象元数据、获取对象ACL、写对象ACL的权限。</p>
<p id="p1284513399419"><a name="p1284513399419"></a><a name="p1284513399419"></a>类型：String</p>
<p id="p1585473914116"><a name="p1585473914116"></a><a name="p1585473914116"></a>示例：</p>
<p id="p9863839104112"><a name="p9863839104112"></a><a name="p9863839104112"></a>POLICY中：{"grant-full-control": "id=domainId1" },</p>
<p id="p387333954111"><a name="p387333954111"></a><a name="p387333954111"></a>HTML中：&lt;input type="text" name="grant-full-control" value="id=domainId1" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p12389102314371"><a name="p12389102314371"></a><a name="p12389102314371"></a>否</p>
</td>
</tr>
<tr id="row55208559"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p42708291"><a name="p42708291"></a><a name="p42708291"></a>x-obs-storage-class</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p36819576"><a name="p36819576"></a><a name="p36819576"></a>创建对象时，可以加上此头域设置对象的存储类型。如果未设置此头域，则以桶的默认存储类型作为对象的存储类型。</p>
<p id="p62940734"><a name="p62940734"></a><a name="p62940734"></a>类型：String</p>
<p id="p29595702"><a name="p29595702"></a><a name="p29595702"></a>说明：存储类型有3种：STANDARD（标准存储）、WARM（低频访问存储）、COLD（归档存储）。因此这里可配置的值有：STANDARD、WARM和COLD，注意大小写敏感。</p>
<p id="p65034727"><a name="p65034727"></a><a name="p65034727"></a>示例：</p>
<p id="p48441636"><a name="p48441636"></a><a name="p48441636"></a>POLICY中：{"storage-class": "STANDARD" },</p>
<p id="p33321540"><a name="p33321540"></a><a name="p33321540"></a>HTML中：&lt;input type="text" name="x-obs-storage-class" value="STANDARD" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p14690238"><a name="p14690238"></a><a name="p14690238"></a>否</p>
</td>
</tr>
<tr id="row65103281"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p38874400"><a name="p38874400"></a><a name="p38874400"></a>Cache-Control,</p>
<p id="p14325287"><a name="p14325287"></a><a name="p14325287"></a>Content-Type,</p>
<p id="p61818720"><a name="p61818720"></a><a name="p61818720"></a>Content-Disposition,</p>
<p id="p19497574"><a name="p19497574"></a><a name="p19497574"></a>Content-Encoding</p>
<p id="p92111354122920"><a name="p92111354122920"></a><a name="p92111354122920"></a>Expires</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p35799650"><a name="p35799650"></a><a name="p35799650"></a>这5个参数是HTTP标准消息头，OBS将这些参数记录下来，当用户下载此对象或Head Object时，在响应消息头中携带这些参数。</p>
<p id="p53761394"><a name="p53761394"></a><a name="p53761394"></a>类型：String</p>
<p id="p14090498"><a name="p14090498"></a><a name="p14090498"></a>示例：</p>
<p id="p59705619"><a name="p59705619"></a><a name="p59705619"></a>POLICY中：["starts-with", "$Content-Type", "text/"],</p>
<p id="p479662"><a name="p479662"></a><a name="p479662"></a>HTML中：&lt;input type="text" name="content-type" value="text/plain" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p38852687"><a name="p38852687"></a><a name="p38852687"></a>否</p>
</td>
</tr>
<tr id="row14129871"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p3668922"><a name="p3668922"></a><a name="p3668922"></a>success_action_redirect</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p28747278"><a name="p28747278"></a><a name="p28747278"></a>此参数的值是一个URL，用于指定当此次请求操作成功响应后的重定向的地址。</p>
<a name="ul57398910"></a><a name="ul57398910"></a><ul id="ul57398910"><li>如果此参数值有效且操作成功，响应码为303，Location头域由此参数以及桶名、对象名、对象的ETag组成。</li><li>如果此参数值无效，则OBS忽略此参数的作用，响应码为204，Location头域为对象地址。</li></ul>
<p id="p34983438"><a name="p34983438"></a><a name="p34983438"></a>类型：String</p>
<p id="p46415489"><a name="p46415489"></a><a name="p46415489"></a>示例：</p>
<p id="p15086219"><a name="p15086219"></a><a name="p15086219"></a>POLICY中：{"success_action_redirect": "http://123458.com"},</p>
<p id="p1558245"><a name="p1558245"></a><a name="p1558245"></a>HTML中：&lt;input type="text" name="success_action_redirect" value="http://123458.com" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p59109014"><a name="p59109014"></a><a name="p59109014"></a>否</p>
</td>
</tr>
<tr id="row62219078"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p6580564"><a name="p6580564"></a><a name="p6580564"></a>x-obs-meta-*</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p63263715"><a name="p63263715"></a><a name="p63263715"></a>创建对象时，可以在HTTP请求中加入“x-obs-meta-”消息头或以“x-obs-meta-”开头的消息头，用来加入自定义的元数据，以便对对象进行自定义管理。当用户获取此对象或查询此对象元数据时，加入的自定义元数据将会在返回消息的消息头中出现。更多说明详见<a href="https://support.huaweicloud.com/ugobs-obs/obs_41_0025.html" target="_blank" rel="noopener noreferrer">对象自定义元数据介绍</a>。</p>
<p id="p32502531"><a name="p32502531"></a><a name="p32502531"></a>类型：String</p>
<p id="p24087323"><a name="p24087323"></a><a name="p24087323"></a>示例：</p>
<p id="p15459317"><a name="p15459317"></a><a name="p15459317"></a>POLICY中：{" x-obs-meta-test ": " test metadata " },</p>
<p id="p4916131"><a name="p4916131"></a><a name="p4916131"></a>HTML中：&lt;input type="text" name=" x-obs-meta-test " value=" test metadata " /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p62662307"><a name="p62662307"></a><a name="p62662307"></a>否</p>
</td>
</tr>
<tr id="row123451324134712"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p4346324184714"><a name="p4346324184714"></a><a name="p4346324184714"></a>x-obs-persistent-headers</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p131182482477"><a name="p131182482477"></a><a name="p131182482477"></a><span>创建对象时，可以在</span><span>HTTP</span><span>请求中加入</span><span>“x-obs-persistent-headers”</span><span>消息头，用来加入一个或多个自定义的响应头，当用户获取此对象或查询此对象元数据时，加入的自定义响应头将会在返回消息的头域中出现。</span></p>
<p id="p84948414535"><a name="p84948414535"></a><a name="p84948414535"></a><span>类型：String</span></p>
<p id="p1353812159536"><a name="p1353812159536"></a><a name="p1353812159536"></a><span>格式：</span><span>x-obs-persistent-headers: key1:base64_encode(value1),key2:base64_encode(value2)....</span></p>
<p id="p16502951155516"><a name="p16502951155516"></a><a name="p16502951155516"></a><span>说明：其中</span><span>key1/key2</span><span>等为自定义</span><span>header</span><span>，若含有非</span><span>ASCII</span><span>码或不可识别字符，可以采用</span><span>URL</span><span>编码或者</span><span>Base64</span><span>编码，服务端只会作为字符串处理，不会做解码。</span><span>value1/value2</span><span>等为对应自定义</span><span>header</span><span>的值，</span><span>base64_encode</span><span>指做</span><span>base64</span><span>编码，即将自定义</span><span>header</span><span>和对应值的</span><span>base64</span><span>编码作为一个</span><span>key-value</span><span>对用</span><span>“:”</span><span>连接，然后用</span><span>“,”</span><span>将所有的</span><span>key-value</span><span>对连接起来，放在</span><span>x-obs-persistent-headers</span><span>这个</span><span>header</span><span>中即可，服务端会对上传的value做解码处理。</span></p>
<p id="p177331724175311"><a name="p177331724175311"></a><a name="p177331724175311"></a><span>示例：</span></p>
<p id="p85819101103"><a name="p85819101103"></a><a name="p85819101103"></a><span>POLICY</span><span>中：</span><span>{"x-obs-persistent-headers": "key1:dmFsdWUx,key2:dmFsdWUy" },</span></p>
<p id="p658710100"><a name="p658710100"></a><a name="p658710100"></a><span>HTML</span><span>中：</span><span>&lt;</span><span>input type="text" name="x-obs-persistent-headers" value="key1:dmFsdWUx,key2:dmFsdWUy" /</span><span>&gt;</span></p>
<p id="p295283133319"><a name="p295283133319"></a><a name="p295283133319"></a><span>下载此对象或获取此对象元数据时：返回两个头域分别为</span><span>“key1:value1”</span><span>与</span><span>“key2:value2”</span></p>
<p id="p021318214576"><a name="p021318214576"></a><a name="p021318214576"></a><span>约束：</span></p>
<p id="p321319217572"><a name="p321319217572"></a><a name="p321319217572"></a><span>1. </span><span>通过该方式指定的自定义响应头不能以</span><span>“x-obs-”</span><span>为前缀，比如可以指定</span><span>“key1”</span><span>，但是不能指定</span><span>“x-obs-key1”</span></p>
<p id="p521312119578"><a name="p521312119578"></a><a name="p521312119578"></a><span>2. </span><span>不能指定</span><span>http</span><span>标准头，例如</span><span>host/content-md5/origin/range/Content-Disposition</span><span>等</span></p>
<p id="p221302117570"><a name="p221302117570"></a><a name="p221302117570"></a><span>3. </span><span>此头域和自定义元数据总长度不能超过</span><span>8KB</span></p>
<p id="p16213321185717"><a name="p16213321185717"></a><a name="p16213321185717"></a><span>4. </span><span>如果传入相同</span><span>key</span><span>，将</span><span>value</span><span>以</span><span>“,”</span><span>拼接后放入同一个</span><span>key</span><span>中返回</span></p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p1734642410477"><a name="p1734642410477"></a><a name="p1734642410477"></a>否</p>
</td>
</tr>
<tr id="row27089856"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p46794728"><a name="p46794728"></a><a name="p46794728"></a>success_action_status</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p32276637"><a name="p32276637"></a><a name="p32276637"></a>这个参数指定成功响应的状态码，允许设定的值为200，201，204。</p>
<a name="ul22054279"></a><a name="ul22054279"></a><ul id="ul22054279"><li>如果此参数值被设定为200或204，OBS响应消息中body为空。</li><li>如果此参数值被设定为201，则OBS响应消息中包含一个XML文档描述此次请求的响应。</li><li>当请求不协带此参数或参数无效时，OBS响应码为204。</li></ul>
<p id="p11419181"><a name="p11419181"></a><a name="p11419181"></a>类型：String</p>
<p id="p35663766"><a name="p35663766"></a><a name="p35663766"></a>示例：</p>
<p id="p52538440"><a name="p52538440"></a><a name="p52538440"></a>POLICY中：["starts-with", "$success_action_status", ""],</p>
<p id="p3083916"><a name="p3083916"></a><a name="p3083916"></a>HTML中：&lt;input type="text" name="success_action_status" value="200" /&gt;</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p48470680"><a name="p48470680"></a><a name="p48470680"></a>否</p>
</td>
</tr>
<tr id="row33582936"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p35863325"><a name="p35863325"></a><a name="p35863325"></a>x-obs-website-redirect-location</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p19248235"><a name="p19248235"></a><a name="p19248235"></a>当桶设置了Website配置，可以将获取这个对象的请求重定向到桶内另一个对象或一个外部的URL，OBS将这个值从头域中取出，保存在对象的元数据中。</p>
<p id="p39016388"><a name="p39016388"></a><a name="p39016388"></a>默认值：无</p>
<p id="p15603177"><a name="p15603177"></a><a name="p15603177"></a>约束：必须以“/”、“http://”或“https://”开头，长度不超过2K。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p55897791"><a name="p55897791"></a><a name="p55897791"></a>否</p>
</td>
</tr>
<tr id="row33318075"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p14409545"><a name="p14409545"></a><a name="p14409545"></a>x-obs-server-side-encryption</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p26322500"><a name="p26322500"></a><a name="p26322500"></a>使用该头域表示服务端加密是SSE-KMS方式。</p>
<p id="p35575909"><a name="p35575909"></a><a name="p35575909"></a>类型：String</p>
<p id="p51747731"><a name="p51747731"></a><a name="p51747731"></a>示例：x-obs-server-side-encryption：kms</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p30816671"><a name="p30816671"></a><a name="p30816671"></a>否。当使用SSE-KMS方式时，必选。</p>
</td>
</tr>
<tr id="row8914583"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p50992584"><a name="p50992584"></a><a name="p50992584"></a>x-obs-server-side-encryption-kms-key-id</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p36758634"><a name="p36758634"></a><a name="p36758634"></a>SSE-KMS方式下使用该头域，该头域表示主密钥，如果用户没有提供该头域，那么默认的主密钥将会被使用。</p>
<p id="p62392252"><a name="p62392252"></a><a name="p62392252"></a>类型：String</p>
<p id="p6679135313114"><a name="p6679135313114"></a><a name="p6679135313114"></a>支持两种格式的描述方式：</p>
<p id="p1611719113354"><a name="p1611719113354"></a><a name="p1611719113354"></a>1. regionID:domainID(租户ID):key/key_id</p>
<p id="p17964154220128"><a name="p17964154220128"></a><a name="p17964154220128"></a>或者</p>
<p id="p090816596123"><a name="p090816596123"></a><a name="p090816596123"></a>2.key_id</p>
<p id="p558627121315"><a name="p558627121315"></a><a name="p558627121315"></a>其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是从<span>数据加密服务</span>创建的密钥ID。</p>
<p id="p17830152818144"><a name="p17830152818144"></a><a name="p17830152818144"></a>示例：</p>
<p id="p4765922"><a name="p4765922"></a><a name="p4765922"></a>1. x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0  或者</p>
<p id="p9607740151414"><a name="p9607740151414"></a><a name="p9607740151414"></a>2. x-obs-server-side-encryption-kms-key-id：4f1cd4de-ab64-4807-920a-47fc42e7f0d0</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p51251487"><a name="p51251487"></a><a name="p51251487"></a>否</p>
</td>
</tr>
<tr id="row58610204"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p49806107"><a name="p49806107"></a><a name="p49806107"></a>x-obs-server-side-encryption-customer-algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p7762862"><a name="p7762862"></a><a name="p7762862"></a>SSE-C方式下使用该头域，该头域表示加密使用的算法。</p>
<p id="p2756899"><a name="p2756899"></a><a name="p2756899"></a>类型：String</p>
<p id="p24812094"><a name="p24812094"></a><a name="p24812094"></a>示例：x-obs-server-side-encryption-customer-algorithm：AES256</p>
<p id="p21982256"><a name="p21982256"></a><a name="p21982256"></a>约束：需要和x-obs-server-side-encryption-customer-key， x-obs-server-side-encryption-customer-key-MD5一起使用。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p35732293"><a name="p35732293"></a><a name="p35732293"></a>否。当使用SSE-C方式时，必选。</p>
</td>
</tr>
<tr id="row53155187"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p10602856"><a name="p10602856"></a><a name="p10602856"></a>x-obs-server-side-encryption-customer-key</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p53524985"><a name="p53524985"></a><a name="p53524985"></a>SSE-C方式下使用该头域，该头域表示加密使用的密钥。该密钥用于加密对象。</p>
<p id="p11962824"><a name="p11962824"></a><a name="p11962824"></a>类型：String</p>
<p id="p40556560"><a name="p40556560"></a><a name="p40556560"></a>示例：x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=</p>
<p id="p29464720"><a name="p29464720"></a><a name="p29464720"></a>约束：该头域由256-bit的密钥经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key-MD5一起使用。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p37832104"><a name="p37832104"></a><a name="p37832104"></a>否。当使用SSE-C方式时，必选。</p>
</td>
</tr>
<tr id="row4944617"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p64969725"><a name="p64969725"></a><a name="p64969725"></a>x-obs-server-side-encryption-customer-key-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p28056373"><a name="p28056373"></a><a name="p28056373"></a>SSE-C方式下使用该头域，该头域表示加密使用的密钥的MD5值。MD5值用于验证密钥传输过程中没有出错。</p>
<p id="p51180770"><a name="p51180770"></a><a name="p51180770"></a>类型：String</p>
<p id="p57973754"><a name="p57973754"></a><a name="p57973754"></a>示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==</p>
<p id="p52001740"><a name="p52001740"></a><a name="p52001740"></a>约束: 该头域由密钥的128-bit MD5值经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key一起使用。</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p51391439"><a name="p51391439"></a><a name="p51391439"></a>否。当使用SSE-C方式时，必选。</p>
</td>
</tr>
<tr id="row7583033195917"><td class="cellrowborder" valign="top" width="29.592959295929592%" headers="mcps1.2.4.1.1 "><p id="p1514215711573"><a name="p1514215711573"></a><a name="p1514215711573"></a>x-obs-expires</p>
</td>
<td class="cellrowborder" valign="top" width="61.22612261226122%" headers="mcps1.2.4.1.2 "><p id="p6876185903819"><a name="p6876185903819"></a><a name="p6876185903819"></a>表示对象的过期时间，单位是天。过期之后对象会被自动删除。（从对象最后修改时间开始计算）</p>
<p id="p133831235577"><a name="p133831235577"></a><a name="p133831235577"></a>类型：Integer</p>
<p id="p638302312574"><a name="p638302312574"></a><a name="p638302312574"></a>示例：x-obs-expires:3</p>
</td>
<td class="cellrowborder" valign="top" width="9.180918091809183%" headers="mcps1.2.4.1.3 "><p id="p1014357105719"><a name="p1014357105719"></a><a name="p1014357105719"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 响应消息样式<a name="section9552642"></a>

```
HTTP/1.1 status_code
Content-Type: application/xml 
Location: location
Date: date
ETag: etag
```

## 响应消息头<a name="section18864917"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

除公共响应消息头之外，还可能使用如[表3](#table35215532173747)中的消息头。

**表 3**  附加响应消息头

<a name="table35215532173747"></a>
<table><thead align="left"><tr id="row9381568"><th class="cellrowborder" valign="top" width="40%" id="mcps1.2.3.1.1"><p id="p21709532"><a name="p21709532"></a><a name="p21709532"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.3.1.2"><p id="p13641628"><a name="p13641628"></a><a name="p13641628"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row31230056"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p46606633"><a name="p46606633"></a><a name="p46606633"></a>x-obs-version-id</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p17040967"><a name="p17040967"></a><a name="p17040967"></a>对象的版本号。如果桶的多版本状态为开启，则会返回对象的版本号。如果桶的多版本状态为暂停，则会返回<strong id="b19150980"><a name="b19150980"></a><a name="b19150980"></a>null</strong>。</p>
<p id="p38141097"><a name="p38141097"></a><a name="p38141097"></a>类型：String</p>
</td>
</tr>
<tr id="row7725560"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p21790587"><a name="p21790587"></a><a name="p21790587"></a>Access-Control-Allow-Origin</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p20207160"><a name="p20207160"></a><a name="p20207160"></a>当桶设置了CORS配置，如果请求的Origin满足服务端的CORS配置，则在响应中包含这个Origin。</p>
<p id="p47646715"><a name="p47646715"></a><a name="p47646715"></a>类型：String</p>
</td>
</tr>
<tr id="row26167253"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p39172730"><a name="p39172730"></a><a name="p39172730"></a>Access-Control-Allow-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p18874576"><a name="p18874576"></a><a name="p18874576"></a>当桶设置了CORS配置，如果请求的headers满足服务端的CORS配置，则在响应中包含这个headers。</p>
<p id="p35653461"><a name="p35653461"></a><a name="p35653461"></a>类型：String</p>
</td>
</tr>
<tr id="row52445694"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p20242861"><a name="p20242861"></a><a name="p20242861"></a>Access-Control-Max-Age</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p29059077"><a name="p29059077"></a><a name="p29059077"></a>当桶设置了CORS配置，服务端CORS配置中的MaxAgeSeconds。</p>
<p id="p60205103"><a name="p60205103"></a><a name="p60205103"></a>类型：Integer</p>
</td>
</tr>
<tr id="row4975021"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p323533"><a name="p323533"></a><a name="p323533"></a>Access-Control-Allow-Methods</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p26206222"><a name="p26206222"></a><a name="p26206222"></a>当桶设置了CORS配置，如果请求的Access-Control-Request-Method满足服务端的CORS配置，则在响应中包含这条rule中的Methods。</p>
<p id="p34529410"><a name="p34529410"></a><a name="p34529410"></a>类型：String</p>
<p id="p42329239"><a name="p42329239"></a><a name="p42329239"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
</td>
</tr>
<tr id="row45418839"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p55047328"><a name="p55047328"></a><a name="p55047328"></a>Access-Control-Expose-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p29648582"><a name="p29648582"></a><a name="p29648582"></a>当桶设置了CORS配置，服务端CORS配置中的ExposeHeader。</p>
<p id="p65510647"><a name="p65510647"></a><a name="p65510647"></a>类型：String</p>
</td>
</tr>
<tr id="row52724912"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p42859462"><a name="p42859462"></a><a name="p42859462"></a>x-obs-server-side-encryption</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p49064434"><a name="p49064434"></a><a name="p49064434"></a>如果服务端加密是SSE-KMS方式，响应包含该头域。</p>
<p id="p38926722"><a name="p38926722"></a><a name="p38926722"></a>类型：String</p>
<p id="p14796185"><a name="p14796185"></a><a name="p14796185"></a>示例：x-obs-server-side-encryption：kms</p>
</td>
</tr>
<tr id="row66056807"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p49001173"><a name="p49001173"></a><a name="p49001173"></a>x-obs-server-side-encryption-kms-key-id</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p9672051"><a name="p9672051"></a><a name="p9672051"></a>如果服务端加密是SSE-KMS方式，响应包含该头域，该头域表示主密钥。</p>
<p id="p10474191820349"><a name="p10474191820349"></a><a name="p10474191820349"></a>类型：String</p>
<p id="p11972162218372"><a name="p11972162218372"></a><a name="p11972162218372"></a>格式为： regionID:domainID(租户ID):key/key_id</p>
<p id="p204741187343"><a name="p204741187343"></a><a name="p204741187343"></a>其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是本次加密使用的密钥ID。</p>
<p id="p10474718183413"><a name="p10474718183413"></a><a name="p10474718183413"></a>示例： x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0</p>
</td>
</tr>
<tr id="row45238633"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p40450656"><a name="p40450656"></a><a name="p40450656"></a>x-obs-server-side-encryption-customer-algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p55277695"><a name="p55277695"></a><a name="p55277695"></a>如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的算法。</p>
<p id="p27737214"><a name="p27737214"></a><a name="p27737214"></a>类型：String</p>
<p id="p48308335"><a name="p48308335"></a><a name="p48308335"></a>示例：x-obs-server-side-encryption-customer-algorithm：AES256</p>
</td>
</tr>
<tr id="row32121837"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p51731993"><a name="p51731993"></a><a name="p51731993"></a>x-obs-server-side-encryption-customer-key-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p29541865"><a name="p29541865"></a><a name="p29541865"></a>如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的密钥的MD5值。</p>
<p id="p64550194"><a name="p64550194"></a><a name="p64550194"></a>类型：String</p>
<p id="p44080837"><a name="p44080837"></a><a name="p44080837"></a>示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==</p>
</td>
</tr>
</tbody>
</table>

## 响应消息元素<a name="section35566529"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section51663312"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例1<a name="section14482163815396"></a>

**普通POST上传**

```
POST / HTTP/1.1
Date: WED, 01 Jul 2015 04:15:23 GMT
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Content-Type: multipart/form-data; boundary=7db143f50da2
Content-Length: 2424
Origin: www.example.com
Access-Control-Request-Headers:acc_header_1

--7db143f50da2
Content-Disposition: form-data; name="key"

object01
--7db143f50da2
Content-Disposition: form-data; name="acl"

public-read
--7db143f50da2 
Content-Disposition: form-data; name="content-type"

text/plain
--7db143f50da2
Content-Disposition: form-data; name="expires"

WED, 01 Jul 2015 04:16:15 GMT
--7db143f50da2
Content-Disposition: form-data; name="AccessKeyId"

14RZT432N80TGDF2Y2G2
--7db143f50da2
Content-Disposition: form-data; name="policy"

ew0KICAiZXhaaXJhdGlvbiI6ICIyMDE1LTA3LTAxVDEyOjAwOjAwLjAwMFoiLA0KICAiY29uZGl0aW9ucyI6IFsNCiAgICB7ImJ1Y2tldCI6ICJleG1hcGxlYnVja2V0IiB9LA0KICAgIHsiYWNsIjogInB1YmxpYy1yZWFkIiB9LA0KICAgIHsiRXhaaXJlcyI6ICIxMDAwIiB9LA0KICAgIFsiZXEiLCAiJGtleSIsICJvYmplY3QwMSJdLA0KICAgIFsic3RhcnRzLXdpdGgiLCAiJENvbnRlbnQtVHlwZSIsICJ0ZXh0LyJdLA0KICBdDQp9DQo=
--7db143f50da2
Content-Disposition: form-data; name="signature"

Vk6rwO0Nq09BLhvNSIYwSJTRQ+k=
--7db143f50da2
Content-Disposition: form-data; name="file"; filename="C:\Testtools\UpLoadFiles\object\1024Bytes.txt"
Content-Type: text/plain

01234567890
--7db143f50da2
Content-Disposition: form-data; name="submit"

Upload
--7db143f50da2--
```

## 响应示例1<a name="section76081155815"></a>

桶配置cors后，响应会包含Access-Control-\*的信息。

```
HTTP/1.1 204 No Content
x-obs-request-id: 90E2BA00C26C00000133B442A90063FD
x-obs-id-2: OTBFMkJBMDBDMjZDMDAwMDAxMzNCNDQyQTkwMDYzRkRBQUFBQUFBQWJiYmJiYmJi
Access-Control-Allow-Origin: www.example.com
Access-Control-Allow-Methods: POST,GET,HEAD,PUT
Access-Control-Allow-Headers: acc_header_01
Access-Control-Max-Age: 100
Access-Control-Expose-Headers: exp_header_01
Content-Type: text/xml
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/object01
Date: WED, 01 Jul 2015 04:15:23 GMT
ETag: "ab7abb0da4bca5323ab6119bb5dcd296"
```

## 请求示例2<a name="section392181218378"></a>

**带x-obs-acl头域并指定存储类型，重定向头域，上传对象**

编码前，policy的内容为

```
{
    "expiration":"2018-07-17T04:54:35Z",
    "conditions":[
        {
            "content-type":"text/plain"
        },
        {
            "x-obs-storage-class":"WARM"
        },
        {
            "success_action_redirect":"http://www.example.com"
        },
        {
            "x-obs-acl":"public-read"
        },
        [
            "starts-with",
            "$bucket",
            ""
        ],
        [
            "starts-with",
            "$key",
            ""
        ]
    ]
}
```

请求示例：

```
POST / HTTP/1.1
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept-Encoding: identity
Content-Length: 947
Content-Type: multipart/form-data; boundary=9431149156168
User-Agent: OBS/Test

--9431149156168
Content-Disposition: form-data; name="x-obs-acl"

public-read
--9431149156168
Content-Disposition: form-data; name="AccessKeyId"

H4IPJX0TQTHTHEBQQCEC
--9431149156168
Content-Disposition: form-data; name="key"

my-obs-object-key-demo
--9431149156168
Content-Disposition: form-data; name="signature"

WNwv8P1ZiWdqPQqjXeLmAfzPDAI=
--9431149156168
Content-Disposition: form-data; name="policy"

eyJleHBpcmF0aW9uIjoiMjAxOC0wNy0xN1QwODozNDoyM1oiLCAiY29uZGl0aW9ucyI6W3siY29udGVudC10eXBlIjoidGV4dC9wbGFpbiJ9LHsieC1vYnMtYWNsIjoicHVibGljLXJlYWQifSxbInN0YXJ0cy13aXRoIiwgIiRidWNrZXQiLCAiIl0sWyJzdGFydHMtd2l0aCIsICIka2V5IiwgIiJdXX0=
--9431149156168
Content-Disposition: form-data; name="content-type"

text/plain
--9431149156168
Content-Disposition: form-data; name="file"; filename="myfile"
Content-Type: text/plain

c2c6cd0f-898e-11e8-aab6-e567c91fb541
52b8e8a0-8481-4696-96f3-910635215a78

--9431149156168--
```

## 响应示例2<a name="section1999141253715"></a>

```
HTTP/1.1 204 No Content
Server: OBS
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/my-obs-object-key-demo
ETag: "17a83fc8d431273405bd266114b7e034"
x-obs-request-id: 5DEB00000164A728A7C7F4E032214CFA
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSwj2PcBE0YcoLHUDO7GSj+rVByzjflA
Date: Tue, 17 Jul 2018 07:33:36 GMT
```

## 请求示例3<a name="section430011014337"></a>

**使用token进行鉴权**

```
POST / HTTP/1.1
Content-Type:multipart/form-data; boundary=9431149156168
Content-Length: 634
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
 
--9431149156168
Content-Disposition: form-data; name="key"
obj01
 
--9431149156168
Content-Disposition: form-data; name="token"
UDSIAMSTUBTEST002538:XsVcTzR2/A284oE4VH9qPndGcuE=:eyJjb25kaXRpb25zIjogW3siYnVja2V0IjogInRlc3QzMDAzMDU4NzE2NjI2ODkzNjcuMTIifSwgeyJDb250ZW50LVR5cGUiOiAiYXBwbGljYXRpb24veG1sIn0sIFsiZXEiLCAiJGtleSIsICJvYmoudHh0Il1dLCAiZXhwaXJhdGlvbiI6ICIyMDIyLTA5LTA5VDEyOjA5OjI3WiJ9
 
--9431149156168
Content-Disposition: form-data; name="file"; filename="myfile"
Content-Type: text/plain
01234567890
 
--9431149156168--
Content-Disposition: form-data; name="submit"
Upload to OBS
```

## 响应示例3<a name="section47211218103213"></a>

**使用token进行鉴权，响应消息。**

```
HTTP/1.1 204 No Content
Server: OBS
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/my-obs-object-key-demo
ETag: "7eda50a430fed940023acb9c4c6a2fff"
x-obs-request-id: 000001832010443D80F30B649B969C47
x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCTj0yO9KJd5In+i9pzTgCDVG9vMnk7O/
Date: Fri,09Sep 2022 02: 24:40 GMT
```

