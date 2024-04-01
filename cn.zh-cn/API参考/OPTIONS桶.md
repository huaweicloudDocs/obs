# OPTIONS桶<a name="obs_04_0077"></a>

## 功能介绍<a name="section5584184924715"></a>

OPTIONS，称为预请求，是客户端发送给服务端的一种请求，通常被用于检测客户端是否具有对服务端进行操作的权限。只有当预请求成功返回，客户端才开始执行后续的请求。

OBS允许在桶内保存静态的网页资源，在正确的使用下，OBS的桶可以成为网站资源。在这种使用场景下，OBS中的桶作为服务端，需要处理客户端发送的OPTIONS预请求。

要处理OPTIONS，OBS的桶必须已经配置CORS，关于CORS的使用说明，请参见章节  [设置桶的CORS配置](设置桶的CORS配置.md)。

## 与OPTIONS对象的区别<a name="section9125142514612"></a>

OPTIONS对象需在URL中指定对象名；OPTIONS桶提交的URL为桶域名，无需指定对象名。两者的请求行分别为：

```
OPTIONS /object HTTP/1.1
```

```
OPTIONS / HTTP/1.1
```

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

|消息头名称|描述|是否必选|
|--|--|--|
|Origin|预请求指定的跨域请求Origin（通常为域名）。类型：String|是|
|Access-Control-Request-Method|实际请求可以带的HTTP方法，可以带多个方法头域。类型：String有效值：GET、PUT、HEAD、POST 、DELETE|是|
|Access-Control-Request-Headers|实际请求可以带的HTTP头域，可以带多个头域。类型：String|否|


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

|消息头名称|描述|
|--|--|
|Access-Control-Allow-Origin|如果请求的Origin满足服务端的CORS配置，则在响应中包含这个Origin。类型：String|
|Access-Control-Allow-Headers|如果请求的headers满足服务端的CORS配置，则在响应中包含这个headers。类型：String|
|Access-Control-Max-Age|服务端CORS配置中的MaxAgeSeconds。类型：Integer|
|Access-Control-Allow-Methods|如果请求的Access-Control-Request-Method满足服务端的CORS配置，则在响应中包含这条rule中的Methods。类型：String有效值：GET、PUT、HEAD、POST 、DELETE|
|Access-Control-Expose-Headers|服务端CORS配置中的ExposeHeader。类型：String|


## 响应消息元素<a name="section5256624"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section47309617"></a>

此请求可能的特殊错误如下[表3](#table1322139420210)描述。

**表 3**  特殊错误

|错误码|描述|HTTP状态码|
|--|--|--|
|Bad Request|Invalid Access-Control-Request-Method: null桶配置了CORS，OPTIONS桶时，没有加入method头域。|400 BadRequest|
|Bad Request|Insufficient information. Origin request header needed.桶配置了CORS，OPTIONS桶时，没有加入origin头域。|400 BadRequest|
|AccessForbidden|CORSResponse: This CORS request is not allowed. This is usually because the evalution of Origin, request method / Access-Control-Request-Method or Access-Control-Requet-Headers are not whitelisted by the resource's CORS spec.桶配置了CORS，OPTIONS桶时，Origin、method、Headers与任一rule匹配不上。|403 Forbidden|


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

