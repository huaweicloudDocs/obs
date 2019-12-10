# 设置桶ACL<a name="ZH-CN_TOPIC_0100846744"></a>

## 功能介绍<a name="section5584184924715"></a>

OBS支持对桶操作进行权限控制。默认情况下，只有桶的创建者才有该桶的读写权限。用户也可以设置其他的访问策略，比如对一个桶可以设置公共访问策略，允许所有人对其都有读权限。

OBS用户在创建桶时可以设置权限控制策略，也可以通过ACL操作API接口对已存在的桶更改或者获取ACL\(access control list\) 。

使用桶ACL进行权限控制请参考《对象存储服务开发指南》的[权限控制](https://support.huaweicloud.com/devg-obs/zh-cn_topic_0132788578.html)章节。

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

<a name="table46013138"></a>
<table><thead align="left"><tr id="row55711245"><th class="cellrowborder" valign="top" width="16.36163616361636%" id="mcps1.2.4.1.1"><p id="p16316966"><a name="p16316966"></a><a name="p16316966"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="59.17591759175917%" id="mcps1.2.4.1.2"><p id="p46605831"><a name="p46605831"></a><a name="p46605831"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="24.462446244624463%" id="mcps1.2.4.1.3"><p id="p16975961"><a name="p16975961"></a><a name="p16975961"></a>是否必须</p>
</th>
</tr>
</thead>
<tbody><tr id="row32875587"><td class="cellrowborder" valign="top" width="16.36163616361636%" headers="mcps1.2.4.1.1 "><p id="p45676910"><a name="p45676910"></a><a name="p45676910"></a>x-obs-acl</p>
</td>
<td class="cellrowborder" valign="top" width="59.17591759175917%" headers="mcps1.2.4.1.2 "><p id="p8842242"><a name="p8842242"></a><a name="p8842242"></a>通过canned ACL的方式来设置桶的ACL。</p>
<p id="p45132965"><a name="p45132965"></a><a name="p45132965"></a>取值范围：private | public-read | public-read-write | public-read-delivered | public-read-write-delivered | bucket-owner-full-control</p>
<p id="p12471314"><a name="p12471314"></a><a name="p12471314"></a>类型：字符串</p>
</td>
<td class="cellrowborder" valign="top" width="24.462446244624463%" headers="mcps1.2.4.1.3 "><p id="p31891586"><a name="p31891586"></a><a name="p31891586"></a>否</p>
</td>
</tr>
</tbody>
</table>

## 请求消息元素<a name="section36295384"></a>

更改桶的ACL请求需要在消息元素中带上ACL信息，元素的具体含义如[表3](构造请求.md#table25197309)所示。

**表 2**  附加请求消息元素

<a name="table62369028"></a>
<table><thead align="left"><tr id="row29679703"><th class="cellrowborder" valign="top" width="35.709999999999994%" id="mcps1.2.4.1.1"><p id="p55245705"><a name="p55245705"></a><a name="p55245705"></a><strong id="b27449303"><a name="b27449303"></a><a name="b27449303"></a>元素名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="42.86%" id="mcps1.2.4.1.2"><p id="p8801047"><a name="p8801047"></a><a name="p8801047"></a><strong id="b12100564"><a name="b12100564"></a><a name="b12100564"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="21.43%" id="mcps1.2.4.1.3"><p id="p40621628"><a name="p40621628"></a><a name="p40621628"></a><strong id="b30050337"><a name="b30050337"></a><a name="b30050337"></a>是否必选</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row18158267"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p61533550"><a name="p61533550"></a><a name="p61533550"></a>Owner</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p18161633"><a name="p18161633"></a><a name="p18161633"></a>桶的所有者信息，包含ID。</p>
<p id="p29236970"><a name="p29236970"></a><a name="p29236970"></a>类型：XML。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p19384352"><a name="p19384352"></a><a name="p19384352"></a>否</p>
</td>
</tr>
<tr id="row40241448"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p38331852"><a name="p38331852"></a><a name="p38331852"></a>ID</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p17872337"><a name="p17872337"></a><a name="p17872337"></a>被授权用户的租户Id。</p>
<p id="p26633311"><a name="p26633311"></a><a name="p26633311"></a>类型：字符串。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p9814616"><a name="p9814616"></a><a name="p9814616"></a>否</p>
</td>
</tr>
<tr id="row12128409"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p42877090"><a name="p42877090"></a><a name="p42877090"></a>Grant</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p50492235"><a name="p50492235"></a><a name="p50492235"></a>用于标记用户及用户的权限。</p>
<p id="p51776931"><a name="p51776931"></a><a name="p51776931"></a>类型：XML。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p33181855"><a name="p33181855"></a><a name="p33181855"></a>否</p>
</td>
</tr>
<tr id="row30201246"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p30381848"><a name="p30381848"></a><a name="p30381848"></a>Grantee</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p45010643"><a name="p45010643"></a><a name="p45010643"></a>记录用户信息。</p>
<p id="p21983479"><a name="p21983479"></a><a name="p21983479"></a>类型：XML。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p35831338"><a name="p35831338"></a><a name="p35831338"></a>否</p>
</td>
</tr>
<tr id="row57331916125210"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p373461620527"><a name="p373461620527"></a><a name="p373461620527"></a>Canned</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p916103775218"><a name="p916103775218"></a><a name="p916103775218"></a>向所有人授予权限。</p>
<p id="p121544984412"><a name="p121544984412"></a><a name="p121544984412"></a>取值范围：Everyone</p>
<p id="p19164637145219"><a name="p19164637145219"></a><a name="p19164637145219"></a>类型：枚举类型。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p17361816115214"><a name="p17361816115214"></a><a name="p17361816115214"></a>否</p>
</td>
</tr>
<tr id="row181794203527"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p1517952017528"><a name="p1517952017528"></a><a name="p1517952017528"></a>Delivered</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p417902025215"><a name="p417902025215"></a><a name="p417902025215"></a>桶的ACL是否向桶内对象传递。</p>
<p id="p4656194515534"><a name="p4656194515534"></a><a name="p4656194515534"></a>类型：布尔类型。默认false。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p517912209528"><a name="p517912209528"></a><a name="p517912209528"></a>否</p>
</td>
</tr>
<tr id="row54046594"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p15698002"><a name="p15698002"></a><a name="p15698002"></a>Permission</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p63578630"><a name="p63578630"></a><a name="p63578630"></a>授予的权限。</p>
<p id="p5666973716"><a name="p5666973716"></a><a name="p5666973716"></a>取值范围：READ | WRITE |  FULL_CONTROL</p>
<p id="p49595399"><a name="p49595399"></a><a name="p49595399"></a>类型：枚举类型。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p57804348"><a name="p57804348"></a><a name="p57804348"></a>否</p>
</td>
</tr>
<tr id="row50477085"><td class="cellrowborder" valign="top" width="35.709999999999994%" headers="mcps1.2.4.1.1 "><p id="p62112124"><a name="p62112124"></a><a name="p62112124"></a>AccessControlList</p>
</td>
<td class="cellrowborder" valign="top" width="42.86%" headers="mcps1.2.4.1.2 "><p id="p65026180"><a name="p65026180"></a><a name="p65026180"></a>访问控制列表，包含Grant、 Grantee、Permission三个元素。</p>
<p id="p48364710"><a name="p48364710"></a><a name="p48364710"></a>类型：XML。</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.4.1.3 "><p id="p25227453"><a name="p25227453"></a><a name="p25227453"></a>否</p>
</td>
</tr>
</tbody>
</table>

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

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF2600000164361F2954B4D063164704
x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT78HTIBuhe0FbtSptrb/akwELtwyPKs
Date: WED, 01 Jul 2015 02:37:22 GMT
Content-Length: 0
```

