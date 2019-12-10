# 获取对象ACL<a name="ZH-CN_TOPIC_0100846781"></a>

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

<a name="table22962068"></a>
<table><thead align="left"><tr id="row51500263"><th class="cellrowborder" valign="top" width="24.240000000000002%" id="mcps1.2.4.1.1"><p id="p10771806"><a name="p10771806"></a><a name="p10771806"></a><strong id="b29837390"><a name="b29837390"></a><a name="b29837390"></a>参数名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="57.58%" id="mcps1.2.4.1.2"><p id="p909510"><a name="p909510"></a><a name="p909510"></a><strong id="b8185591"><a name="b8185591"></a><a name="b8185591"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="18.18%" id="mcps1.2.4.1.3"><p id="p59053163"><a name="p59053163"></a><a name="p59053163"></a><strong id="b61716423"><a name="b61716423"></a><a name="b61716423"></a>是否必选</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row32974368"><td class="cellrowborder" valign="top" width="24.240000000000002%" headers="mcps1.2.4.1.1 "><p id="p53678186"><a name="p53678186"></a><a name="p53678186"></a>acl</p>
</td>
<td class="cellrowborder" valign="top" width="57.58%" headers="mcps1.2.4.1.2 "><p id="p52965837"><a name="p52965837"></a><a name="p52965837"></a>指定该请求是获取对象的acl。</p>
<p id="p6930487"><a name="p6930487"></a><a name="p6930487"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.4.1.3 "><p id="p24498545"><a name="p24498545"></a><a name="p24498545"></a>是</p>
</td>
</tr>
<tr id="row19160315"><td class="cellrowborder" valign="top" width="24.240000000000002%" headers="mcps1.2.4.1.1 "><p id="p8481687"><a name="p8481687"></a><a name="p8481687"></a>versionId</p>
</td>
<td class="cellrowborder" valign="top" width="57.58%" headers="mcps1.2.4.1.2 "><p id="p15928043"><a name="p15928043"></a><a name="p15928043"></a>指定对象的版本号。</p>
<p id="p9134666"><a name="p9134666"></a><a name="p9134666"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="18.18%" headers="mcps1.2.4.1.3 "><p id="p1710502"><a name="p1710502"></a><a name="p1710502"></a>否</p>
</td>
</tr>
</tbody>
</table>

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

<a name="table995015721520"></a>
<table><thead align="left"><tr id="row43542352"><th class="cellrowborder" valign="top" width="40.400000000000006%" id="mcps1.2.3.1.1"><p id="p37269637"><a name="p37269637"></a><a name="p37269637"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="59.599999999999994%" id="mcps1.2.3.1.2"><p id="p66050606"><a name="p66050606"></a><a name="p66050606"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row48498868"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p36094206"><a name="p36094206"></a><a name="p36094206"></a>x-obs-version-id</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p37949556"><a name="p37949556"></a><a name="p37949556"></a>指定对象的版本号。</p>
<p id="p6001692"><a name="p6001692"></a><a name="p6001692"></a>有效值：字符串</p>
<p id="p54015232"><a name="p54015232"></a><a name="p54015232"></a>默认值：无</p>
</td>
</tr>
</tbody>
</table>

## 响应消息元素<a name="section13141676"></a>

该请求的响应消息中通过消息元素返回对象的ACL信息，元素的具体意义如[表3](#table23161487)所示。

**表 3**  响应消息元素

<a name="table23161487"></a>
<table><thead align="left"><tr id="row5296547"><th class="cellrowborder" valign="top" width="35.35%" id="mcps1.2.3.1.1"><p id="p26367153"><a name="p26367153"></a><a name="p26367153"></a><strong id="b35977789"><a name="b35977789"></a><a name="b35977789"></a>元素名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="64.64999999999999%" id="mcps1.2.3.1.2"><p id="p28519821"><a name="p28519821"></a><a name="p28519821"></a><strong id="b55351803"><a name="b55351803"></a><a name="b55351803"></a>描述</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row64485412"><td class="cellrowborder" valign="top" width="35.35%" headers="mcps1.2.3.1.1 "><p id="p55935922"><a name="p55935922"></a><a name="p55935922"></a>ID</p>
</td>
<td class="cellrowborder" valign="top" width="64.64999999999999%" headers="mcps1.2.3.1.2 "><p id="p34515844"><a name="p34515844"></a><a name="p34515844"></a>用户的DomainId。</p>
<p id="p42207147"><a name="p42207147"></a><a name="p42207147"></a>类型：字符串。</p>
</td>
</tr>
<tr id="row44320003"><td class="cellrowborder" valign="top" width="35.35%" headers="mcps1.2.3.1.1 "><p id="p33150486"><a name="p33150486"></a><a name="p33150486"></a>AccessControlList</p>
</td>
<td class="cellrowborder" valign="top" width="64.64999999999999%" headers="mcps1.2.3.1.2 "><p id="p834854"><a name="p834854"></a><a name="p834854"></a>访问控制列表，记录了对该桶有访问权限的用户列表。</p>
<p id="p7513688"><a name="p7513688"></a><a name="p7513688"></a>类型：XML。</p>
</td>
</tr>
<tr id="row514330"><td class="cellrowborder" valign="top" width="35.35%" headers="mcps1.2.3.1.1 "><p id="p41660763"><a name="p41660763"></a><a name="p41660763"></a>Grant</p>
</td>
<td class="cellrowborder" valign="top" width="64.64999999999999%" headers="mcps1.2.3.1.2 "><p id="p19078608"><a name="p19078608"></a><a name="p19078608"></a>用于标记用户及用户的权限。</p>
<p id="p37489745"><a name="p37489745"></a><a name="p37489745"></a>类型：XML。</p>
</td>
</tr>
<tr id="row1863393"><td class="cellrowborder" valign="top" width="35.35%" headers="mcps1.2.3.1.1 "><p id="p16717176"><a name="p16717176"></a><a name="p16717176"></a>Grantee</p>
</td>
<td class="cellrowborder" valign="top" width="64.64999999999999%" headers="mcps1.2.3.1.2 "><p id="p11913978"><a name="p11913978"></a><a name="p11913978"></a>记录用户信息。</p>
<p id="p40116944"><a name="p40116944"></a><a name="p40116944"></a>类型：XML。</p>
</td>
</tr>
<tr id="row236755121147"><td class="cellrowborder" valign="top" width="35.35%" headers="mcps1.2.3.1.1 "><p id="p1561393711411"><a name="p1561393711411"></a><a name="p1561393711411"></a>Delivered</p>
</td>
<td class="cellrowborder" valign="top" width="64.64999999999999%" headers="mcps1.2.3.1.2 "><p id="p5676939411411"><a name="p5676939411411"></a><a name="p5676939411411"></a>对象ACL是否继承桶的ACL。</p>
<p id="p4116250211411"><a name="p4116250211411"></a><a name="p4116250211411"></a>类型：布尔类型。</p>
</td>
</tr>
<tr id="row25508177"><td class="cellrowborder" valign="top" width="35.35%" headers="mcps1.2.3.1.1 "><p id="p52896485"><a name="p52896485"></a><a name="p52896485"></a>Permission</p>
</td>
<td class="cellrowborder" valign="top" width="64.64999999999999%" headers="mcps1.2.3.1.2 "><p id="p56756893"><a name="p56756893"></a><a name="p56756893"></a>指定的用户对该对象所具有的操作权限。</p>
<p id="p41049994"><a name="p41049994"></a><a name="p41049994"></a>类型：字符串。</p>
</td>
</tr>
</tbody>
</table>

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

