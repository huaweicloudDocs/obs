# 获取桶级默认WORM策略<a name="obs_04_0168"></a>

## 功能介绍<a name="section6114129132213"></a>

获取该桶设置的桶级默认WORM策略。

要正确执行此操作，需要确保操作者有GetBucketObjectLockConfiguration权限。默认情况下只有桶的所有者可以执行此操作，也可以通过设置桶策略或用户策略授权给其他用户。

>![](public_sys-resources/icon-note.gif) **说明：** 
>如果您打开了桶级WORM开关，但从未配置过桶级默认WORM策略，您依然可以使用此接口查看开关的打开情况。

## 请求消息样式<a name="section8242218182219"></a>

```
GET /?object-lock HTTP/1.1
Host: bucketname.obs.cn-north-4.myhuaweicloud.com
Date: date
Authorization: authorization
Content-Type: application/xml
Content-Length: length
```

## 请求消息参数<a name="section1523630102210"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section124123711224"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section12877144252210"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section839134922216"></a>

```
HTTP/1.1 status_code
Date: date
Content-Type: application/xml
Content-Length: length

<?xml version="1.0" encoding="UTF-8"?>
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

## 响应消息头<a name="section22975413237"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section72110115233"></a>

在此请求返回的响应消息体中包含的桶级默认WORM策略元素如下[表1](#table17259161213419)描述。

**表 1**  桶级默认WORM策略元素

|名称|描述|
|--|--|
|ObjectLockConfiguration|桶级WORM配置的容器类型：Container|
|ObjectLockEnabled|WORM开关状态，只能为Enabled类型：String示例：Enabled|
|Rule|桶级默认WORM策略的规则容器，如果从未配置过桶级默认WORM策略，则返回中不会包含此部分类型：Container|
|DefaultRetention|桶级默认WORM策略的容器类型：Container|
|Mode|默认的保护策略，当前仅支持合规模式"COMPLIANCE"类型：String示例：COMPLIANCE|
|Days|默认的保护天数，取值范围为1-36500天类型：Integer示例：1|
|Years|默认的保护年数，取值范围为1-100年，一年实际上视为保护365天，不会考虑闰年类型：Integer示例：1|


## 错误响应消息<a name="section32451518182310"></a>

此请求可能的特殊错误如下[表2](#table13791928162213)描述。

**表 2** 

|错误码|描述|HTTP状态码|
|--|--|--|
|InvalidRequest|目标桶没有开启桶级WORM开关|400|


其余错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例 1<a name="section4223182814232"></a>

打开了桶级WORM开关，未配置桶级默认WORM策略的情况

```
GET /?object-lock HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 02:25:05 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
Content-Length: 0
```

## 响应示例 1<a name="section1533013378230"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016435CE298386946AE4C482
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
Date: WED, 01 Jul 2015 02:25:06 GMT
Content-Length: 157

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>  <ObjectLockEnabled>Enabled</ObjectLockEnabled>
</ObjectLockConfiguration>
```

## 请求示例 2<a name="section1981774824014"></a>

打开了桶级WORM开关，且配置了桶级默认WORM策略的情况：

```
GET /?object-lock HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 02:25:05 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
Content-Length: 0
```

## 响应示例 2<a name="section18751190114410"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016435CE298386946AE4C482
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
Date: WED, 01 Jul 2015 02:25:06 GMT
Content-Length: 157

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ObjectLockConfiguration xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/">
  <ObjectLockEnabled>Enabled</ObjectLockEnabled>
  <Rule>
    <DefaultRetention>
      <Mode>COMPLIANCE</Mode>
      <Days>10</Days>
      <Years>0</Years>
    </DefaultRetention>
  </Rule>
</ObjectLockConfiguration>
```

