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

|消息头名称|描述|是否必选|
|--|--|--|
|Content-MD5|按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串。也支持设置Content-SHA256头域，其值为消息体256-bit SHA256值经过base64编码后得到的字符串，Content-MD5和Content-SHA256二选一。类型：String示例：n58IG6hfM7vqI4K0vnWpog==|是|


## 请求消息元素<a name="section54295418"></a>

在此请求中，需要在请求的消息体中配置桶的CORS配置信息。配置信息以XML格式上传，具体的配置元素如[表2](#table35453405161544)描述。

**表 2**  CORS配置元素

|名称|描述|是否必选|
|--|--|--|
|CORSConfiguration|CORSRules的根节点，最大不超过64 KB。类型：Container父节点：无。|是|
|CORSRule|CORS规则，CORSConfiguration下可最多包含100个规则。类型：Container父节点：CORSConfiguration。|是|
|ID|一条Rule的标识，由不超过255个字符的字符串组成。类型：String父节点：CORSRule。|否|
|AllowedMethod|CORS规则允许的Method。类型：String有效值：GET、PUT、HEAD、POST 、DELETE父节点：CORSRule。|是|
|AllowedOrigin|CORS规则允许的Origin（表示域名的字符串，仅支持英文域名），通过正则表达式进行匹配，可以带一个匹配符“*”。每一个AllowedOrigin可以带最多一个“*”通配符。类型：String父节点：CORSRule。|是|
|AllowedHeader|配置CORS请求中允许携带的“Access-Control-Request-Headers”头域。如果一个请求带了“Access-Control-Request-Headers”头域，则只有匹配上AllowedHeader中的配置才认为是一个合法的CORS请求（通过正则表达式进行匹配）。每一个AllowedHeader可以带最多一个“*”通配符，不可出现空格。类型：String父节点：CORSRule。|否|
|MaxAgeSeconds|客户端可以缓存的CORS响应时间，以秒为单位。每个CORSRule可以包含至多一个MaxAgeSeconds，可以设置为负值。类型：Integer父节点：CORSRule。|否|
|ExposeHeader|CORS响应中带的附加头域，给客户端提供额外的信息，不可出现空格。类型：String父节点：CORSRule。|否|


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

## 请求示例：为桶配置两条CORS规则<a name="section1086510712157"></a>

```
PUT /?cors HTTP/1.1
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:iqSPeUBl66PwXDApxjRKk6hlcN4=
User-Agent: curl/7.29.0
Host: examplebucket.obs.region.myhuaweicloud.com
Date: WED, 01 Jul 2015 02:37:22 GMT
Content-Type: application/xml
Content-MD5: HwVUAzslyD0rroMp/eIdwQ==
 
<CORSConfiguration>
    <CORSRule>
        <AllowedOrigin>http://www.example.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedMethod>POST</AllowedMethod>
        <AllowedMethod>DELETE</AllowedMethod>
        <AllowedHeader>*</AllowedHeader>
    </CORSRule>
    <CORSRule>
        <AllowedOrigin>*</AllowedOrigin>
        <AllowedMethod>GET</AllowedMethod>
    </CORSRule>
</CORSConfiguration>
```

## 响应示例：为桶配置两条CORS规则<a name="section173758189154"></a>

```
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCTPXg+yj9IXC9r6mgmWgfSfqQGvHM3rS
x-obs-request-id: 0000018A3A14051AD2886D166EE13D98
Server: OBS
Content-Length: 0
Date: WED, 01 Jul 2015 02:37:22 GMT
```

