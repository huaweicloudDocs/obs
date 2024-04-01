# 获取桶ACL<a name="obs_04_0031"></a>

## 功能介绍<a name="section5584184924715"></a>

用户执行获取桶ACL的操作，返回信息包含指定桶的权限控制列表信息。用户必须拥有对指定桶READ\_ACP的权限或FULL\_CONTROL权限，才能执行获取桶ACL的操作。

## 请求消息样式<a name="section29461583"></a>

```
GET /?acl HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization
```

## 请求消息参数<a name="section63827656"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section37578000"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section2657687"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section23919191"></a>

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
    <AccessControlList> 
        <Grant> 
            <Grantee> 
                <ID>id</ID> 
            </Grantee> 
            <Permission>permission</Permission> 
            <Delivered>false</Delivered>
        </Grant> 
    </AccessControlList> 
</AccessControlPolicy>
```

## 响应消息头<a name="section13946127"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section58406281"></a>

该请求的响应中以消息元素的形式返回桶的ACL信息，元素的具体意义如[表1](#table46938871)所示。

**表 1**  响应消息元素

|**元素**|**元素说明**|
|--|--|
|Owner|桶的所有者信息。类型：XML|
|ID|用户所属租户的租户Id。类型：String|
|AccessControlList|访问控制列表，记录了对该桶有访问权限的用户列表和这些用户具有的权限。类型：XML|
|Grant|用于标记用户及用户的权限。类型：XML|
|Grantee|记录用户信息。类型：XML|
|Canned|向所有人授予权限。类型：String，其值只能是Everyone。|
|Delivered|桶的ACL是否向桶内对象传递。类型：Boolean|
|Permission|指定的用户对该桶所具有的操作权限。类型：String|


## 错误响应消息<a name="section55894487"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14819157124617"></a>

```
GET /?acl HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 02:39:28 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:X7HtzGsIEkzJbd8vo1DRu30vVrs=
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF260000016436B69D82F14E93528658
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSjTh8661+HF5y8uAnTOBIpNO133hji+
Content-Type: application/xml
Date: WED, 01 Jul 2015 02:39:28 GMT
Content-Length: 784

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AccessControlPolicy xmlns="http://obs.cn-north-4.myhuaweicloud.com/doc/2015-06-30/">
  <Owner> 
    <ID>b4bf1b36d9ca43d984fbcb9491b6fce9</ID> 
  </Owner>  
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
      <Delivered>false</Delivered> 
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

