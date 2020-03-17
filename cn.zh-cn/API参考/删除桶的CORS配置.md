# 删除桶的CORS配置<a name="obs_04_0076"></a>

## 功能介绍<a name="section5584184924715"></a>

删除指定桶的CORS配置信息。删除后桶以及桶中的对象将不能再被其他网址发送的请求访问。

要正确执行此操作，需要确保执行者有PutBucketCORS权限\(在桶策略中配置删除桶CORS权限时和设置桶CORS使用同一个Action\)。

## 请求消息样式<a name="section47741860"></a>

```
DELETE /?cors HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization
```

## 请求消息参数<a name="section27023556"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section41885417"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section41424434"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section37275594"></a>

```
HTTP/1.1 status_code
Date: date
Content-Type:  application/xml 
Content-Length: length
```

## 响应消息头<a name="section67044897"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section66533169"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section61927609"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
DELETE /?cors HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 03:56:41 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:mKUs/uIPb8BP0ZhvMd4wEy+EbiI=
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 204 No Content
Server: OBS
x-obs-request-id: BF26000001643639F290185BB27F793A
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSLWMRFJfckapW+ktT/+1AnAz7XlNU0b
Date: WED, 01 Jul 2015 03:56:41 GMT
```

