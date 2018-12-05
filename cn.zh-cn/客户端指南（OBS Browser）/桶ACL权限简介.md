# 桶ACL权限简介<a name="zh-cn_topic_0086375574"></a>

OBS支持通过ACL对如下授权用户授予访问桶的指定权限，如[表1](#zh-cn_topic_0075617858_table23236845)所示。

**表 1**  OBS支持的被授权用户

<a name="zh-cn_topic_0075617858_table23236845"></a>
<table><thead align="left"><tr id="zh-cn_topic_0075617858_row16039151"><th class="cellrowborder" valign="top" width="27%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0075617858_p24102815"><a name="zh-cn_topic_0075617858_p24102815"></a><a name="zh-cn_topic_0075617858_p24102815"></a>被授权用户</p>
</th>
<th class="cellrowborder" valign="top" width="73%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0075617858_p6170971"><a name="zh-cn_topic_0075617858_p6170971"></a><a name="zh-cn_topic_0075617858_p6170971"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0075617858_row30086668"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0075617858_p21101082"><a name="zh-cn_topic_0075617858_p21101082"></a><a name="zh-cn_topic_0075617858_p21101082"></a>桶的拥有者</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p82371758102019"><a name="p82371758102019"></a><a name="p82371758102019"></a>拥有者是指创建桶的账户。桶拥有者默认拥有所有的桶访问权限，其中桶ACL的读取和写入这两种权限永远拥有，且不支持修改。</p>
<div class="note" id="note1556018562260"><a name="note1556018562260"></a><a name="note1556018562260"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="zh-cn_topic_0129289302_p8237175842016"><a name="zh-cn_topic_0129289302_p8237175842016"></a><a name="zh-cn_topic_0129289302_p8237175842016"></a>去掉桶读取权限和桶写入权限将导致用户无法执行获取桶内对象列表、在桶中上传对象等基本操作，为正常使用OBS，不建议修改桶拥有者的权限。</p>
</div></div>
</td>
</tr>
<tr id="r3060af3019e342fbbf3b4ed1eb5339a0"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="af072ea7a0c77448c92aa60b55822c0a0"><a name="af072ea7a0c77448c92aa60b55822c0a0"></a><a name="af072ea7a0c77448c92aa60b55822c0a0"></a>匿名用户</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p112397589206"><a name="p112397589206"></a><a name="p112397589206"></a>未注册华为云云服务的普通访客。如果匿名用户被授予了访问桶的权限，则表示所有人都可以访问对应的桶，并且不需要经过任何身份认证。</p>
<div class="notice" id="note1437509296"><a name="note1437509296"></a><a name="note1437509296"></a><span class="noticetitle"> 注意： </span><div class="noticebody"><p id="zh-cn_topic_0129289302_p122391580206"><a name="zh-cn_topic_0129289302_p122391580206"></a><a name="zh-cn_topic_0129289302_p122391580206"></a>开启匿名用户的桶访问权限后，所有人都可以在不经过身份认证的情况下，对桶进行访问。为安全起见，不建议通过桶ACL为匿名用户设置桶的访问权限。</p>
</div></div>
</td>
</tr>
<tr id="zh-cn_topic_0075617858_row14759379"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0075617858_p54659014"><a name="zh-cn_topic_0075617858_p54659014"></a><a name="zh-cn_topic_0075617858_p54659014"></a>注册用户组</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p6239185816209"><a name="p6239185816209"></a><a name="p6239185816209"></a>注册用户组代表所有注册了华为云云服务的账号（仅指账号，不包括通过IAM创建的用户组或用户）。注册用户必须要经过身份认证（目前主要通过AK/SK进行身份认证），才可以获取对应的访问权限。例如，当注册用户组被授予桶写入权限后，世界上任何已通过身份验证的华为云云服务账号，都可以向您的桶上传、覆盖和删除对象。</p>
</td>
</tr>
<tr id="zh-cn_topic_0075617858_row35559643"><td class="cellrowborder" valign="top" width="27%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0075617858_p61758841"><a name="zh-cn_topic_0075617858_p61758841"></a><a name="zh-cn_topic_0075617858_p61758841"></a>日志投递用户组</p>
</td>
<td class="cellrowborder" valign="top" width="73%" headers="mcps1.2.3.1.2 "><p id="p11239175822012"><a name="p11239175822012"></a><a name="p11239175822012"></a>日志投递用户组用于投递OBS桶及对象的访问日志。由于OBS本身不能在账户的桶中创建或上传任何文件，因此在需要为桶记录访问日志时，只能由账户授予日志投递用户组一定权限后，OBS才能将访问日志写入指定的日志存储桶中。该用户组仅用于OBS内部的日志记录。</p>
<div class="notice" id="note71171158122010"><a name="note71171158122010"></a><a name="note71171158122010"></a><span class="noticetitle"> 注意： </span><div class="noticebody"><p id="zh-cn_topic_0129289302_p7241158152013"><a name="zh-cn_topic_0129289302_p7241158152013"></a><a name="zh-cn_topic_0129289302_p7241158152013"></a>当日志记录开启后，目标存储桶的日志投递用户组会同步开启桶的写入权限和ACL读取权限。若手动将日志投递用户组的桶写入权限和ACL读取权限关闭，桶的日志记录会失败。</p>
</div></div>
</td>
</tr>
</tbody>
</table>

针对桶，OBS当前支持五种访问权限，如[表2](#tc594413d8d3240d2832dbf714ae030f7)所示。

**表 2**  OBS支持的访问权限

<a name="tc594413d8d3240d2832dbf714ae030f7"></a>
<table><thead align="left"><tr id="zh-cn_topic_0129289302_row61083978"><th class="cellrowborder" valign="top" width="19.55%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0129289302_p55592582172343"><a name="zh-cn_topic_0129289302_p55592582172343"></a><a name="zh-cn_topic_0129289302_p55592582172343"></a>权限</p>
</th>
<th class="cellrowborder" valign="top" width="14.97%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0129289302_p48855171"><a name="zh-cn_topic_0129289302_p48855171"></a><a name="zh-cn_topic_0129289302_p48855171"></a>选项</p>
</th>
<th class="cellrowborder" valign="top" width="65.48%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0129289302_p64954777"><a name="zh-cn_topic_0129289302_p64954777"></a><a name="zh-cn_topic_0129289302_p64954777"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0129289302_row26845555"><td class="cellrowborder" rowspan="2" valign="top" width="19.55%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0129289302_p6705326172343"><a name="zh-cn_topic_0129289302_p6705326172343"></a><a name="zh-cn_topic_0129289302_p6705326172343"></a>桶访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.97%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0129289302_p27006329"><a name="zh-cn_topic_0129289302_p27006329"></a><a name="zh-cn_topic_0129289302_p27006329"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="65.48%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0129289302_p40029077"><a name="zh-cn_topic_0129289302_p40029077"></a><a name="zh-cn_topic_0129289302_p40029077"></a>此权限可以获取该桶内对象列表和桶的元数据。</p>
</td>
</tr>
<tr id="zh-cn_topic_0129289302_row21129772"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0129289302_p33789992"><a name="zh-cn_topic_0129289302_p33789992"></a><a name="zh-cn_topic_0129289302_p33789992"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0129289302_p52634865"><a name="zh-cn_topic_0129289302_p52634865"></a><a name="zh-cn_topic_0129289302_p52634865"></a>此权限可以上传、覆盖和删除该桶内任何对象。</p>
</td>
</tr>
<tr id="zh-cn_topic_0129289302_row35565678"><td class="cellrowborder" rowspan="2" valign="top" width="19.55%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0129289302_p46542350172415"><a name="zh-cn_topic_0129289302_p46542350172415"></a><a name="zh-cn_topic_0129289302_p46542350172415"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.97%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0129289302_p62247688"><a name="zh-cn_topic_0129289302_p62247688"></a><a name="zh-cn_topic_0129289302_p62247688"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="65.48%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0129289302_p8897958"><a name="zh-cn_topic_0129289302_p8897958"></a><a name="zh-cn_topic_0129289302_p8897958"></a>此权限可以获取对应的桶的权限控制列表。</p>
<p id="zh-cn_topic_0129289302_p12972762"><a name="zh-cn_topic_0129289302_p12972762"></a><a name="zh-cn_topic_0129289302_p12972762"></a>桶的拥有者默认永远具有ACL的读取权限。</p>
</td>
</tr>
<tr id="zh-cn_topic_0129289302_row49646001"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0129289302_p61903120"><a name="zh-cn_topic_0129289302_p61903120"></a><a name="zh-cn_topic_0129289302_p61903120"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0129289302_p48096812"><a name="zh-cn_topic_0129289302_p48096812"></a><a name="zh-cn_topic_0129289302_p48096812"></a>此权限可以更新对应桶的权限控制列表。</p>
<p id="zh-cn_topic_0129289302_p30218124"><a name="zh-cn_topic_0129289302_p30218124"></a><a name="zh-cn_topic_0129289302_p30218124"></a>桶的拥有者默认永远具有ACL的写入权限。</p>
</td>
</tr>
</tbody>
</table>

>![](public_sys-resources/icon-note.gif) **说明：**   
>每一次对桶的授权操作都将覆盖桶或对象已有的权限列表，而不会对其新增权限。  

