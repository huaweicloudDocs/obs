# OPTIONS对象<a name="obs_04_0078"></a>

## 功能介绍<a name="section5584184924715"></a>

请参见章节  [OPTIONS桶](OPTIONS桶.md)。

## 与OPTIONS桶的区别<a name="section9125142514612"></a>

OPTIONS对象需在URL中指定对象名；OPTIONS桶提交的URL为桶域名，无需指定对象名。两者的请求行分别为：

```
OPTIONS /object HTTP/1.1
```

```
OPTIONS / HTTP/1.1
```

## 请求消息样式<a name="section20503664"></a>

```
OPTIONS /object HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
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

|消息头名称|描述|是否必选|
|--|--|--|
|Origin|预请求指定的跨域请求Origin（通常为域名）。类型：String|是|
|Access-Control-Request-Method|实际请求可以带的HTTP方法，可以带多个方法头域。类型：String有效值：GET、PUT、HEAD、POST 、DELETE|是|
|Access-Control-Request-Headers|实际请求可以带的HTTP头域，可以带多个头域。类型：String|否|


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

|消息头名称|描述|
|--|--|
|Access-Control-Allow-Origin|如果请求的Origin满足服务端的CORS配置，则在响应中包含这个Origin。类型：String|
|Access-Control-Allow-Headers|如果请求的headers满足服务端的CORS配置，则在响应中包含这个headers。类型：String|
|Access-Control-Max-Age|服务端CORS配置中的MaxAgeSeconds。类型：Integer|
|Access-Control-Allow-Methods|如果请求的Access-Control-Request-Method满足服务端的CORS配置，则在响应中包含这条rule中的Methods。类型：String有效值：GET、PUT、HEAD、POST 、DELETE|
|Access-Control-Expose-Headers|服务端CORS配置中的ExposeHeader。类型：String|


## 响应消息元素<a name="section21752117"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section61551329"></a>

此请求可能的特殊错误如下[表3](#table38908138205823)描述。

**表 3**  特殊错误

|错误码|描述|HTTP状态码|
|--|--|--|
|Bad Request|Invalid Access-Control-Request-Method: null桶配置了CORS，OPTIONS桶时，没有加入method头域。|400 BadRequest|
|Bad Request|Insufficient information. Origin request header needed.桶配置了CORS，OPTIONS桶时，没有加入origin头域。|400 BadRequest|
|AccessForbidden|CORSResponse: This CORS request is not allowed. This is usually because the evalution of Origin, request method / Access-Control-Request-Method or Access-Control-Requet-Headers are not whitelisted by the resource's CORS spec.桶配置了CORS，OPTIONS桶时，Origin、method、Headers与任一rule匹配不上。|403 Forbidden|


其余错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
OPTIONS /object_1 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
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

