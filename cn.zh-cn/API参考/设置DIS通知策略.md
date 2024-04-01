# 设置DIS通知策略<a name="obs_04_0139"></a>

## 功能介绍<a name="section19372229152946"></a>

本接口用于为指定桶配置DIS通知策略。接口是幂等的，如果桶上已存在相同策略内容，则返回成功，status code返回值为200；否则status code返回值为201。

## 请求消息样式<a name="section51167945152946"></a>

```
PUT /?disPolicy HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Authorization: authorization
Content-Type: application/json
Content-Length: length
Date: date
Body:
{
    "rules": [{
        "id":"rule_id",
        "stream": "stream_name",
        "project": "project_id",
        "events": ["ObjectCreated:*", "ObjectRemoved:*"],
        "prefix": "",
        "suffix": "",
        "agency": "agency_name"
    }]
}
```

## 请求消息参数<a name="section1298623631616"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section16227023104816"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section23158684"></a>

**表 1**  请求消息元素

|名称|描述|是否必选|
|--|--|--|
|rules|策略规则数组。类型：Container取值范围：[1, 10]同一个桶下的不同策略前缀不能重复和起始包含，委托建议使用同一个。|是|


**表 2**  rules参数说明

|名称|描述|是否必选|
|--|--|--|
|id|规则ID。当前桶上配置的DIS策略规则的唯一标识。类型：String取值范围：[1, 256]，满足“^[a-zA-Z0-9_-]{1, 256}$”|是|
|stream|DIS服务通道名称。需要先在DIS服务创建此通道。类型：String|是|
|project|DIS服务通道所属的项目ID。类型：String|是|
|events|OBS事件列表。类型：String有效值：长度[0, 1023]，值允许为任意字符，支持如下事件类型：ObjectCreated:* （所有上传操作）ObjectCreated:Put （上传对象）ObjectCreated:Post （使用浏览器上传对象）ObjectCreated:Copy （拷贝对象）ObjectCreated:CompleteMultipartUpload （合并段）ObjectRemoved:* （所有删除操作）ObjectRemoved:Delete （指定对象版本号删除对象）ObjectRemoved:DeleteMarkerCreated （不指定对象版本号删除对象）|是|
|prefix|对象名前缀，用于指定的对象名关键字，根据定义的前缀，输入需要过滤的对象的关键字信息，字符越长匹配精度越高，最大可支持1024个字符，最小可为空。同时，prefix和suffix加起来长度最大为1024个字符。类型：String取值范围：[0, 1024]|否|
|suffix|对象名后缀。用于指定的对象名关键字，根据定义的后缀，输入需要过滤的对象的关键字信息，字符越长匹配精度越高，最大可支持1024个字符，最小可为空。同时，prefix和suffix加起来长度最大为1024个字符。类型：String取值范围：[0, 1024]|否|
|agency|IAM委托名，被委托方必须包含OBS服务，赋予的权限必须是DIS服务的DIS Administrator或DIS User。类型：String|是|


## 响应消息样式<a name="section920694152946"></a>

```
HTTP/1.1 status
Server: OBS
Date: date
Content-Length: length
```

## 响应消息头<a name="section8877856"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section12791844"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section48017739"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
PUT /?disPolicy HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:sc2PM13Wlfcoc/YZLK0MwsI2Zpo=
Content-Type: application/json
Content-Length: 1049
Date: Tue, 21 Jul 2020 15:38:30 GMT
{
    "rules": [{
        "id":"event-01",
        "stream": "stream_name",
        "project": "project_id",
        "events": ["ObjectCreated:*", "ObjectRemoved:*"],
        "prefix": "",
        "suffix": "",
        "agency": "dis_agency"
    }]
}
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 201 Created
Server: OBS
Date: Tue, 07 Jul 2020 07:29:13 GMT
Content-Length: 0
```

