# 设置桶ACL<a name="obs_04_0030"></a>

## 功能介绍<a name="section5584184924715"></a>

OBS支持对桶操作进行权限控制。默认情况下，只有桶的创建者才有该桶的读写权限。用户也可以设置其他的访问策略，比如对一个桶可以设置公共访问策略，允许所有人对其都有读权限。

OBS用户在创建桶时可以设置权限控制策略，也可以通过ACL操作API接口对已存在的桶更改或者获取ACL\(access control list\) 。一个桶的ACL最多支持100条Grant授权。PUT接口为幂等的覆盖写语意，新设置的桶ACL将覆盖原有的桶ACL，如果需要修改或者删除某条ACL重新PUT一个新的桶ACL即可。

使用桶ACL进行权限控制请参考《对象存储服务权限配置指南》的[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)章节。

## 请求消息样式<a name="section8518944"></a>

```
PUT /?acl HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Date: date
Authorization: authorization
Content-Type: application/xml 
Content-Length: length

<AccessControlPolicy> 
    <Owner> 
        <ID>ID</ID> 
    </Owner> 
    <AccessControlList> 
        <Grant> 
            <Grantee>
               <ID>domainId</ID>
            </Grantee> 
            <Permission>permission</Permission> 
            <Delivered>false</Delivered>
        </Grant>
    </AccessControlList> 
</AccessControlPolicy>
```

## 请求消息参数<a name="section9561640"></a>

该操作请求不带消息参数。

## 请求消息头<a name="section18945901"></a>

使用者可以使用头域设置的方式来更改桶的ACL，每一种头域设置的ACL都有一套自己预先定义好的被授权用户以及相应权限，通过头域设置的方式授予访问权限，使用者必须添加以下的头域并且指定取值。

**表 1**  头域方式设置桶ACL

|名称|描述|是否必须|
|--|--|--|
|x-obs-acl|通过canned ACL的方式来设置桶的ACL。取值范围：private | public-read | public-read-write | public-read-delivered | public-read-write-delivered类型：String|否|


## 请求消息元素<a name="section36295384"></a>

更改桶的ACL请求需要在消息元素中带上ACL信息，元素的具体含义如[表3](构造请求.md#table25197309)所示。

**表 2**  附加请求消息元素

|**元素名称**|**描述**|**是否必选**|
|--|--|--|
|Owner|桶的所有者信息，包含ID。类型：XML|是|
|ID|被授权用户的租户Id。类型：String|是|
|Grant|用于标记用户及用户的权限。单个桶的ACL，Grant元素不能超过100个。类型：XML|否|
|Grantee|记录用户信息。类型：XML|否|
|Canned|向所有人授予权限。取值范围：Everyone类型：String|否|
|Delivered|桶的ACL是否向桶内对象传递。作用于桶内所有对象。类型：Boolean默认：false|否|
|Permission|授予的权限。详情参见桶ACL访问权限。取值范围：READ | READ_ACP | WRITE | WRITE_ACP | FULL_CONTROL类型：String|否|
|AccessControlList|访问控制列表，包含Grant、 Grantee、Permission三个元素。类型：XML|是|


## 响应消息样式<a name="section58223002"></a>

```
HTTP/1.1 status_code
Date: date
Content-Length: length
```

## 响应消息头<a name="section54244972"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section18442703"></a>

该请求的响应消息中不带有响应元素。

## 错误响应消息<a name="section31766605"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section14482163815396"></a>

```
PUT /?acl HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 02:37:22 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:iqSPeUBl66PwXDApxjRKk6hlcN4=
Content-Length: 727

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

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF2600000164361F2954B4D063164704
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT78HTIBuhe0FbtSptrb/akwELtwyPKs
Date: WED, 01 Jul 2015 02:37:22 GMT
Content-Length: 0
```

## 请求示例：使用头域方式指定的访问权限<a name="section835691118820"></a>

```
PUT /?acl HTTP/1.1
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:iqSPeUBl66PwXDApxjRKk6hlcN4=
User-Agent: curl/7.29.0
Host: examplebucket.obs.region.myhuaweicloud.com
x-obs-acl: private
Date: WED, 01 Jul 2015 02:37:22 GMT
Content-Type: application/xml
```

## 响应示例：使用头域方式指定的访问权限<a name="section051115261698"></a>

```
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSmpL2dv6zZLM2HmUrXKTAi258MPqmrp
x-obs-request-id: 0000018A2A73AF59D3085C8F8ABF0C65
Server: OBS
Content-Length: 0
Date: WED, 01 Jul 2015 02:37:22 GMT
```

