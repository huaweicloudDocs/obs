# OPTIONS对象<a name="ZH-CN_TOPIC_0100846769"></a>

## 功能介绍<a name="section5584184924715"></a>

请参见章节  [OPTIONS桶](OPTIONS桶.md)。

## 请求消息样式<a name="section20503664"></a>

```
OPTIONS /object HTTP/1.1 
Host: bucketname.obs.cn-north-1.myhuaweicloud.com 
Date: date
Authorization: authorization
Origin: origin
Access-Control-Request-Method: method
```

## 请求消息参数<a name="section50315253"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section50184093"></a>

该请求使用的消息头如下[表1](#table39180475205737)所示。

**表 1**  OPTIONS请求消息头

<a name="table39180475205737"></a>
<table><thead align="left"><tr id="row43151909"><th class="cellrowborder" valign="top" width="19.388061193880613%" id="mcps1.2.4.1.1"><p id="p5643772"><a name="p5643772"></a><a name="p5643772"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="63.26367363263674%" id="mcps1.2.4.1.2"><p id="p54492350"><a name="p54492350"></a><a name="p54492350"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="17.348265173482652%" id="mcps1.2.4.1.3"><p id="p51804245"><a name="p51804245"></a><a name="p51804245"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row35394345"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p48369697"><a name="p48369697"></a><a name="p48369697"></a>Origin</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p25631398"><a name="p25631398"></a><a name="p25631398"></a>预请求指定的跨域请求Origin（通常为域名）。</p>
<p id="p29355992"><a name="p29355992"></a><a name="p29355992"></a>类型：字符串</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p29025179"><a name="p29025179"></a><a name="p29025179"></a>是</p>
</td>
</tr>
<tr id="row59900021"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p20063503"><a name="p20063503"></a><a name="p20063503"></a>Access-Control-Request-Method</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p14531029"><a name="p14531029"></a><a name="p14531029"></a>实际请求可以带的HTTP方法，可以带多个方法头域。</p>
<p id="p63670405"><a name="p63670405"></a><a name="p63670405"></a>类型：字符串</p>
<p id="p36162737"><a name="p36162737"></a><a name="p36162737"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p43500552"><a name="p43500552"></a><a name="p43500552"></a>是</p>
</td>
</tr>
<tr id="row55960654"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p36519148"><a name="p36519148"></a><a name="p36519148"></a>Access-Control-Request-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p5260986"><a name="p5260986"></a><a name="p5260986"></a>实际请求可以带的HTTP头域，可以带多个头域。</p>
<p id="p47348874"><a name="p47348874"></a><a name="p47348874"></a>类型：字符串</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p10053604"><a name="p10053604"></a><a name="p10053604"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 请求消息元素<a name="section49003659"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section38379751"></a>

```
HTTP/1.1 status_code
Content-Type: type
Access-Control-Allow-Origin: origin
Access-Control-Allow-Methods: method
Access-Control-Allow-Header: header
Access-Control-Max-Age: time
Access-Control-Expose-Headers: header
Date: date
Content-Length: length
```

## 响应消息头<a name="section9873442"></a>

该请求使用的消息头如下[表2](#table14690348205823)所示。

**表 2**  CORS请求消息头

<a name="table14690348205823"></a>
<table><thead align="left"><tr id="row37872586"><th class="cellrowborder" valign="top" width="28.28%" id="mcps1.2.3.1.1"><p id="p47780665"><a name="p47780665"></a><a name="p47780665"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="71.72%" id="mcps1.2.3.1.2"><p id="p45028689"><a name="p45028689"></a><a name="p45028689"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row23445177"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p20011161"><a name="p20011161"></a><a name="p20011161"></a>Access-Control-Allow-Origin</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p10291354"><a name="p10291354"></a><a name="p10291354"></a>如果请求的Origin满足服务端的CORS配置，则在响应中包含这个Origin。</p>
<p id="p25513326"><a name="p25513326"></a><a name="p25513326"></a>类型：字符串</p>
</td>
</tr>
<tr id="row28293347"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p10059805"><a name="p10059805"></a><a name="p10059805"></a>Access-Control-Allow-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p9537904"><a name="p9537904"></a><a name="p9537904"></a>如果请求的headers满足服务端的CORS配置，则在响应中包含这个headers。</p>
<p id="p18732274"><a name="p18732274"></a><a name="p18732274"></a>类型：字符串</p>
</td>
</tr>
<tr id="row34372739"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p32728446"><a name="p32728446"></a><a name="p32728446"></a>Access-Control-Max-Age</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p33758474"><a name="p33758474"></a><a name="p33758474"></a>服务端CORS配置中的MaxAgeSeconds。</p>
<p id="p35390814"><a name="p35390814"></a><a name="p35390814"></a>类型：整数</p>
</td>
</tr>
<tr id="row50081870"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p30099699"><a name="p30099699"></a><a name="p30099699"></a>Access-Control-Allow-Methods</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p22156577"><a name="p22156577"></a><a name="p22156577"></a>如果请求的Access-Control-Request-Method满足服务端的CORS配置，则在响应中包含这条rule中的Methods。</p>
<p id="p65191466"><a name="p65191466"></a><a name="p65191466"></a>类型：字符串</p>
<p id="p49852287"><a name="p49852287"></a><a name="p49852287"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
</td>
</tr>
<tr id="row46017399"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p36421857"><a name="p36421857"></a><a name="p36421857"></a>Access-Control-Expose-Headers</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p64489295"><a name="p64489295"></a><a name="p64489295"></a>服务端CORS配置中的ExposeHeader。</p>
<p id="p43532747"><a name="p43532747"></a><a name="p43532747"></a>类型：字符串</p>
</td>
</tr>
</tbody>
</table>

## 响应消息元素<a name="section21752117"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section61551329"></a>

此请求可能的特殊错误如下[表3](#table38908138205823)描述。

**表 3**  特殊错误

<a name="table38908138205823"></a>
<table><thead align="left"><tr id="row31266288"><th class="cellrowborder" valign="top" width="26.529999999999998%" id="mcps1.2.4.1.1"><p id="p49541410"><a name="p49541410"></a><a name="p49541410"></a>错误码</p>
</th>
<th class="cellrowborder" valign="top" width="48.980000000000004%" id="mcps1.2.4.1.2"><p id="p53431297"><a name="p53431297"></a><a name="p53431297"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="24.490000000000002%" id="mcps1.2.4.1.3"><p id="p32967796"><a name="p32967796"></a><a name="p32967796"></a>HTTP状态码</p>
</th>
</tr>
</thead>
<tbody><tr id="row53145828"><td class="cellrowborder" valign="top" width="26.529999999999998%" headers="mcps1.2.4.1.1 "><p id="p9844792"><a name="p9844792"></a><a name="p9844792"></a>Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="48.980000000000004%" headers="mcps1.2.4.1.2 "><p id="p59230681"><a name="p59230681"></a><a name="p59230681"></a>Invalid Access-Control-Request-Method: null</p>
<p id="p63314081"><a name="p63314081"></a><a name="p63314081"></a>桶配置了CORS，OPTIONS桶时，没有加入method头域。</p>
</td>
<td class="cellrowborder" valign="top" width="24.490000000000002%" headers="mcps1.2.4.1.3 "><p id="p28166943"><a name="p28166943"></a><a name="p28166943"></a>400 BadRequest</p>
</td>
</tr>
<tr id="row52175903"><td class="cellrowborder" valign="top" width="26.529999999999998%" headers="mcps1.2.4.1.1 "><p id="p65498646"><a name="p65498646"></a><a name="p65498646"></a>Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="48.980000000000004%" headers="mcps1.2.4.1.2 "><p id="p3790072"><a name="p3790072"></a><a name="p3790072"></a>Insufficient information. Origin request header needed.</p>
<p id="p34110654"><a name="p34110654"></a><a name="p34110654"></a>桶配置了CORS，OPTIONS桶时，没有加入origin头域。</p>
</td>
<td class="cellrowborder" valign="top" width="24.490000000000002%" headers="mcps1.2.4.1.3 "><p id="p11499566"><a name="p11499566"></a><a name="p11499566"></a>400 BadRequest</p>
</td>
</tr>
<tr id="row36387235"><td class="cellrowborder" valign="top" width="26.529999999999998%" headers="mcps1.2.4.1.1 "><p id="p61684923"><a name="p61684923"></a><a name="p61684923"></a>AccessForbidden</p>
</td>
<td class="cellrowborder" valign="top" width="48.980000000000004%" headers="mcps1.2.4.1.2 "><p id="p30422880"><a name="p30422880"></a><a name="p30422880"></a>CORSResponse: This CORS request is not allowed. This is usually because the evalution of Origin, request method / Access-Control-Request-Method or Access-Control-Requet-Headers are not whitelisted by the resource's CORS spec.</p>
<p id="p5370466"><a name="p5370466"></a><a name="p5370466"></a>桶配置了CORS，OPTIONS桶时，Origin、method、Headers与任一rule匹配不上。</p>
</td>
<td class="cellrowborder" valign="top" width="24.490000000000002%" headers="mcps1.2.4.1.3 "><p id="p32354629"><a name="p32354629"></a><a name="p32354629"></a>403 Forbidden</p>
</td>
</tr>
</tbody>
</table>

其余错误已经包含在[表1](错误码列表.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
OPTIONS /object_1 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:02:19 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:bQZG9c2aokAJsHOOkuVBK6cHZZQ=
Origin: www.example.com
Access-Control-Request-Method: PUT
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF26000001643632D12EFCE1C1294555
Access-Control-Allow-Origin: www.example.com
Access-Control-Allow-Methods: POST,GET,HEAD,PUT,DELETE
Access-Control-Max-Age: 100
Access-Control-Expose-Headers: ExposeHeader_1,ExposeHeader_2
Access-Control-Allow-Credentials: true
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCS+DXV4zZetbTqFehhEcuXywTa/mi3T3
Date: WED, 01 Jul 2015 04:02:19 GMT
Content-Length: 0
```

