# 桶ACL和对象ACL<a name="zh-cn_topic_0045829069"></a>

访问控制列表（Access Control List，ACL）是一个指定被授权者和所授予权限的授权列表。

OBS桶和对象的ACL是基于账号的访问控制，默认情况下，创建桶和对象时会同步创建ACL，授权拥有者对桶和对象资源的完全控制权限。

OBS  ACL是基于账号级别的读写权限控制，权限控制细粒度不如桶策略和IAM权限。一般情况下，建议使用IAM权限和桶策略进行访问控制。

OBS支持通过ACL对[表1](#table177445813209)所示用户或用户组授予桶的访问权限。

**表 1** OBS支持的被授权用户

<a name="table177445813209"></a>
<table><thead align="left"><tr id="row5236185882019"><th class="cellrowborder" valign="top" width="27%" id="mcps1.2.3.1.1"><p id="p4236185812209"><a name="p4236185812209"></a><a name="p4236185812209"></a>被授权用户</p>
</th>
<th class="cellrowborder" valign="top" width="73%" id="mcps1.2.3.1.2"><p id="p0236185811200"><a name="p0236185811200"></a><a name="p0236185811200"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row122361958192016"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="p1223615586209"><a name="p1223615586209"></a><a name="p1223615586209"></a>特定用户</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p1377083924318"><a name="p1377083924318"></a><a name="p1377083924318"></a>ACL支持通过账号授予桶/对象的访问权限。授予账号权限后，账号下所有具有<span id="ph6770113934313"><a name="ph6770113934313"></a><a name="ph6770113934313"></a>OBS</span>资源权限的IAM用户都可以拥有此桶/对象的访问权限。</p>
<p id="p223612587202"><a name="p223612587202"></a><a name="p223612587202"></a>当需要为不同IAM用户授予不同的权限时，可以通过桶策略配置，具体操作请参见<a href="桶拥有者为IAM用户授予桶权限.md">桶拥有者为IAM用户授予桶权限</a>。</p>
</td>
</tr>
<tr id="row14236115815207"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="p4237195812018"><a name="p4237195812018"></a><a name="p4237195812018"></a>拥有者</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p82371758102019"><a name="p82371758102019"></a><a name="p82371758102019"></a>桶的拥有者是指创建桶的账号。桶拥有者默认拥有所有的桶访问权限，其中桶ACL的读取和写入这两种权限永远拥有，且不支持修改。</p>
<p id="p108801457143318"><a name="p108801457143318"></a><a name="p108801457143318"></a>对象的拥有者是上传对象的账号，而不是对象所属的桶的拥有者。对象拥有者默认永远拥有对象读取权限、ACL的读取和写入权限，且不支持修改。</p>
<div class="notice" id="note16704211185110"><a name="note16704211185110"></a><a name="note16704211185110"></a><span class="noticetitle"> 须知： </span><div class="noticebody"><p id="p11704131114517"><a name="p11704131114517"></a><a name="p11704131114517"></a>不建议修改桶拥有者的对桶读取和写入权限。</p>
</div></div>
</td>
</tr>
<tr id="row0239105872015"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="p2239658142016"><a name="p2239658142016"></a><a name="p2239658142016"></a>匿名用户</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p112397589206"><a name="p112397589206"></a><a name="p112397589206"></a>未注册云服务的普通访客。如果匿名用户被授予了访问桶/对象的权限，则表示所有人都可以访问对应的桶/对象，并且不需要经过任何身份认证。</p>
<div class="notice" id="note1437509296"><a name="note1437509296"></a><a name="note1437509296"></a><span class="noticetitle"> 须知： </span><div class="noticebody"><p id="p122391580206"><a name="p122391580206"></a><a name="p122391580206"></a>开启匿名用户的桶/对象访问权限后，所有人都可以在不经过身份认证的情况下，对桶/对象进行访问。</p>
</div></div>
</td>
</tr>
<tr id="row112391958122020"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="p1123911582207"><a name="p1123911582207"></a><a name="p1123911582207"></a>注册用户组</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p6239185816209"><a name="p6239185816209"></a><a name="p6239185816209"></a>注册用户组代表所有注册了云服务的账号（仅指账号，不包括通过IAM创建的用户组或用户）。注册用户必须要经过身份认证（目前主要通过AK/SK进行身份认证），才可以获取对应的访问权限。例如，当注册用户组被授予桶写入权限后，世界上任何已通过身份验证的云服务账号，都可以向您的桶上传、覆盖和删除对象。</p>
</td>
</tr>
<tr id="row1123945814203"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="p19239165817208"><a name="p19239165817208"></a><a name="p19239165817208"></a>日志投递用户组</p>
<div class="note" id="note0623203504215"><a name="note0623203504215"></a><a name="note0623203504215"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p12623113515421"><a name="p12623113515421"></a><a name="p12623113515421"></a>仅桶ACL支持。</p>
</div></div>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p11239175822012"><a name="p11239175822012"></a><a name="p11239175822012"></a>日志投递用户组用于投递<span id="ph1992164812018"><a name="ph1992164812018"></a><a name="ph1992164812018"></a>OBS</span>桶及对象的访问日志。由于<span id="ph4888162118"><a name="ph4888162118"></a><a name="ph4888162118"></a>OBS</span>本身不能在账户的桶中创建或上传任何文件，因此在需要为桶记录访问日志时，只能由账户授予日志投递用户组一定权限后，<span id="ph144717722112"><a name="ph144717722112"></a><a name="ph144717722112"></a>OBS</span>才能将访问日志写入指定的日志存储桶中。该用户组仅用于<span id="ph72025512207"><a name="ph72025512207"></a><a name="ph72025512207"></a>OBS</span>内部的日志记录。</p>
<div class="notice" id="note71171158122010"><a name="note71171158122010"></a><a name="note71171158122010"></a><span class="noticetitle"> 须知： </span><div class="noticebody"><p id="p7241158152013"><a name="p7241158152013"></a><a name="p7241158152013"></a>当日志记录开启后，目标存储桶的日志投递用户组会同步开启桶的写入权限和ACL读取权限。若手动将日志投递用户组的桶写入权限和ACL读取权限关闭，桶的日志记录会失败。</p>
</div></div>
</td>
</tr>
</tbody>
</table>

## ACL权限<a name="section1314334415429"></a>

桶ACL的访问权限如[表2](#table28226836)所示：

**表 2**  桶ACL访问权限

<a name="table28226836"></a>
<table><thead align="left"><tr id="row61083978"><th class="cellrowborder" valign="top" width="19.55%" id="mcps1.2.4.1.1"><p id="p55592582172343"><a name="p55592582172343"></a><a name="p55592582172343"></a>权限</p>
</th>
<th class="cellrowborder" valign="top" width="14.97%" id="mcps1.2.4.1.2"><p id="p48855171"><a name="p48855171"></a><a name="p48855171"></a>选项</p>
</th>
<th class="cellrowborder" valign="top" width="65.48%" id="mcps1.2.4.1.3"><p id="p64954777"><a name="p64954777"></a><a name="p64954777"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row26845555"><td class="cellrowborder" rowspan="2" valign="top" width="19.55%" headers="mcps1.2.4.1.1 "><p id="p6705326172343"><a name="p6705326172343"></a><a name="p6705326172343"></a>桶访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.97%" headers="mcps1.2.4.1.2 "><p id="p27006329"><a name="p27006329"></a><a name="p27006329"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="65.48%" headers="mcps1.2.4.1.3 "><p id="p40029077"><a name="p40029077"></a><a name="p40029077"></a>此权限可以获取该桶内对象列表和桶的元数据。</p>
</td>
</tr>
<tr id="row21129772"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p33789992"><a name="p33789992"></a><a name="p33789992"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p52634865"><a name="p52634865"></a><a name="p52634865"></a>此权限可以上传、覆盖和删除该桶内任何对象。</p>
</td>
</tr>
<tr id="row35565678"><td class="cellrowborder" rowspan="2" valign="top" width="19.55%" headers="mcps1.2.4.1.1 "><p id="p46542350172415"><a name="p46542350172415"></a><a name="p46542350172415"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.97%" headers="mcps1.2.4.1.2 "><p id="p62247688"><a name="p62247688"></a><a name="p62247688"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="65.48%" headers="mcps1.2.4.1.3 "><p id="p8897958"><a name="p8897958"></a><a name="p8897958"></a>此权限可以获取对应的桶的权限控制列表。</p>
<p id="p12972762"><a name="p12972762"></a><a name="p12972762"></a>桶的拥有者默认永远具有ACL的读取权限。</p>
</td>
</tr>
<tr id="row49646001"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p61903120"><a name="p61903120"></a><a name="p61903120"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p48096812"><a name="p48096812"></a><a name="p48096812"></a>此权限可以更新对应桶的权限控制列表。</p>
<p id="p30218124"><a name="p30218124"></a><a name="p30218124"></a>桶的拥有者默认永远具有ACL的写入权限。</p>
</td>
</tr>
</tbody>
</table>

对象ACL的访问权限如[表3](#table63381242464)所示：

**表 3**  对象ACL访问权限

<a name="table63381242464"></a>
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
>每一次对桶/对象的授权操作都将覆盖桶/对象已有的权限列表，而不会对其新增权限。  

## 桶ACL使用场景<a name="section7479813113513"></a>

在以下场景，建议您使用桶ACL：

-   授予日志投递用户组桶写入权限，用以存储桶访问请求日志。
-   授予指定账号桶读取权限和桶写入权限，用以共享桶数据或挂载外部桶。比如，账号A授予账号B桶读取权限及桶写入权限后，账号B就可以通过OBS Browser+挂载外部桶、API&SDK等方式访问到该桶。

## 对象ACL使用场景<a name="section41561114217"></a>

在以下场景，建议您使用对象ACL：

-   需要对象级的访问权限控制时。桶策略可以授予对象或对象集访问权限，当授予一个对象集权限后，想对对象集中某一个对象再进行单独授权，通过配置桶策略的方法显然不太实际。此时建议使用对象ACL，使得单个对象的权限控制更加方便。
-   使用对象链接访问对象时。一般使用对象ACL，将某一个对象通过对象链接开放给匿名用户进行读取操作。

