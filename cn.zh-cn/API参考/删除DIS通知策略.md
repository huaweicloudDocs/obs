# 删除DIS通知策略<a name="obs_04_0141"></a>

## 功能介绍<a name="section19372229152946"></a>

本接口用于删除指定桶中配置的全部DIS通知策略。删除成功，status code返回值为204。

## 请求消息样式<a name="section51167945152946"></a>

```
DELETE /?disPolicy HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Authorization: authorization
Date: date
```

## 请求消息参数<a name="section11252648"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section16227023104816"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section23158684"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section920694152946"></a>

```
HTTP/1.1 status_code
Server: OBS
Date: date
```

## 响应消息头<a name="section8877856"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section12791844"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section48017739"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
DELETE /?disPolicy HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:sc2PM13Wlfcoc/YZLK0MwsI2Zpo=
Date: Tue, 21 Jul 2020 17:28:46 GMT
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 204 No Content
Server: OBS
Date: Tue, 07 Jul 2020 07:38:30 GMT
```

