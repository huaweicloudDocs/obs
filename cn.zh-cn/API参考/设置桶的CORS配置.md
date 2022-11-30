# 设置桶的CORS配置<a name="obs_04_0074"></a>

## 功能介绍<a name="section5584184924715"></a>

CORS（Cross Origin Resource Sharing），即跨域资源共享，是W3C标准化组织提出的一种规范机制，允许客户端的跨域请求的配置。在通常的网页请求中，由于安全策略SOP（Same Origin Policy）的存在，一个网站的脚本和内容是不能与另一个网站的脚本和内容发生交互的。

OBS允许在桶内保存静态的网页资源，在正确的使用下，OBS的桶可以成为网站资源（请参见[设置桶的网站配置](设置桶的网站配置.md)）。只有进行了适当的CORS配置，OBS中的网站才能响应另一个网站的跨域请求。

典型的应用场景如下：

-   你可以使用CORS支持，使用JavaScript和HTML 5来构建Web应用，直接访问OBS中的资源，而不再需要代理服务器做中转。
-   可以使用HTML 5中的拖拽功能，直接向OBS上传文件，展示上传进度，或是直接从Web应用中更新内容。
-   托管在不同域中的外部网页、样式表和HTML 5应用，现在可以引用存储在OBS中的Web字体或图片，让这些资源能被多个网站共享。

要正确执行此操作，需要确保执行者有PutBucketCORS权限。默认情况下只有桶的所有者可以执行此操作，也可以通过设置桶策略或用户策略授权给其他用户。

## 请求消息样式<a name="section29072136"></a>

```
PUT /?cors HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Content-Length: length
Date: date
Authorization: authorization
Content-MD5: MD5
<?xml version="1.0" encoding="UTF-8"?> 
<CORSConfiguration> 
    <CORSRule> 
        <ID>id</ID> 
        <AllowedMethod>method</AllowedMethod> 
        <AllowedOrigin>origin</AllowedOrigin> 
        <AllowedHeader>header</AllowedHeader> 
        <MaxAgeSeconds>seconds</MaxAgeSeconds> 
        <ExposeHeader>header</ExposeHeader> 
    </CORSRule> 
</CORSConfiguration>
```

## 请求消息参数<a name="section60322637"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section6032824"></a>

