# 获取桶的CORS配置<a name="ZH-CN_TOPIC_0100846771"></a>

## 功能介绍<a name="section5584184924715"></a>

获取指定桶的CORS配置信息。

要正确执行此操作，需要确保执行者有GetBucketCORS权限。默认情况下只有桶的所有者可以执行此操作，也可以通过设置桶策略或用户策略授权给其他用户。

## 请求消息样式<a name="section34774393"></a>

```
GET /?cors HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization
```

## 请求消息参数<a name="section44534087"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section65262468"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section50491305"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section51768568"></a>

```
HTTP/1.1 status_code
Content-Type:  application/xml 
Date: date
Content-Length: length

<?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
<CORSConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/"> 
    <CORSRule> 
        ... 
    </CORSRule> 
</CORSConfiguration>
```

## 响应消息头<a name="section63263928"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section32504443"></a>

在此请求返回的响应消息体中包含的配置元素如下[表1](#table2259502317110)描述。

**表 1**  CORS配置元素

<a name="table2259502317110"></a>
<table><thead align="left"><tr id="row663422"><th class="cellrowborder" valign="top" width="28.28%" id="mcps1.2.3.1.1"><p id="p53737197"><a name="p53737197"></a><a name="p53737197"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="71.72%" id="mcps1.2.3.1.2"><p id="p57745689"><a name="p57745689"></a><a name="p57745689"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row46889193"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p39928261"><a name="p39928261"></a><a name="p39928261"></a>CORSConfiguration</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p12963734"><a name="p12963734"></a><a name="p12963734"></a>CORSRules的根节点，最大不超过64 KB。</p>
<p id="p49564750"><a name="p49564750"></a><a name="p49564750"></a>类型：容器。</p>
<p id="p43429572"><a name="p43429572"></a><a name="p43429572"></a>父节点：无。</p>
</td>
</tr>
<tr id="row55321833"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p51883501"><a name="p51883501"></a><a name="p51883501"></a>CORSRule</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p41814016"><a name="p41814016"></a><a name="p41814016"></a>CORS规则，CORSConfiguration下可最多包含100个规则。</p>
<p id="p40781832"><a name="p40781832"></a><a name="p40781832"></a>类型：容器。</p>
<p id="p31492173"><a name="p31492173"></a><a name="p31492173"></a>父节点：CORSConfiguration。</p>
</td>
</tr>
<tr id="row14994104"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p6562892"><a name="p6562892"></a><a name="p6562892"></a>ID</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p61832237"><a name="p61832237"></a><a name="p61832237"></a>一条Rule的标识，由不超过255个字符的字符串组成。</p>
<p id="p19619221"><a name="p19619221"></a><a name="p19619221"></a>类型：字符串。</p>
<p id="p42355266"><a name="p42355266"></a><a name="p42355266"></a>父节点：Rule。</p>
</td>
</tr>
<tr id="row45653075"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p6911634"><a name="p6911634"></a><a name="p6911634"></a>AllowedMethod</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p22971514"><a name="p22971514"></a><a name="p22971514"></a>CORS规则允许的Method。</p>
<p id="p5417036"><a name="p5417036"></a><a name="p5417036"></a>类型：字符串。</p>
<p id="p48753330"><a name="p48753330"></a><a name="p48753330"></a>有效值：GET、PUT、HEAD、POST 、DELETE</p>
<p id="p36126787"><a name="p36126787"></a><a name="p36126787"></a>父节点：Rule。</p>
</td>
</tr>
<tr id="row56705634"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p29753651"><a name="p29753651"></a><a name="p29753651"></a>AllowedOrigin</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p61235532"><a name="p61235532"></a><a name="p61235532"></a>CORS规则允许的Origin（表示域名的字符串），可以带一个匹配符”*”。每一个AllowedOrigin可以带最多一个“*”通配符。</p>
<p id="p14248884"><a name="p14248884"></a><a name="p14248884"></a>类型：字符串。</p>
<p id="p61131094"><a name="p61131094"></a><a name="p61131094"></a>父节点：Rule。</p>
</td>
</tr>
<tr id="row13308941"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p4282435"><a name="p4282435"></a><a name="p4282435"></a>AllowedHeader</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p11332925"><a name="p11332925"></a><a name="p11332925"></a>配置CORS请求中允许携带的“Access-Control-Request-Headers”头域。如果一个请求带了“Access-Control-Request-Headers”头域，则只有匹配上AllowedHeader中的配置才认为是一个合法的CORS请求。每一个AllowedHeader可以带最多一个“*”通配符，不可出现空格。</p>
<p id="p34887463"><a name="p34887463"></a><a name="p34887463"></a>类型：字符串。</p>
<p id="p45551715"><a name="p45551715"></a><a name="p45551715"></a>父节点：Rule。</p>
</td>
</tr>
<tr id="row7312259"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p55422103"><a name="p55422103"></a><a name="p55422103"></a>MaxAgeSeconds</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p60005388"><a name="p60005388"></a><a name="p60005388"></a>客户端可以缓存的CORS响应时间，以秒为单位。</p>
<p id="p3177586"><a name="p3177586"></a><a name="p3177586"></a>每个CORSRule可以包含至多一个MaxAgeSeconds，可以设置为负值。</p>
<p id="p28598282"><a name="p28598282"></a><a name="p28598282"></a>类型：整数。</p>
<p id="p56057947"><a name="p56057947"></a><a name="p56057947"></a>父节点：Rule。</p>
</td>
</tr>
<tr id="row34759480"><td class="cellrowborder" valign="top" width="28.28%" headers="mcps1.2.3.1.1 "><p id="p64054462"><a name="p64054462"></a><a name="p64054462"></a>ExposeHeader</p>
</td>
<td class="cellrowborder" valign="top" width="71.72%" headers="mcps1.2.3.1.2 "><p id="p21028933"><a name="p21028933"></a><a name="p21028933"></a>CORS响应中带的附加头域，给客户端提供额外的信息，不可出现空格。</p>
<p id="p55042672"><a name="p55042672"></a><a name="p55042672"></a>类型：字符串。</p>
<p id="p25622004"><a name="p25622004"></a><a name="p25622004"></a>父节点：Rule。</p>
</td>
</tr>
</tbody>
</table>

## 错误响应消息<a name="section24104539"></a>

此请求可能的特殊错误如下[表2](#table2262289217914)描述。

**表 2**  特殊错误

<a name="table2262289217914"></a>
<table><thead align="left"><tr id="row19846403"><th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.1"><p id="p64054849"><a name="p64054849"></a><a name="p64054849"></a>错误码</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.2"><p id="p21060291"><a name="p21060291"></a><a name="p21060291"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="p28162034"><a name="p28162034"></a><a name="p28162034"></a>HTTP状态码</p>
</th>
</tr>
</thead>
<tbody><tr id="row66532277"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p20405365"><a name="p20405365"></a><a name="p20405365"></a>NoSuchCORSConfiguration</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p42221849"><a name="p42221849"></a><a name="p42221849"></a>桶的CORS配置不存在</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p64526602"><a name="p64526602"></a><a name="p64526602"></a>404 Not Found</p>
</td>
</tr>
</tbody>
</table>

其余错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
GET /?cors HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 03:54:36 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:WJGghTrPQQXRuCx5go1fHyE+Wwg=
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF2600000164363593F10738B80CACBE
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSpngvwC5TskcLGh7Fz5KRmCFIayuY8p
Content-Type: application/xml
Date: WED, 01 Jul 2015 03:54:36 GMT
Content-Length: 825

<?xml version="1.0" encoding="utf-8"?> 
<CORSConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/"> 
  <CORSRule> 
    <ID>783fc6652cf246c096ea836694f71855</ID>  
    <AllowedMethod>POST</AllowedMethod>  
    <AllowedMethod>GET</AllowedMethod>  
    <AllowedMethod>HEAD</AllowedMethod>  
    <AllowedMethod>PUT</AllowedMethod>  
    <AllowedMethod>DELETE</AllowedMethod>  
    <AllowedOrigin>obs.myhuaweicloud.com</AllowedOrigin>  
    <AllowedOrigin>obs.example.com</AllowedOrigin>  
    <AllowedOrigin>www.example.com</AllowedOrigin>  
    <AllowedHeader>AllowedHeader_1</AllowedHeader>  
    <AllowedHeader>AllowedHeader_2</AllowedHeader>  
    <MaxAgeSeconds>100</MaxAgeSeconds>  
    <ExposeHeader>ExposeHeader_1</ExposeHeader>  
    <ExposeHeader>ExposeHeader_2</ExposeHeader> 
  </CORSRule>
</CORSConfiguration>
```

