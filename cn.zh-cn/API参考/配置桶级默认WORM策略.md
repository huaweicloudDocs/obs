# 配置桶级默认WORM策略<a name="obs_04_0167"></a>

## 功能介绍<a name="section825319515138"></a>

桶的WORM开关开启后，支持配置默认保护策略和保护期限。

当您在桶内配置了桶级默认WORM策略以后，如果您在上传对象时没有指定保护策略和保护期限，则新上传的对象会自动应用桶级默认WORM策略。和配置对象级WORM保护策略不同的地方在于，对象级WORM保护策略需要您提供一个明确的时间，在这个时间之前对象都会受到保护，桶级默认WORM策略则要求您提供一个保护期限，实际上对象受到保护的时间点为其上传时间+您指定的保护期限。

要正确执行此操作，需要确保执行者有 "PutBucketObjectLockConfiguration"权限。默认情况下只有桶的所有者可以执行此操作，也可以通过设置桶策略或用户策略授权给其他用户。

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   您可以修改甚至清空桶级默认WORM策略，但这仅对修改后上传的对象生效，修改前上传的对象的保护状态不受影响。
>-   多段上传的对象在合并前不受保护，合并后受桶级默认对象策略保护，您可以在其合并后单独为其配置对象级WORM保护策略。

其它约束如下：

-   策略目前仅支持设置为合规模式"COMPLIANCE"
-   支持设置的保留期限为1天-100\*365天或1年\~100年。

## 请求消息样式<a name="section1035113371133"></a>

```
PUT /?object-lock HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
Date: date
Authorization: authorization
Content-Type: application/xml
Content-Length: length
<ObjectLockConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/">
    <ObjectLockEnabled>Enabled</ObjectLockEnabled>
    <Rule>
       <DefaultRetention>
          <Days>integer</Days>
          <Mode>COMPLIANCE</Mode>
          <Years>integer</Years>
       </DefaultRetention>
    </Rule>
</ObjectLockConfiguration>
```

## 请求消息参数<a name="section4305204519136"></a>

该请求消息中不使用消息参数

## 请求消息头<a name="section1555665711135"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section1994410681414"></a>

**表 1**  请求消息元素表

|**名字**|**描述**|**是否必选**|
|--|--|--|
|ObjectLockConfiguration|桶级WORM配置的容器类型：Container|是|
|ObjectLockEnabled|桶级WORM开关状态，只能为Enabled类型：String示例：Enabled|否|
|Rule|桶级默认WORM策略的规则容器类型：Container|设置桶级默认WORM策略配置时必选，不携带则会清空当前配置的桶级默认WORM策略|
|DefaultRetention|桶级默认WORM策略的容器类型：Container|如果有Rule容器则必选|
|Mode|默认的保护策略，当前仅支持合规模式"COMPLIANCE"类型：String示例：COMPLIANCE|如果有DefaultRetention容器则必选|
|Days|默认的保护天数，取值范围为1-36500天类型：Integer示例：1|如果有DefaultRetention容器则和Years二选一，必须选择其中一个且不能同时指定|
|Years|默认的保护年数，取值范围为1-100年，一年实际上视为保护365天，不会考虑闰年类型：Integer示例：1|如果有DefaultRetention容器则和Days二选一，必须选择其中一个且不能同时指定|


## 响应消息样式<a name="section5720132219153"></a>

```
HTTP/1.1 status_code
Date: date
Content-Length: length
```

## 响应消息头<a name="section11201162351411"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section7772229111415"></a>

该请求的响应消息不带消息元素。

## 错误响应消息<a name="section15262153611419"></a>

此请求可能的特殊错误如下[表2](#table13791928162213)描述。

**表 2** 

|错误码|描述|HTTP状态码|
|--|--|--|
|InvalidRequest|目标桶没有开启桶级WORM开关|400|
|MalformedXML|策略配置格式错误|400|


其余错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例 1<a name="section1451984311413"></a>

配置桶级默认WORM策略为保护两年

```
PUT /?object-lock HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
Date: WED, 01 Jul 2015 02:25:05 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
Content-Type: application/xml
Content-Length: 157
<ObjectLockConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/">
    <ObjectLockEnabled>Enabled</ObjectLockEnabled>
    <Rule>
       <DefaultRetention>
          <Mode>COMPLIANCE</Mode>
          <Years>2</Years>
       </DefaultRetention>
    </Rule>
</ObjectLockConfiguration>
```

## 响应示例 1<a name="section179921048191417"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016435CE298386946AE4C482
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
Date: WED, 01 Jul 2015 02:25:06 GMT
Content-Length: 0
```

## 请求示例 2<a name="section28394401810"></a>

清空当前的桶级默认WORM策略配置

```
PUT /?object-lock HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
Date: WED, 01 Jul 2015 02:25:05 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
Content-Type: application/xml
Content-Length: 157
<ObjectLockConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/">
</ObjectLockConfiguration>
```

## 响应示例 2<a name="section13520621188"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016435CE298386946AE4C482
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
Date: WED, 01 Jul 2015 02:25:06 GMT
Content-Length: 0
```

