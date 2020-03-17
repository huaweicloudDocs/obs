# OPTIONS桶<a name="obs_04_0077"></a>

## 功能介绍<a name="section5584184924715"></a>

OPTIONS，称为预请求，是客户端发送给服务端的一种请求，通常被用于检测客户端是否具有对服务端进行操作的权限。只有当预请求成功返回，客户端才开始执行后续的请求。

OBS允许在桶内保存静态的网页资源，在正确的使用下，OBS的桶可以成为网站资源。在这种使用场景下，OBS中的桶作为服务端，需要处理客户端发送的OPTIONS预请求。

要处理OPTIONS，OBS的桶必须已经配置CORS，关于CORS的使用说明，请参见章节  [设置桶的CORS配置](设置桶的CORS配置.md)。

## 请求消息样式<a name="section40480049"></a>

```
OPTIONS / HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization
Origin: origin
Access-Control-Request-Method: method
```

## 请求消息参数<a name="section28776129"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section57658576"></a>

该请求使用的消息头如下[表1](#table2585568620633)所示。

**表 1**  OPTIONS请求消息头

<a name="table2585568620633"></a>
<table><thead align="left"><tr id="row61203858"><th class="cellrowborder" valign="top" width="19.388061193880613%" id="mcps1.2.4.1.1"><p id="p58565490"><a name="p58565490"></a><a name="p58565490"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="63.26367363263674%" id="mcps1.2.4.1.2"><p id="p46184267"><a name="p46184267"></a><a name="p46184267"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="17.348265173482652%" id="mcps1.2.4.1.3"><p id="p49938116"><a name="p49938116"></a><a name="p49938116"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row18455557"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p18505143"><a name="p18505143"></a><a name="p18505143"></a>Origin</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p22521601"><a name="p22521601"></a><a name="p22521601"></a>预请求指定的跨域请求Origin（通常为域名）。</p>
<p id="p1367823"><a name="p1367823"></a><a name="p1367823"></a>类型：字符串</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p43684849"><a name="p43684849"></a><a name="p43684849"></a>是</p>
</td>
</tr>
<tr id="row57619328"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p36653955"><a name="p36653955"></a><a name="p36653955"></a>Access-Control-Request-Method</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p16180416"><a name="p16180416"></a><a name="p16180416"></a>实际请求可以带的HTTP方法，可以带多个方法头域。</p>
<p id="p11406019"><a name="p11406019"></a><a name="p11406019"></a>类型：字符串</p>
<p id="p35545309"><a name="p35545309"></a><a name="p35545309"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p60597762"><a name="p60597762"></a><a name="p60597762"></a>是</p>
</td>
</tr>
<tr id="row8508952"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p18136477"><a name="p18136477"></a><a name="p18136477"></a>Access-Control-Request-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p59768510"><a name="p59768510"></a><a name="p59768510"></a>实际请求可以带的HTTP头域，可以带多个头域。</p>
<p id="p1045685"><a name="p1045685"></a><a name="p1045685"></a>类型：字符串</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p17591693"><a name="p17591693"></a><a name="p17591693"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 请求消息元素<a name="section49165144"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section39833112"></a>

```
HTTP/1.1 status_code
Content-Type: application/xml 
Access-Control-Allow-Origin: origin
Access-Control-Allow-Methods: method
Access-Control-Allow-Header: header
Access-Control-Max-Age: time
Access-Control-Expose-Headers: header
Date: date
Content-Length: length
```

## 响应消息头<a name="section22953690"></a>

该响应使用的消息头如下[表2](#table40550587202855)所示。

**表 2**  CORS响应消息头

<a name="table40550587202855"></a>
<table><thead align="left"><tr id="row4273512"><th class="cellrowborder" valign="top" width="28.28%" id="mcps1.2.3.1.1"><p id="p10610183"><a name="p10610183"></a><a name="p10610183"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="71.72%" id="mcps1.2.3.1.2"><p id="p54118519"><a name="p54118519"></a><a name="p54118519"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row21523936"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p65717225"><a name="p65717225"></a><a name="p65717225"></a>Access-Control-Allow-Origin</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p21494970"><a name="p21494970"></a><a name="p21494970"></a>如果请求的Origin满足服务端的CORS配置，则在响应中包含这个Origin。</p>
<p id="p59237005"><a name="p59237005"></a><a name="p59237005"></a>类型：字符串</p>
</td>
</tr>
<tr id="row63371004"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p32777686"><a name="p32777686"></a><a name="p32777686"></a>Access-Control-Allow-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p37746929"><a name="p37746929"></a><a name="p37746929"></a>如果请求的headers满足服务端的CORS配置，则在响应中包含这个headers。</p>
<p id="p4178046"><a name="p4178046"></a><a name="p4178046"></a>类型：字符串</p>
</td>
</tr>
<tr id="row37602421"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p25897224"><a name="p25897224"></a><a name="p25897224"></a>Access-Control-Max-Age</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p17300437"><a name="p17300437"></a><a name="p17300437"></a>服务端CORS配置中的MaxAgeSeconds。</p>
<p id="p21486208"><a name="p21486208"></a><a name="p21486208"></a>类型：整数</p>
</td>
</tr>
<tr id="row59158146"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p27080503"><a name="p27080503"></a><a name="p27080503"></a>Access-Control-Allow-Methods</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p46037149"><a name="p46037149"></a><a name="p46037149"></a>如果请求的Access-Control-Request-Method满足服务端的CORS配置，则在响应中包含这条rule中的Methods。</p>
<p id="p11681162"><a name="p11681162"></a><a name="p11681162"></a>类型：字符串</p>
<p id="p38021595"><a name="p38021595"></a><a name="p38021595"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
</td>
</tr>
<tr id="row6650043"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p1782642"><a name="p1782642"></a><a name="p1782642"></a>Access-Control-Expose-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p10176276"><a name="p10176276"></a><a name="p10176276"></a>服务端CORS配置中的ExposeHeader。</p>
<p id="p24477626"><a name="p24477626"></a><a name="p24477626"></a>类型：字符串</p>
</td>
</tr>
</tbody>
</table>

## 响应消息元素<a name="section5256624"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section47309617"></a>

此请求可能的特殊错误如下[表3](#table1322139420210)描述。

**表 3**  特殊错误

<a name="table1322139420210"></a>
<table><thead align="left"><tr id="row42502533"><th class="cellrowborder" valign="top" width="26.529999999999998%" id="mcps1.2.4.1.1"><p id="p20153131"><a name="p20153131"></a><a name="p20153131"></a>错误码</p>
</th>
<th class="cellrowborder" valign="top" width="48.980000000000004%" id="mcps1.2.4.1.2"><p id="p21790951"><a name="p21790951"></a><a name="p21790951"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="24.490000000000002%" id="mcps1.2.4.1.3"><p id="p20236574"><a name="p20236574"></a><a name="p20236574"></a>HTTP状态码</p>
</th>
</tr>
</thead>
<tbody><tr id="row28549818"><td class="cellrowborder" valign="top" width="26.529999999999998%" headers="mcps1.2.4.1.1 "><p id="p30833955"><a name="p30833955"></a><a name="p30833955"></a>Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="48.980000000000004%" headers="mcps1.2.4.1.2 "><p id="p14522432"><a name="p14522432"></a><a name="p14522432"></a>Invalid Access-Control-Request-Method: null</p>
<p id="p63593030"><a name="p63593030"></a><a name="p63593030"></a>桶配置了CORS，OPTIONS桶时，没有加入method头域。</p>
</td>
<td class="cellrowborder" valign="top" width="24.490000000000002%" headers="mcps1.2.4.1.3 "><p id="p50761805"><a name="p50761805"></a><a name="p50761805"></a>400 BadRequest</p>
</td>
</tr>
<tr id="row54203064"><td class="cellrowborder" valign="top" width="26.529999999999998%" headers="mcps1.2.4.1.1 "><p id="p28372067"><a name="p28372067"></a><a name="p28372067"></a>Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="48.980000000000004%" headers="mcps1.2.4.1.2 "><p id="p16436066"><a name="p16436066"></a><a name="p16436066"></a>Insufficient information. Origin request header needed.</p>
<p id="p13706869"><a name="p13706869"></a><a name="p13706869"></a>桶配置了CORS，OPTIONS桶时，没有加入origin头域。</p>
</td>
<td class="cellrowborder" valign="top" width="24.490000000000002%" headers="mcps1.2.4.1.3 "><p id="p36514574"><a name="p36514574"></a><a name="p36514574"></a>400 BadRequest</p>
</td>
</tr>
<tr id="row60195710"><td class="cellrowborder" valign="top" width="26.529999999999998%" headers="mcps1.2.4.1.1 "><p id="p44014314"><a name="p44014314"></a><a name="p44014314"></a>AccessForbidden</p>
</td>
<td class="cellrowborder" valign="top" width="48.980000000000004%" headers="mcps1.2.4.1.2 "><p id="p8389707"><a name="p8389707"></a><a name="p8389707"></a>CORSResponse: This CORS request is not allowed. This is usually because the evalution of Origin, request method / Access-Control-Request-Method or Access-Control-Requet-Headers are not whitelisted by the resource's CORS spec.</p>
<p id="p8398507"><a name="p8398507"></a><a name="p8398507"></a>桶配置了CORS，OPTIONS桶时，Origin、method、Headers与任一rule匹配不上。</p>
</td>
<td class="cellrowborder" valign="top" width="24.490000000000002%" headers="mcps1.2.4.1.3 "><p id="p9190486"><a name="p9190486"></a><a name="p9190486"></a>403 Forbidden</p>
</td>
</tr>
</tbody>
</table>

其余错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
OPTIONS / HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:02:15 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:7RqP1vjemo6U+Adv9/Y6eGzWrzA=
Origin: www.example.com
Access-Control-Request-Method: PUT
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016436314E8FF936946DBC9C
Access-Control-Allow-Origin: www.example.com
Access-Control-Allow-Methods: POST,GET,HEAD,PUT,DELETE
Access-Control-Max-Age: 100
Access-Control-Expose-Headers: ExposeHeader_1,ExposeHeader_2
Access-Control-Allow-Credentials: true
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCTlYimJvOyJncCLNm5y/iz6MAGLNxTuS
Date: WED, 01 Jul 2015 04:02:15 GMT
Content-Length: 0
```

