# 获取对象ACL<a name="obs_04_0090"></a>

## 功能介绍<a name="section5584184924715"></a>

用户执行获取对象ACL的操作，返回信息包含指定对象的权限控制列表信息。用户必须拥有对指定对象读ACP\(access control policy\)的权限，才能执行获取对象ACL的操作。

## 多版本<a name="section53856681"></a>

默认情况下，获取最新版本的对象ACL。如果最新版本的对象是删除标记，则返回404。如果要获取指定版本的对象ACL，请求可携带versionId消息参数。

## 请求消息样式<a name="section14948084"></a>

```
GET /ObjectName?acl HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization
```

## 请求消息参数<a name="section315031"></a>

该请求需要在请求消息参数中指定是在获取对象ACL，参数意义如[表1](#table22962068)所示。

**表 1**  请求消息参数

|**参数名称**|**描述**|**是否必选**|
|--|--|--|
|versionId|指定对象的版本号。类型：String|否|


## 请求消息头<a name="section2835283"></a>

该请求使用公共消息头，具体请参考[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section25517554"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section28331395"></a>

```
HTTP/1.1 status_code
Date: date
Content-Length: length
Content-Type: application/xml 

<?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
<AccessControlPolicy xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/"> 
    <Owner> 
        <ID>id</ID> 
    </Owner> 
    <Delivered>true</Delivered>
    <AccessControlList> 
        <Grant> 
            <Grantee> 
                <ID>id</ID> 
            </Grantee> 
            <Permission>permission</Permission> 
        </Grant> 
    </AccessControlList> 
</AccessControlPolicy>
```

## 响应消息头<a name="section53655969"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

除公共响应消息头之外，还可能使用如下[表2](#table995015721520)中的消息头。

**表 2**  附加响应消息头

|消息头名称|描述|
|--|--|
|x-obs-version-id|指定对象的版本号。有效值：字符串默认值：无|


## 响应消息元素<a name="section13141676"></a>

该请求的响应消息中通过消息元素返回对象的ACL信息，元素的具体意义如[表3](#table23161487)所示。

**表 3**  响应消息元素

|**元素名称**|**描述**|
|--|--|
|ID|用户的DomainId。类型：String|
|AccessControlList|访问控制列表，记录了对该桶有访问权限的用户列表。类型：XML|
|Grant|用于标记用户及用户的权限。类型：XML|
|Grantee|记录用户信息。类型：XML|
|Delivered|对象ACL是否继承桶的ACL。类型：Boolean|
|Permission|指定的用户对该对象所具有的操作权限。类型：String|


## 错误响应消息<a name="section51166221"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section339018376100"></a>

```
GET /object011?acl HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:45:55 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:YcmvNQxItGjFeeC1K2HeUEp8MMM=
```

## 响应示例<a name="section179715418192"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D3E650F3065C2295674C
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCS+wsHqRuA2Tx+mXUpNtBbWLPMle9CIx
Content-Type: application/xml
Date: WED, 01 Jul 2015 04:45:55 GMT
Content-Length: 769

<?xml version="1.0" encoding="utf-8"?>
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
      <Permission>READ_ACP</Permission> 
    </Grant> 
  </AccessControlList> 
</AccessControlPolicy>
```

## 请求示例：已启用版本控制<a name="section1512511218519"></a>

```
GET /object01?acl HTTP/1.1
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:iqSPeUBl66PwXDApxjRKk6hlcN4=
versionId: G001118A6803675AFFFFD3043F7F91D0
User-Agent: curl/7.29.0
Host: examplebucket.obs.region.myhuaweicloud.com
Date: WED, 01 Jul 2015 02:37:22 GMT
Content-Type: application/xml
```

## 响应示例：已启用版本控制<a name="section4839225185411"></a>

```
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSmpL2dv6zZLM2HmUrXKTAi258MPqmrp
x-obs-request-id: 0000018A2A73AF59D3085C8F8ABF0C65
Server: OBS
Content-Length: 0
Date: WED, 01 Jul 2015 02:37:22 GMT
x-obs-version-id: G001118A6803675AFFFFD3043F7F91D0
 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AccessControlPolicy  xmlns="http://obs.myhwclouds.com/doc/2015-06-30/">
    <Owner>
        <ID>d6s58yhnm83f3081577800575ee4cf</ID>
    </Owner>
    <Delivered>false</Delivered>
    <AccessControlList>
        <Grant>
            <Grantee>
                <ID>f262a63g69422e8f330af1349c588f</ID>
            </Grantee>
            <Permission>READ</Permission>
        </Grant>
        <Grant>
            <Grantee>
                <ID>c965gfda2a849422e8f3985562432dsaa</ID>
            </Grantee>
            <Permission>FULL_CONTROL</Permission>
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

