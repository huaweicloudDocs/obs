# 获取桶ACL<a name="ZH-CN_TOPIC_0100846754"></a>

## 功能介绍<a name="section5584184924715"></a>

用户执行获取桶ACL的操作，返回信息包含指定桶的权限控制列表信息。用户必须拥有对指定桶READ\_ACP的权限或FULL\_CONTROL权限，才能执行获取桶ACL的操作。

## 请求消息样式<a name="section29461583"></a>

```
GET /?acl HTTP/1.1 
Host: bucketname.obs.cn-north-1.myhuaweicloud.com 
Date: date
Authorization: authorization
```

## 请求消息参数<a name="section63827656"></a>

该请求消息中不使用消息参数。

## 请求消息头<a name="section37578000"></a>

该请求使用公共消息头，具体参见[表3](REST-API介绍.md#table25197309)。

## 请求消息元素<a name="section2657687"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section23919191"></a>

```
HTTP/1.1 status_code
Date: date
Content-Length: length
Content-Type: application/xml 

<?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
<AccessControlPolicy xmlns="http://obs.cn-north-1.myhuaweicloud.com/doc/2015-06-30/"> 
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

该请求的响应消息使用公共消息头，具体请参考[表4](REST-API介绍.md#d0e686)。

## 响应消息元素<a name="section58406281"></a>

该请求的响应中以消息元素的形式返回桶的ACL信息，元素的具体意义如[表1](#table46938871)所示。

**表 1**  响应消息元素

<a name="table46938871"></a>
<table><thead align="left"><tr id="row22931300"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p45495974"><a name="p45495974"></a><a name="p45495974"></a><strong id="b6810588"><a name="b6810588"></a><a name="b6810588"></a>元素</strong></p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p14786732"><a name="p14786732"></a><a name="p14786732"></a><strong id="b65971729"><a name="b65971729"></a><a name="b65971729"></a>元素说明</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row42109833"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p55453326"><a name="p55453326"></a><a name="p55453326"></a>Owner</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p62534407"><a name="p62534407"></a><a name="p62534407"></a>桶的所有者信息。</p>
<p id="p25938755"><a name="p25938755"></a><a name="p25938755"></a>类型：XML。</p>
</td>
</tr>
<tr id="row32122205"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p51761783"><a name="p51761783"></a><a name="p51761783"></a>ID</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p31954877"><a name="p31954877"></a><a name="p31954877"></a>用户所示租户的租户Id。</p>
<p id="p19158445"><a name="p19158445"></a><a name="p19158445"></a>类型：字符串。</p>
</td>
</tr>
<tr id="row49697845"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p66102514"><a name="p66102514"></a><a name="p66102514"></a>AccessControlList</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p52703436"><a name="p52703436"></a><a name="p52703436"></a>访问控制列表，记录了对该桶有访问权限的用户列表和这些用户具有的权限。</p>
<p id="p4568879"><a name="p4568879"></a><a name="p4568879"></a>类型：XML。</p>
</td>
</tr>
<tr id="row41119914"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p42378741"><a name="p42378741"></a><a name="p42378741"></a>Grant</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p10125972"><a name="p10125972"></a><a name="p10125972"></a>用于标记用户及用户的权限。</p>
<p id="p24024887"><a name="p24024887"></a><a name="p24024887"></a>类型：XML。</p>
</td>
</tr>
<tr id="row14897392"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p65838064"><a name="p65838064"></a><a name="p65838064"></a>Grantee</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p31282940"><a name="p31282940"></a><a name="p31282940"></a>记录用户信息。</p>
<p id="p13111011"><a name="p13111011"></a><a name="p13111011"></a>类型：XML。</p>
</td>
</tr>
<tr id="row22578699105646"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p39717156105654"><a name="p39717156105654"></a><a name="p39717156105654"></a>Canned</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p62973095105654"><a name="p62973095105654"></a><a name="p62973095105654"></a>向所有人授予权限。</p>
<p id="p29886945105654"><a name="p29886945105654"></a><a name="p29886945105654"></a>类型：枚举类型。其值只能是Everyone。</p>
</td>
</tr>
<tr id="row33068941105651"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p32426193105654"><a name="p32426193105654"></a><a name="p32426193105654"></a>Delivered</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p9275973105654"><a name="p9275973105654"></a><a name="p9275973105654"></a>桶的ACL是否向桶内对象传递。</p>
<p id="p16374900105654"><a name="p16374900105654"></a><a name="p16374900105654"></a>类型：布尔类型。</p>
</td>
</tr>
<tr id="row50890237"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p28468571"><a name="p28468571"></a><a name="p28468571"></a>Permission</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p24252925"><a name="p24252925"></a><a name="p24252925"></a>指定的用户对该桶所具有的操作权限。</p>
<p id="p16949740"><a name="p16949740"></a><a name="p16949740"></a>类型：字符串。</p>
</td>
</tr>
</tbody>
</table>

## 错误响应消息<a name="section55894487"></a>

无特殊错误，所有错误已经包含在[表1](错误码列表.md#d0e843)中。

## 请求示例<a name="section14819157124617"></a>

```
GET /?acl HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
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
<AccessControlPolicy xmlns="http://obs.myhuaweicloud.com/doc/2015-06-30/">
  
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

