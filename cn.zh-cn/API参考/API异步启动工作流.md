# API异步启动工作流<a name="obs_04_0127"></a>

## 功能介绍<a name="section583694617498"></a>

本接口用于API方式异步启动已有工作流，产生工作流实例。

## 请求消息样式<a name="section88881434644"></a>

```
POST /v2/workflows/{graph_name} HTTP/1.1
Host: obs.cn-north-4.myhuaweicloud.com 
Authorization: authorization
Content-Type: application/json
Content-Length: length
Date: date

json body
```

## 请求消息参数<a name="section05361254193011"></a>

**表 1**  请求消息参数

|名称|是否必选|参数类型|说明|约束|
|--|--|--|--|--|
|graph_name|是|String|工作流名称。|名称必须以字母或数字开头，只能由字母、数字、下划线和中划线组成，长度小于等于64个字符。|


## 请求消息头<a name="section16227023104816"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section8568135410306"></a>

**表 2**  参数说明

|名称|是否必选|参数类型|说明|约束|
|--|--|--|--|--|
|bucket|是|String|桶名。|-|
|object|是|String|对象名。|-|
|inputs|否|Json|工作流中可修改参数列表。|Map中的key必须是工作流中的parameter中的名字。|


## 响应消息样式<a name="section122865113138"></a>

```
HTTP/1.1 status_code 
Date: date 
Content-Length: length 
X-Request-ID: obs request id

json body
```

## 响应消息头<a name="section19656537138"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section28651738111419"></a>

**表 3**  响应元素

|名称|参数类型|说明|
|--|--|--|
|execution_urn|String|运行实例的URN。|
|started_at|String|运行实例启动时间。|
|execution_name|String|运行实例的名字。|


## 错误响应消息<a name="section53511050131419"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section20731125951417"></a>

```
POST /v2/workflows/{graph_name} HTTP/1.1
Host: obs.cn-north-4.myhuaweicloud.com 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:sc2PM13Wlfcoc/YZLK0MwsI2Zpo=
Content-Type: application/json
Content-Length: 100
Date: Thu, 27 Aug 2020 12:38:10 GMT

{
    "bucket": "demo-bucket",
    "object": "/mpc/demo.mp4",
    "inputs": {
        "<parameter-name>": <parameter-value>
    }
}
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK 
Date: Thu, 27 Aug 2020 12:38:10 GMT 
Content-Length: 100 
X-Request-ID: 000001742FE8FB3CCA20173B00807C43

{
    "execution_urn": "urn:fgs:<region_id>:<project_id>:execution:<graph_name>:<execution_name>:<domain_id>",
    "execution_name": "<execution_name>",
    "started_at": "2020-04-23T13:37:43.847Z"
}
```

