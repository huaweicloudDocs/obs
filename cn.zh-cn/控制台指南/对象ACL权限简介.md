# 对象ACL权限简介<a name="zh-cn_topic_0066088967"></a>

OBS提供基于账号的ACL，桶的拥有者可以通过ACL授予其他账号的访问权限，例如对象的读取权限，ACL的读取权限、写入权限。

所有的桶和对象在默认情况下，仅允许桶的拥有者访问桶内的对象。一个账号下的所有用户默认拥有相同的权限，也可以通过桶策略为同一账号下不同用户设置不同的权限。桶ACL只能对账号授权，桶策略可以对账号或者账号下的用户授权。

如果同时配置桶ACL和对象ACL且两者的授权判定产生冲突时，以对象ACL\>桶ACL的优先级顺序决定授权结果。

OBS支持通过ACL对如下授权用户授予访问对象的指定权限，如[表1](#table23236845)所示：

**表 1**  OBS支持的被授权用户

<a name="table23236845"></a>
<table><thead align="left"><tr id="zh-cn_topic_0071293615_row16039151"><th class="cellrowborder" valign="top" width="27%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0071293615_p24102815"><a name="zh-cn_topic_0071293615_p24102815"></a><a name="zh-cn_topic_0071293615_p24102815"></a>被授权用户</p>
</th>
<th class="cellrowborder" valign="top" width="73%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0071293615_p6170971"><a name="zh-cn_topic_0071293615_p6170971"></a><a name="zh-cn_topic_0071293615_p6170971"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0071293615_row30086668"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="afa5f090756de44f6b9b0507e885e6b77"><a name="afa5f090756de44f6b9b0507e885e6b77"></a><a name="afa5f090756de44f6b9b0507e885e6b77"></a>拥有者</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0071293615_p31466092"><a name="zh-cn_topic_0071293615_p31466092"></a><a name="zh-cn_topic_0071293615_p31466092"></a>拥有者是指对象的创建者的账号，默认永远具有ACL的读取和写入这两种权限。</p>
</td>
</tr>
<tr id="r30eade55e6e646dc8fe1c64ab67e6382"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="a8bbaeefc421f4773ae9282e48768170e"><a name="a8bbaeefc421f4773ae9282e48768170e"></a><a name="a8bbaeefc421f4773ae9282e48768170e"></a>匿名用户</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="a4cf47ba94b5f476e91dc55c0c1c4d46b"><a name="a4cf47ba94b5f476e91dc55c0c1c4d46b"></a><a name="a4cf47ba94b5f476e91dc55c0c1c4d46b"></a>未注册OBS的普通访客。如果匿名用户被授予了访问对象的权限，则表示所有人都可以访问对应的对象。</p>
</td>
</tr>
<tr id="zh-cn_topic_0071293615_row14759379"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0071293615_p54659014"><a name="zh-cn_topic_0071293615_p54659014"></a><a name="zh-cn_topic_0071293615_p54659014"></a>注册用户组</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0071293615_p65304051"><a name="zh-cn_topic_0071293615_p65304051"></a><a name="zh-cn_topic_0071293615_p65304051"></a>注册OBS的用户。例如，注册用户可以通过AK/SK访问OBS客户端。</p>
</td>
</tr>
<tr id="zh-cn_topic_0071293615_row59256928"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0071293615_p35081826"><a name="zh-cn_topic_0071293615_p35081826"></a><a name="zh-cn_topic_0071293615_p35081826"></a>特定用户</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0071293615_p23055673"><a name="zh-cn_topic_0071293615_p23055673"></a><a name="zh-cn_topic_0071293615_p23055673"></a>具有访问桶的权限的账号。桶的拥有者通过账号ID或账号名配置此权限。</p>
</td>
</tr>
</tbody>
</table>

针对对象，OBS当前支持如下访问权限，如[表2](#table28226836)所示：

**表 2**  OBS支持的访问权限

<a name="table28226836"></a>
<table><thead align="left"><tr id="zh-cn_topic_0071293615_row61083978"><th class="cellrowborder" valign="top" width="19.55%" id="mcps1.2.4.1.1"><p id="p3671603217261"><a name="p3671603217261"></a><a name="p3671603217261"></a>权限</p>
</th>
<th class="cellrowborder" valign="top" width="14.97%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0071293615_p48855171"><a name="zh-cn_topic_0071293615_p48855171"></a><a name="zh-cn_topic_0071293615_p48855171"></a>选项</p>
</th>
<th class="cellrowborder" valign="top" width="65.48%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0071293615_p64954777"><a name="zh-cn_topic_0071293615_p64954777"></a><a name="zh-cn_topic_0071293615_p64954777"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0071293615_row26845555"><td class="cellrowborder" valign="top" width="19.55%" headers="mcps1.2.4.1.1 "><p id="p2120863117261"><a name="p2120863117261"></a><a name="p2120863117261"></a>对象访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.97%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0071293615_p27006329"><a name="zh-cn_topic_0071293615_p27006329"></a><a name="zh-cn_topic_0071293615_p27006329"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="65.48%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0071293615_p40029077"><a name="zh-cn_topic_0071293615_p40029077"></a><a name="zh-cn_topic_0071293615_p40029077"></a>此权限可以获取该对象内容和元数据。</p>
</td>
</tr>
<tr id="zh-cn_topic_0071293615_row35565678"><td class="cellrowborder" rowspan="2" valign="top" width="19.55%" headers="mcps1.2.4.1.1 "><p id="p3315846717261"><a name="p3315846717261"></a><a name="p3315846717261"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.97%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0071293615_p62247688"><a name="zh-cn_topic_0071293615_p62247688"></a><a name="zh-cn_topic_0071293615_p62247688"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="65.48%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0071293615_p8897958"><a name="zh-cn_topic_0071293615_p8897958"></a><a name="zh-cn_topic_0071293615_p8897958"></a>此权限可以获取对应的对象的权限控制列表。</p>
<p id="zh-cn_topic_0071293615_p12972762"><a name="zh-cn_topic_0071293615_p12972762"></a><a name="zh-cn_topic_0071293615_p12972762"></a>对象的拥有者默认永远具有ACL的读取权限</p>
</td>
</tr>
<tr id="zh-cn_topic_0071293615_row49646001"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0071293615_p61903120"><a name="zh-cn_topic_0071293615_p61903120"></a><a name="zh-cn_topic_0071293615_p61903120"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0071293615_p48096812"><a name="zh-cn_topic_0071293615_p48096812"></a><a name="zh-cn_topic_0071293615_p48096812"></a>此权限可以更新对象的权限控制列表。</p>
<p id="zh-cn_topic_0071293615_p30218124"><a name="zh-cn_topic_0071293615_p30218124"></a><a name="zh-cn_topic_0071293615_p30218124"></a>对象的拥有者默认永远具有ACL的写入权限。</p>
</td>
</tr>
</tbody>
</table>

>![](public_sys-resources/icon-note.gif) **说明：**   
>每一次对对象的授权操作都将覆盖对象已有的权限列表，而不会对其新增权限。  

## 对象ACL使用场景<a name="section41561114217"></a>

在以下场景，我们建议您使用对象ACL。

-   需要对象级的访问权限控制时。桶策略可以授予对象或对象集访问权限，当授予一个对象集权限后，想对对象集中某一个对象再进行单独授权，通过配置桶策略的方法显然不太实际。此时建议使用对象ACL，使得单个对象的权限控制更加方便。
-   使用对象链接访问对象时。一般使用对象ACL，将某一个对象通过对象链接开放给匿名用户进行读取操作。

## 对象ACL和桶访问权限的冲突判定准则<a name="section1915916141114"></a>

如果同时配置桶ACL和对象ACL且两者的授权判定产生冲突时，以对象ACL\>桶ACL的优先级顺序决定授权结果。如果同时还配置有桶策略，当桶策略中定义的对象访问权限与对象ACL配置的访问权限冲突时，遵循桶策略中的Deny优先原则。

## 对象ACL和桶策略的映射关系<a name="section816016146119"></a>

对象ACL主要用于授予对象基本的读写权限。桶策略高级设置中支持更多在对象上可以执行的动作（请参见动作和条件的消息解释）。对象ACL访问权限和桶策略动作的映射关系如下表所示。

<a name="table4160714016"></a>
<table><thead align="left"><tr id="row122474141815"><th class="cellrowborder" valign="top" width="19.388061193880613%" id="mcps1.1.4.1.1"><p id="p92471614310"><a name="p92471614310"></a><a name="p92471614310"></a>对象ACL权限</p>
</th>
<th class="cellrowborder" valign="top" width="14.288571142885711%" id="mcps1.1.4.1.2"><p id="p1024713142118"><a name="p1024713142118"></a><a name="p1024713142118"></a>选项</p>
</th>
<th class="cellrowborder" valign="top" width="66.32336766323368%" id="mcps1.1.4.1.3"><p id="p62479146116"><a name="p62479146116"></a><a name="p62479146116"></a>对应桶策略高级设置中的动作</p>
</th>
</tr>
</thead>
<tbody><tr id="row1724718148112"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.1.4.1.1 "><p id="p102479141019"><a name="p102479141019"></a><a name="p102479141019"></a>对象访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.288571142885711%" headers="mcps1.1.4.1.2 "><p id="p724781411118"><a name="p724781411118"></a><a name="p724781411118"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.32336766323368%" headers="mcps1.1.4.1.3 "><a name="ul1424715141914"></a><a name="ul1424715141914"></a><ul id="ul1424715141914"><li>GetObject</li><li>GetObjectVersion</li></ul>
</td>
</tr>
<tr id="row12247101419112"><td class="cellrowborder" rowspan="2" valign="top" width="19.388061193880613%" headers="mcps1.1.4.1.1 "><p id="p62471514814"><a name="p62471514814"></a><a name="p62471514814"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.288571142885711%" headers="mcps1.1.4.1.2 "><p id="p72471314311"><a name="p72471314311"></a><a name="p72471314311"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.32336766323368%" headers="mcps1.1.4.1.3 "><a name="ul324718149119"></a><a name="ul324718149119"></a><ul id="ul324718149119"><li>GetObjectAcl</li><li>GetObjectVersionAcl</li></ul>
</td>
</tr>
<tr id="row122478141116"><td class="cellrowborder" valign="top" headers="mcps1.1.4.1.1 "><p id="p8247614513"><a name="p8247614513"></a><a name="p8247614513"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.1.4.1.2 "><a name="ul122471014113"></a><a name="ul122471014113"></a><ul id="ul122471014113"><li>PutObjectAcl</li><li>PutObjectVersionAcl</li></ul>
</td>
</tr>
</tbody>
</table>