该请求使用公共消息头外加CORS请求消息头，具体参见[表3](构造请求.md#table25197309)和[表1](#table15021581161521)。

**表 1**  CORS请求消息头

<a name="table15021581161521"></a>
<table><thead align="left"><tr id="row20749318"><th class="cellrowborder" valign="top" width="19.388061193880613%" id="mcps1.2.4.1.1"><p id="p2973159"><a name="p2973159"></a><a name="p2973159"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="63.26367363263674%" id="mcps1.2.4.1.2"><p id="p39499321"><a name="p39499321"></a><a name="p39499321"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="17.348265173482652%" id="mcps1.2.4.1.3"><p id="p45328419"><a name="p45328419"></a><a name="p45328419"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row131151538153117"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p5739124015311"><a name="p5739124015311"></a><a name="p5739124015311"></a>Content-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p99864193216"><a name="p99864193216"></a><a name="p99864193216"></a>按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串。也支持设置Content-SHA256头域，其值为消息体256-bit SHA256值经过base64编码后得到的字符串，Content-MD5和Content-SHA256二选一。</p>
<p id="p1981043326"><a name="p1981043326"></a><a name="p1981043326"></a>类型：String</p>
<p id="p79817417329"><a name="p79817417329"></a><a name="p79817417329"></a>示例：n58IG6hfM7vqI4K0vnWpog==</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p14739124003114"><a name="p14739124003114"></a><a name="p14739124003114"></a>是</p>
</td>
</tr>
</tbody>
</table>

## 请求消息元素<a name="section54295418"></a>

在此请求中，需要在请求的消息体中配置桶的CORS配置信息。配置信息以XML格式上传，具体的配置元素如[表2](#table35453405161544)描述。

**表 2**  CORS配置元素

<a name="table35453405161544"></a>
<table><thead align="left"><tr id="row7895657"><th class="cellrowborder" valign="top" width="19.388061193880613%" id="mcps1.2.4.1.1"><p id="p35568496"><a name="p35568496"></a><a name="p35568496"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="63.26367363263674%" id="mcps1.2.4.1.2"><p id="p62475956"><a name="p62475956"></a><a name="p62475956"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="17.348265173482652%" id="mcps1.2.4.1.3"><p id="p27387676"><a name="p27387676"></a><a name="p27387676"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row3809297"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p40117626"><a name="p40117626"></a><a name="p40117626"></a>CORSConfiguration</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p28302272"><a name="p28302272"></a><a name="p28302272"></a>CORSRules的根节点，最大不超过64 KB。</p>
<p id="p53393857"><a name="p53393857"></a><a name="p53393857"></a>类型：Container</p>
<p id="p10782666"><a name="p10782666"></a><a name="p10782666"></a>父节点：无。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p980736"><a name="p980736"></a><a name="p980736"></a>是</p>
</td>
</tr>
<tr id="row8826632"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p43868588"><a name="p43868588"></a><a name="p43868588"></a>CORSRule</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p63694769"><a name="p63694769"></a><a name="p63694769"></a>CORS规则，CORSConfiguration下可最多包含100个规则。</p>
<p id="p36382015"><a name="p36382015"></a><a name="p36382015"></a>类型：Container</p>
<p id="p59002687"><a name="p59002687"></a><a name="p59002687"></a>父节点：CORSConfiguration。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p14488317"><a name="p14488317"></a><a name="p14488317"></a>是</p>
</td>
</tr>
<tr id="row63285989"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p25891503"><a name="p25891503"></a><a name="p25891503"></a>ID</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p16836989"><a name="p16836989"></a><a name="p16836989"></a>一条Rule的标识，由不超过255个字符的字符串组成。</p>
<p id="p17315177"><a name="p17315177"></a><a name="p17315177"></a>类型：String</p>
<p id="p21618872"><a name="p21618872"></a><a name="p21618872"></a>父节点：CORSRule。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p6298183"><a name="p6298183"></a><a name="p6298183"></a>否</p>
</td>
</tr>
<tr id="row56683650"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p27972907"><a name="p27972907"></a><a name="p27972907"></a>AllowedMethod</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p51212956"><a name="p51212956"></a><a name="p51212956"></a>CORS规则允许的Method。</p>
<p id="p58263423"><a name="p58263423"></a><a name="p58263423"></a>类型：String</p>
<p id="p54608766"><a name="p54608766"></a><a name="p54608766"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
<p id="p21716848"><a name="p21716848"></a><a name="p21716848"></a>父节点：CORSRule。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p14234302"><a name="p14234302"></a><a name="p14234302"></a>是</p>
</td>
</tr>
<tr id="row60999859"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p42041559"><a name="p42041559"></a><a name="p42041559"></a>AllowedOrigin</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p49923082"><a name="p49923082"></a><a name="p49923082"></a>CORS规则允许的Origin（表示域名的字符串），可以带一个匹配符”*”。每一个AllowedOrigin可以带最多一个“*”通配符。</p>
<p id="p46654562"><a name="p46654562"></a><a name="p46654562"></a>类型：String</p>
<p id="p17237879"><a name="p17237879"></a><a name="p17237879"></a>父节点：CORSRule。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p54090948"><a name="p54090948"></a><a name="p54090948"></a>是</p>
</td>
</tr>
<tr id="row17056486"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p39398119"><a name="p39398119"></a><a name="p39398119"></a>AllowedHeader</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p37131036"><a name="p37131036"></a><a name="p37131036"></a>配置CORS请求中允许携带的“Access-Control-Request-Headers”头域。如果一个请求带了“Access-Control-Request-Headers”头域，则只有匹配上AllowedHeader中的配置才认为是一个合法的CORS请求。每一个AllowedHeader可以带最多一个“*”通配符，不可出现空格。</p>
<p id="p65743869"><a name="p65743869"></a><a name="p65743869"></a>类型：String</p>
<p id="p54823917"><a name="p54823917"></a><a name="p54823917"></a>父节点：CORSRule。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p11552324"><a name="p11552324"></a><a name="p11552324"></a>否</p>
</td>
</tr>
<tr id="row36862052"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p33036220"><a name="p33036220"></a><a name="p33036220"></a>MaxAgeSeconds</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p58688140"><a name="p58688140"></a><a name="p58688140"></a>客户端可以缓存的CORS响应时间，以秒为单位。</p>
<p id="p58431217"><a name="p58431217"></a><a name="p58431217"></a>每个CORSRule可以包含至多一个MaxAgeSeconds，可以设置为负值。</p>
<p id="p56118909"><a name="p56118909"></a><a name="p56118909"></a>类型：Integer</p>
<p id="p35308137"><a name="p35308137"></a><a name="p35308137"></a>父节点：CORSRule。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p41386862"><a name="p41386862"></a><a name="p41386862"></a>否</p>
</td>
</tr>
<tr id="row36937440"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p39142691"><a name="p39142691"></a><a name="p39142691"></a>ExposeHeader</p>
</td>
<td class="cellrowborder" valign="top" width="63.26367363263674%" headers="mcps1.2.4.1.2 "><p id="p16441382"><a name="p16441382"></a><a name="p16441382"></a>CORS响应中带的附加头域，给客户端提供额外的信息，不可出现空格。</p>
<p id="p13754711"><a name="p13754711"></a><a name="p13754711"></a>类型：String</p>
<p id="p56683537"><a name="p56683537"></a><a name="p56683537"></a>父节点：CORSRule。</p>
</td>
<td class="cellrowborder" valign="top" width="17.348265173482652%" headers="mcps1.2.4.1.3 "><p id="p27963789"><a name="p27963789"></a><a name="p27963789"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 响应消息样式<a name="section18896716"></a>

```
HTTP/1.1 status_code

Date: date
Content-Length: length
```

## 响应消息头<a name="section35852719"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section54239021"></a>

该请求的响应消息不带消息元素。

## 错误响应消息<a name="section18389141"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
PUT /?cors HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 03:51:52 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:lq7BGoqE9yyhdEwE6KojJ7ysVxU=
Content-MD5: NGLzvw81f/A2C9PiGO0aZQ==
Content-Length: 617

<?xml version="1.0" encoding="utf-8"?>
<CORSConfiguration> 
  <CORSRule> 
    <AllowedMethod>POST</AllowedMethod>  
    <AllowedMethod>GET</AllowedMethod>  
    <AllowedMethod>HEAD</AllowedMethod>  
    <AllowedMethod>PUT</AllowedMethod>  
    <AllowedMethod>DELETE</AllowedMethod>  
    <AllowedOrigin>www.example.com</AllowedOrigin>  
    <AllowedHeader>AllowedHeader_1</AllowedHeader>  
    <AllowedHeader>AllowedHeader_2</AllowedHeader>  
    <MaxAgeSeconds>100</MaxAgeSeconds>  
    <ExposeHeader>ExposeHeader_1</ExposeHeader>  
    <ExposeHeader>ExposeHeader_2</ExposeHeader> 
  </CORSRule>
</CORSConfiguration>
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 100 Continue
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF26000001643627112BD03512FC94A4
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSYi6wLC4bkrvuS9sqnlRjxK2a5Fe3ry
Date: WED, 01 Jul 2015 03:51:52 GMT
Content-Length: 0
```

