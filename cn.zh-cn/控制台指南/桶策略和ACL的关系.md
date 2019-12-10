# 桶策略和ACL的关系<a name="zh-cn_topic_0066088967"></a>

## 桶ACL和桶策略的映射关系<a name="section9370125413594"></a>

桶ACL用于授予桶基本的读写权限，桶策略高级设置中支持更多在桶上可以执行的动作。桶策略是对桶ACL的补充，除了限定的只能由桶ACL授予日志投递用户组权限外，更多时候桶策略可以替代桶ACL管理桶的访问权限。桶ACL访问权限和桶策略动作的映射关系如[表1](#table183716545593)所示。

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
<td class="cellrowborder" valign="top" width="66.66666666666667%" headers="mcps1.2.4.1.3 "><a name="ul1242814546590"></a><a name="ul1242814546590"></a><ul id="ul1242814546590"><li>HeadBucket</li><li>ListBucket</li><li>ListBucketVersions</li><li>ListBucketMultipartUploads</li></ul>
</td>
</tr>
<tr id="row1242885414593"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p134281454115913"><a name="p134281454115913"></a><a name="p134281454115913"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><a name="ul84281154125913"></a><a name="ul84281154125913"></a><ul id="ul84281154125913"><li>PutObject</li><li>DeleteObject</li><li>DeleteObjectVersion</li></ul>
</td>
</tr>
<tr id="row17428135413591"><td class="cellrowborder" rowspan="2" valign="top" width="19.191919191919194%" headers="mcps1.2.4.1.1 "><p id="p174281154105920"><a name="p174281154105920"></a><a name="p174281154105920"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.141414141414144%" headers="mcps1.2.4.1.2 "><p id="p1142885415597"><a name="p1142885415597"></a><a name="p1142885415597"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.66666666666667%" headers="mcps1.2.4.1.3 "><p id="p1842815542599"><a name="p1842815542599"></a><a name="p1842815542599"></a>GetBucketAcl</p>
</td>
</tr>
<tr id="row15428654125911"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1742825465912"><a name="p1742825465912"></a><a name="p1742825465912"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p2429554125918"><a name="p2429554125918"></a><a name="p2429554125918"></a>PutBucketAcl</p>
</td>
</tr>
</tbody>
</table>

## 对象ACL和桶策略的映射关系<a name="section816016146119"></a>

对象ACL用于授予对象基本的读写权限。桶策略高级设置中支持更多在对象上可以执行的动作。对象ACL访问权限和桶策略动作的映射关系如[表2](#table4160714016)所示。

**表 2**  对象ACL和桶策略的映射关系

<a name="table4160714016"></a>
<table><thead align="left"><tr id="row122474141815"><th class="cellrowborder" valign="top" width="19.388061193880613%" id="mcps1.2.4.1.1"><p id="p92471614310"><a name="p92471614310"></a><a name="p92471614310"></a>对象ACL权限</p>
</th>
<th class="cellrowborder" valign="top" width="14.288571142885711%" id="mcps1.2.4.1.2"><p id="p1024713142118"><a name="p1024713142118"></a><a name="p1024713142118"></a>选项</p>
</th>
<th class="cellrowborder" valign="top" width="66.32336766323368%" id="mcps1.2.4.1.3"><p id="p62479146116"><a name="p62479146116"></a><a name="p62479146116"></a>对应桶策略高级设置中的动作</p>
</th>
</tr>
</thead>
<tbody><tr id="row1724718148112"><td class="cellrowborder" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p102479141019"><a name="p102479141019"></a><a name="p102479141019"></a>对象访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.288571142885711%" headers="mcps1.2.4.1.2 "><p id="p724781411118"><a name="p724781411118"></a><a name="p724781411118"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.32336766323368%" headers="mcps1.2.4.1.3 "><a name="ul1424715141914"></a><a name="ul1424715141914"></a><ul id="ul1424715141914"><li>GetObject</li><li>GetObjectVersion</li></ul>
</td>
</tr>
<tr id="row12247101419112"><td class="cellrowborder" rowspan="2" valign="top" width="19.388061193880613%" headers="mcps1.2.4.1.1 "><p id="p62471514814"><a name="p62471514814"></a><a name="p62471514814"></a>ACL访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="14.288571142885711%" headers="mcps1.2.4.1.2 "><p id="p72471314311"><a name="p72471314311"></a><a name="p72471314311"></a>读取权限</p>
</td>
<td class="cellrowborder" valign="top" width="66.32336766323368%" headers="mcps1.2.4.1.3 "><a name="ul324718149119"></a><a name="ul324718149119"></a><ul id="ul324718149119"><li>GetObjectAcl</li><li>GetObjectVersionAcl</li></ul>
</td>
</tr>
<tr id="row122478141116"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p8247614513"><a name="p8247614513"></a><a name="p8247614513"></a>写入权限</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><a name="ul122471014113"></a><a name="ul122471014113"></a><ul id="ul122471014113"><li>PutObjectAcl</li><li>PutObjectVersionAcl</li></ul>
</td>
</tr>
</tbody>
</table>

