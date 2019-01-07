# 桶ACL和桶策略的关系<a name="zh-cn_topic_0066037836"></a>

如果桶ACL和桶策略同时使用且两者的授权判定产生冲突时，以桶策略\>桶ACL的优先级顺序决定授权结果。

桶ACL只能对账号授权，桶策略可以对账号或者账号下的用户授权。

## 桶ACL和桶策略的映射关系<a name="section9370125413594"></a>

桶ACL主要用于授予桶基本的读写权限。桶策略高级设置中支持更多在桶上可以执行的动作（请参见[桶策略动作](桶策略动作.md)）。桶策略是对桶ACL的补充，除了限定的只能由桶ACL授予日志投递用户组权限外，更多时候桶策略可以替代桶ACL管理桶的访问权限。桶ACL访问权限和桶策略动作的映射关系如[表1](#table183716545593)所示。

**表 1**  桶ACL和桶策略的映射关系

<a name="table183716545593"></a>
<table><thead align="left"><tr id="row10426205416593"><th class="cellrowborder" valign="top" width="19.191919191919194%" id="mcps1.2.4.1.1"><p id="p6426165418599"><a name="p6426165418599"></a><a name="p6426165418599"></a>ACL权限</p>
</th>
<th class="cellrowborder" valign="top" width="14.141414141414144%" id="mcps1.2.4.1.2"><p id="p1842615544595"><a name="p1842615544595"></a><a name="p1842615544595"></a>选项</p>
</th>
<th class="cellrowborder" valign="top" width="66.66666666666667%" id="mcps1.2.4.1.3"><p id="p8428125435912"><a name="p8428125435912"></a><a name="p8428125435912"></a>对应桶策略高级设置中的动作</p>
</th>
</tr>
</thead>
<tbody><tr id="row942885416596"><td class="cellrowborder" rowspan="2" valign="top" width="19.191919191919194%" headers="mcps1.2.4.1.1 "><p id="p184281354195919"><a name="p184281354195919"></a><a name="p184281354195919"></a>桶访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.141414141414144%" headers="mcps1.2.4.1.2 "><p id="p54287547598"><a name="p54287547598"></a><a name="p54287547598"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.66666666666667%" headers="mcps1.2.4.1.3 "><a name="ul1242814546590"></a><a name="ul1242814546590"></a><ul id="ul1242814546590"><li>HeadBucket（判断桶是否存在）</li><li>ListBucket（列举桶内对象，获取桶元数据）</li><li>ListBucketVersions（列举桶内多版本对象）</li><li>ListBucketMultipartUploads（列举多段上传任务）</li></ul>
</td>
</tr>
<tr id="row1242885414593"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p134281454115913"><a name="p134281454115913"></a><a name="p134281454115913"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><a name="ul84281154125913"></a><a name="ul84281154125913"></a><ul id="ul84281154125913"><li>PutObject（PUT上传，POST上传，上传段，初始化上传段任务，合并段）</li><li>DeleteObject（删除对象）</li><li>DeleteObjectVersion（删除特定版本的对象）</li></ul>
</td>
</tr>
<tr id="row17428135413591"><td class="cellrowborder" rowspan="2" valign="top" width="19.191919191919194%" headers="mcps1.2.4.1.1 "><p id="p174281154105920"><a name="p174281154105920"></a><a name="p174281154105920"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.141414141414144%" headers="mcps1.2.4.1.2 "><p id="p1142885415597"><a name="p1142885415597"></a><a name="p1142885415597"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.66666666666667%" headers="mcps1.2.4.1.3 "><p id="p1842815542599"><a name="p1842815542599"></a><a name="p1842815542599"></a>GetBucketAcl（获取桶ACL的相关信息）</p>
</td>
</tr>
<tr id="row15428654125911"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1742825465912"><a name="p1742825465912"></a><a name="p1742825465912"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p2429554125918"><a name="p2429554125918"></a><a name="p2429554125918"></a>PutBucketAcl（设置桶ACL）</p>
</td>
</tr>
</tbody>
</table>

## 桶ACL和桶策略的冲突判断<a name="section06951081503"></a>

桶ACL和桶策略冲突主要体现在桶ACL中设置了权限，但在桶策略中限制了此权限。例如，桶ACL中为账号B设置了桶读取权限，桶策略中设置拒绝账号B对桶执行ListBucket（获取桶内对象）操作，最终判断结果将表现为账号B无法执行ListBucket操作。

如果桶ACL和桶策略同时使用且两者的授权判定产生冲突时，以桶策略优先作为授权判断标准。

