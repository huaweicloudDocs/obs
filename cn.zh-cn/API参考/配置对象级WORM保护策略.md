# 配置对象级WORM保护策略<a name="obs_04_0166"></a>

## 功能介绍<a name="section1418853462"></a>

开启了WORM开关的桶，上传的对象支持配置或修改对象保护期限。

-   如果上传对象时没有配置保护期限或自动应用桶级默认保护策略，您可以通过该操作配置对象保护期限。
-   如果上传对象时配置了保护期限或自动应用了默认保护期限，允许用户通过该操作延长保护期限。
-   对象保护期限仅允许修改，不允许删除。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >用户需要拥有“PutObjectRetention”权限才能配置或修改对象保护期限。

## 多版本<a name="section166231716962"></a>

开启了WORM开关的桶默认开启了多版本，因此桶内对象在上传时会具备版本号。您在配置对象级WORM保护策略时可以指定版本号来为特定版本的对象配置，如果您不指定版本号，则改动只会对同名对象的最新版本生效。WORM功能不会对带唯一版本号的删除标记生效。

## 多段操作<a name="section212181410230"></a>

多段上传的对象在合并前不会自动应用桶级默认WORM策略，也无法通过在上传或合并时指定头域来配置对象级WORM保护策略，指定已上传的段作为此接口的目标对象也无法进行配置。如果您需要对多段对象进行保护，您可以在合并多段对象后通过此接口为其配置对象级WORM保护策略。

## 请求消息样式<a name="section1688810391961"></a>

```
PUT /ObjectName?retention HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization

<Retention>
    <Mode>String</Mode>
    <RetainUntilDate>Timestamp</RetainUntilDate>
</Retention>
```

## 请求消息参数<a name="section1056812491663"></a>

请求参数说明如[表1](#table44298471191845)所示。

**表 1**  请求消息参数

|**参数名称**|**描述**|**是否必选**|
|--|--|--|
|versionId|对象的版本号。标示更改指定版本的对象的对象级WORM策略。不携带则为最新版本。类型：String|否|


## 请求消息头<a name="section326625618613"></a>

该请求使用公共请求消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section2747181671"></a>

|**名字**|**描述**|**是否必选**|
|--|--|--|
|Retention|对象级WORM保护策略配置的容器类型：Container|是|
|Mode|对象的保护策略，当前仅支持合规模式"COMPLIANCE"类型：String示例：COMPLIANCE|是|
|RetainUntilDate|对象的保护期限，时间戳格式，精确到毫秒级，如2015年7月1日13点20分35秒对应的值为1435728035000。该字段必须晚于当前时间，且仅可延长不能缩短。类型：Long示例：1435728035000|是|


## 响应消息样式<a name="section4341481779"></a>

```
HTTP/1.1 status_code
Date: date
Content-Length: length
```

## 响应消息头<a name="section19822152117719"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section1461933014718"></a>

该请求的响应消息不带消息元素。

## 错误响应消息<a name="section4672343878"></a>

此请求可能的特殊错误如下[表2](#table13791928162213)描述。

**表 2** 

|错误码|描述|HTTP状态码|
|--|--|--|
|InvalidRequest|目标桶没有开启桶级WORM开关|400|
|InvalidRequest|保护期限设置错误|400|
|MalformedObjectLockError|策略配置格式错误|400|


其余错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section20891205319711"></a>

```
PUT /objectname?retention HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
Date: WED, 01 Jul 2015 02:25:05 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
Content-Type: application/xml
Content-Length: 157
<Retention>
    <Mode>COMPLIANCE</Mode>
    <RetainUntilDate>1435728035000</RetainUntilDate>
</Retention>
```

## 响应示例<a name="section10684516817"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016435CE298386946AE4C482
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
Date: WED, 01 Jul 2015 02:25:06 GMT
Content-Length: 0
```

