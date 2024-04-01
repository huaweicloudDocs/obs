# 获取桶的CORS配置<a name="obs_04_0075"></a>

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

|名称|描述|
|--|--|
|CORSConfiguration|CORSRules的根节点，最大不超过64 KB。类型：Container父节点：无。|
|CORSRule|CORS规则，CORSConfiguration下可最多包含100个规则。类型：Container父节点：CORSConfiguration。|
|ID|一条Rule的标识，由不超过255个字符的字符串组成。类型：String父节点：CORSRule。|
|AllowedMethod|CORS规则允许的Method。类型：String有效值：GET、PUT、HEAD、POST 、DELETE父节点：CORSRule。|
|AllowedOrigin|CORS规则允许的Origin（表示域名的字符串），可以带一个匹配符”*”。每一个AllowedOrigin可以带最多一个“*”通配符。类型：String父节点：CORSRule。|
|AllowedHeader|配置CORS请求中允许携带的“Access-Control-Request-Headers”头域。如果一个请求带了“Access-Control-Request-Headers”头域，则只有匹配上AllowedHeader中的配置才认为是一个合法的CORS请求。每一个AllowedHeader可以带最多一个“*”通配符，不可出现空格。类型：String父节点：CORSRule。|
|MaxAgeSeconds|客户端可以缓存的CORS响应时间，以秒为单位。每个CORSRule可以包含至多一个MaxAgeSeconds，可以设置为负值。类型：Integer父节点：CORSRule。|
|ExposeHeader|CORS响应中带的附加头域，给客户端提供额外的信息，不可出现空格。类型：String父节点：CORSRule。|


## 错误响应消息<a name="section24104539"></a>

此请求可能的特殊错误如下[表2](#table2262289217914)描述。

**表 2**  特殊错误

|错误码|描述|HTTP状态码|
|--|--|--|
|NoSuchCORSConfiguration|桶的CORS配置不存在|404 Not Found|


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
    <AllowedOrigin>obs.cn-north-4.myhuaweicloud.com</AllowedOrigin>  
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

