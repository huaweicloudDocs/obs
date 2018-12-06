# 设置对象ACL<a name="ZH-CN_TOPIC_0100846778"></a>

## 功能介绍<a name="section5584184924715"></a>

OBS支持对对象的操作进行权限控制。默认情况下，只有对象的创建者才有该对象的读写权限。用户也可以设置其他的访问策略，比如对一个对象可以设置公共访问策略，允许所有人对其都有读权限。SSE-KMS方式加密的对象即使设置了ACL，跨租户也不生效。

OBS用户在上传对象时可以设置权限控制策略，也可以通过ACL操作API接口对已存在的对象更改或者获取ACL\(access control list\) 。

本节将介绍如何更改对象ACL，改变对象的访问权限。

## 多版本<a name="section48384196"></a>

默认情况下，更改的是最新版本的对象ACL。要设置指定版本的对象ACL，请求可以带参数versionId。

## 请求消息格式<a name="section32804580"></a>

```
PUT /ObjectName?acl HTTP/1.1 
Host: bucketname.obs.cn-north-1.myhuaweicloud.com 
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

<a name="table44298471191845"></a>
<table><thead align="left"><tr id="row25509231"><th class="cellrowborder" valign="top" width="22.220000000000002%" id="mcps1.2.4.1.1"><p id="p52981853"><a name="p52981853"></a><a name="p52981853"></a><strong id="b7074630"><a name="b7074630"></a><a name="b7074630"></a>参数名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="62.629999999999995%" id="mcps1.2.4.1.2"><p id="p36174163"><a name="p36174163"></a><a name="p36174163"></a><strong id="b57132017"><a name="b57132017"></a><a name="b57132017"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="15.15%" id="mcps1.2.4.1.3"><p id="p64290664"><a name="p64290664"></a><a name="p64290664"></a><strong id="b41745067"><a name="b41745067"></a><a name="b41745067"></a>是否必选</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row25907270"><td class="cellrowborder" valign="top" width="22.220000000000002%" headers="mcps1.2.4.1.1 "><p id="p18114101"><a name="p18114101"></a><a name="p18114101"></a>versionId</p>
</td>
<td class="cellrowborder" valign="top" width="62.629999999999995%" headers="mcps1.2.4.1.2 "><p id="p57956065"><a name="p57956065"></a><a name="p57956065"></a>对象的版本号。标示更改指定版本的对象ACL。</p>
<p id="p51842537"><a name="p51842537"></a><a name="p51842537"></a>类型：字符串</p>
</td>
<td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.4.1.3 "><p id="p38495930"><a name="p38495930"></a><a name="p38495930"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 请求消息头<a name="section39925296"></a>

该请求使用公共请求消息头，具体参见[表3](REST-API介绍.md#table25197309)。

## 请求消息元素<a name="section23783351"></a>

该请求消息通过带消息元素来传递对象的ACL信息，元素的意义如[表2](#table6365150)所示。

**表 2**  请求消息元素

<a name="table6365150"></a>
<table><thead align="left"><tr id="row46397570"><th class="cellrowborder" valign="top" width="25.509999999999998%" id="mcps1.2.4.1.1"><p id="p106807"><a name="p106807"></a><a name="p106807"></a><strong id="b961269"><a name="b961269"></a><a name="b961269"></a>元素名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="41.839999999999996%" id="mcps1.2.4.1.2"><p id="p10753930"><a name="p10753930"></a><a name="p10753930"></a><strong id="b29676507"><a name="b29676507"></a><a name="b29676507"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="32.65%" id="mcps1.2.4.1.3"><p id="p54986906"><a name="p54986906"></a><a name="p54986906"></a><strong id="b25120114"><a name="b25120114"></a><a name="b25120114"></a>是否必选</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row21463316"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p60807051"><a name="p60807051"></a><a name="p60807051"></a>ID</p>
</td>
<td class="cellrowborder" valign="top" width="41.839999999999996%" headers="mcps1.2.4.1.2 "><p id="p26424127"><a name="p26424127"></a><a name="p26424127"></a>用户DomainId。</p>
<p id="p36490555"><a name="p36490555"></a><a name="p36490555"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="32.65%" headers="mcps1.2.4.1.3 "><p id="p2944980"><a name="p2944980"></a><a name="p2944980"></a>否</p>
</td>
</tr>
<tr id="row4036034411024"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p4238406111028"><a name="p4238406111028"></a><a name="p4238406111028"></a>Delivered</p>
</td>
<td class="cellrowborder" valign="top" width="41.839999999999996%" headers="mcps1.2.4.1.2 "><p id="p1055692911028"><a name="p1055692911028"></a><a name="p1055692911028"></a>对象ACL是否继承桶的ACL。</p>
<p id="p2790349711028"><a name="p2790349711028"></a><a name="p2790349711028"></a>类型：布尔类型。默认true。</p>
</td>
<td class="cellrowborder" valign="top" width="32.65%" headers="mcps1.2.4.1.3 "><p id="p4559078011028"><a name="p4559078011028"></a><a name="p4559078011028"></a>否</p>
</td>
</tr>
<tr id="row34127147"><td class="cellrowborder" valign="top" width="25.509999999999998%" headers="mcps1.2.4.1.1 "><p id="p12835559"><a name="p12835559"></a><a name="p12835559"></a>Permission</p>
</td>
<td class="cellrowborder" valign="top" width="41.839999999999996%" headers="mcps1.2.4.1.2 "><p id="p33047326"><a name="p33047326"></a><a name="p33047326"></a>授予权限。</p>
<p id="p28990484"><a name="p28990484"></a><a name="p28990484"></a>类型：枚举类型。</p>
</td>
<td class="cellrowborder" valign="top" width="32.65%" headers="mcps1.2.4.1.3 "><p id="p66527890"><a name="p66527890"></a><a name="p66527890"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 响应消息样式<a name="section12723569"></a>

```
HTTP/1.1 status_code
Content-Length: length
Content-Type: application/xml
```

## 响应消息头<a name="section47403265"></a>

该请求的响应消息使用公共消息头，具体请参考[表4](REST-API介绍.md#d0e686)。

除公共响应消息头之外，还可能使用如[表3](#table21765641102739)中的消息头。

**表 3**  附加响应消息头

<a name="table21765641102739"></a>
<table><thead align="left"><tr id="row52223563"><th class="cellrowborder" valign="top" width="40.400000000000006%" id="mcps1.2.3.1.1"><p id="p2250249"><a name="p2250249"></a><a name="p2250249"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="59.599999999999994%" id="mcps1.2.3.1.2"><p id="p48052491"><a name="p48052491"></a><a name="p48052491"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row67046586"><td class="cellrowborder" valign="top" width="40.400000000000006%" headers="mcps1.2.3.1.1 "><p id="p62064381"><a name="p62064381"></a><a name="p62064381"></a>x-obs-version-id</p>
</td>
<td class="cellrowborder" valign="top" width="59.599999999999994%" headers="mcps1.2.3.1.2 "><p id="p61158973"><a name="p61158973"></a><a name="p61158973"></a>被更改ACL的对象的版本号。</p>
<p id="p13559847"><a name="p13559847"></a><a name="p13559847"></a>类型：字符串</p>
</td>
</tr>
</tbody>
</table>

## 响应消息元素<a name="section23976207"></a>

该请求的响应消息中不带有消息元素。

## 错误响应消息<a name="section14459276"></a>

该请求的响应无特殊错误，所有错误已经包含在[表1](错误码列表.md#d0e843)中。

## 请求实例<a name="section817219485150"></a>

```
PUT /obj2?acl HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:42:34 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:8xAODun1ofjkwHm8YhtN0QEcy9M=
Content-Length: 727

<AccessControlPolicy xmlns="http://obs.myhuaweicloud.com/doc/2015-06-30/">  
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

## 响应实例<a name="section1981019229519"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D3F0FD2A03D2D30B0542
x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCTjCqTmsA1XRpIrmrJdvcEWvZyjbztdd
Date: WED, 01 Jul 2015 04:42:34 GMT
Content-Length: 0
```

