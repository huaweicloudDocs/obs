# 设置对象ACL<a name="obs_04_0089"></a>

## 功能介绍<a name="section5584184924715"></a>

OBS支持对对象的操作进行权限控制。默认情况下，只有对象的创建者才有该对象的读写权限。用户也可以设置其他的访问策略，比如对一个对象可以设置公共访问策略，允许所有人对其都有读权限。SSE-KMS方式加密的对象即使设置了ACL，跨租户也不生效。

OBS用户在上传对象时可以设置权限控制策略，也可以通过ACL操作API接口对已存在的对象更改或者获取ACL\(access control list\) 。一个对象的ACL最多支持100条Grant授权。

本节将介绍如何更改对象ACL，改变对象的访问权限。

## 多版本<a name="section48384196"></a>

默认情况下，更改的是最新版本的对象ACL。要设置指定版本的对象ACL，请求可以带参数versionId。

## 请求消息格式<a name="section32804580"></a>

```
PUT /ObjectName?acl HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization

<AccessControlPolicy> 
    <Owner> 
        <ID>ID</ID> 
    </Owner> 
    <Delivered>true</Delivered>
    <AccessControlList> 
        <Grant> 
            <Grantee>
               <ID>ID</ID>
            </Grantee> 
            <Permission>permission</Permission> 
        </Grant> 
    </AccessControlList> 
</AccessControlPolicy>
```

## 请求消息参数<a name="section26805765"></a>

请求参数说明如[表1](#table44298471191845)所示。

**表 1**  请求消息参数

|**参数名称**|**描述**|**是否必选**|
|--|--|--|
|versionId|对象的版本号。标示更改指定版本的对象ACL。类型：String|否|


## 请求消息头<a name="section39925296"></a>

该请求使用公共请求消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section23783351"></a>

该请求消息通过带消息元素来传递对象的ACL信息，元素的意义如[表2](#table6365150)所示。

**表 2**  请求消息元素

|**元素名称**|**描述**|**是否必选**|
|--|--|--|
|Owner|桶的所有者信息，包含ID。类型：XML|是|
|ID|用户DomainId。类型：String|是|
|Grant|用于标记用户及用户的权限。单个对象的ACL，Grant元素不能超过100个。类型：XML|否|
|Grantee|记录用户信息。类型：XML|否|
|Canned|向所有人授予权限。取值范围：Everyone。类型：String|否|
|Delivered|对象ACL是否继承桶的ACL。类型：Boolean默认：true。|否|
|Permission|授予权限。取值范围：READ | READ_ACP | WRITE_ACP | FULL_CONTROL类型：String|否|
|AccessControlList|访问控制列表，包含Grant、 Grantee、Permission三个元素。类型：XML|是|


## 响应消息样式<a name="section12723569"></a>

```
HTTP/1.1 status_code
Content-Length: length
Content-Type: application/xml
```

## 响应消息头<a name="section47403265"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

除公共响应消息头之外，还可能使用如[表3](#table21765641102739)中的消息头。

**表 3**  附加响应消息头

|消息头名称|描述|
|--|--|
|x-obs-version-id|被更改ACL的对象的版本号。类型：String|


## 响应消息元素<a name="section23976207"></a>

该请求的响应消息中不带有消息元素。

## 错误响应消息<a name="section14459276"></a>

该请求的响应无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section817219485150"></a>

```
PUT /obj2?acl HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:42:34 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:8xAODun1ofjkwHm8YhtN0QEcy9M=
Content-Length: 727

<AccessControlPolicy xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/">
  <Owner> 
    <ID>b4bf1b36d9ca43d984fbcb9491b6fce9</ID> 
  </Owner>  
  <Delivered>false</Delivered>
  <AccessControlList> 
    <Grant> 
      <Grantee> 
        <ID>b4bf1b36d9ca43d984fbcb9491b6fce9</ID> 
      </Grantee>  
      <Permission>FULL_CONTROL</Permission> 
    </Grant>  
    <Grant> 
      <Grantee> 
        <ID>783fc6652cf246c096ea836694f71855</ID> 
      </Grantee>  
      <Permission>READ</Permission>
    </Grant>  
    <Grant> 
      <Grantee> 
        <Canned>Everyone</Canned> 
      </Grantee>  
      <Permission>READ</Permission> 
    </Grant> 
  </AccessControlList> 
</AccessControlPolicy>
```

## 响应示例<a name="section1981019229519"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D3F0FD2A03D2D30B0542
x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCTjCqTmsA1XRpIrmrJdvcEWvZyjbztdd
Date: WED, 01 Jul 2015 04:42:34 GMT
Content-Length: 0
```

## 请求示例：已启用版本控制<a name="section1518719170616"></a>

```
PUT /object01?acl&versionId=G001118A6803675AFFFFD3043F7F91D0 HTTP/1.1
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:iqSPeUBl66PwXDApxjRKk6hlcN4=
User-Agent: curl/7.29.0
Host: examplebucket.obs.region.myhuaweicloud.com
Date: WED, 01 Jul 2015 02:37:22 GMT
Content-Type: application/xml
 
<AccessControlPolicy  xmlns="http://obs.region.myhuaweicloud.com/doc/2015-06-30/">
    <Owner>
        <ID>d029cb567d46458sp0x75800575ee4cf</ID>
    </Owner>
    <Delivered>false</Delivered>
    <AccessControlList>
        <Grant>
            <Grantee>
                <ID>f98sx63gg849422e8f330af1349c588f</ID>
            </Grantee>
            <Permission>FULL_CONTROL</Permission>
        </Grant>
        <Grant>
            <Grantee>
                <ID>fa558a82a84946sn98u30af195as3hi5</ID>
            </Grantee>
            <Permission>READ</Permission>
        </Grant>
        <Grant>
            <Grantee>
                <Canned>Everyone</Canned>
            </Grantee>
            <Permission>READ</Permission>
        </Grant>
    </AccessControlList>
</AccessControlPolicy>
```

## 响应示例：已启用版本控制<a name="section69861381066"></a>

```
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSmpL2dv6zZLM2HmUrXKTAi258MPqmrp
x-obs-request-id: 0000018A2A73AF59D3085C8F8ABF0C65
Server: OBS
Content-Length: 0
Date: WED, 01 Jul 2015 02:37:22 GMT
x-obs-version-id: G001118A6803675AFFFFD3043F7F91D0
```

