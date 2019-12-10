# 桶拥有者为IAM用户授予桶权限<a name="obs_03_0080"></a>

在主账号下创建一个IAM用户，IAM用户不加入任何用户组，该IAM用户没有任何权限。桶拥有者（主账号）可以通过配置桶策略授予IAM用户桶的权限。

下面示例中，主账号授予IAM用户访问桶和上传对象的权限。

## 操作步骤<a name="section13279211683"></a>

1.  在OBS管理控制台左侧导航栏选择“对象存储“。
2.  在桶列表单击待操作的桶，进入“概览”页面。
3.  在左侧导航栏，单击“访问权限控制”，进入权限管理页面。
4.  单击“桶策略\>高级桶策略”。
5.  单击“创建桶策略”，系统弹出“创建桶策略”对话框。
6.  配置如下参数，授予IAM用户访问桶的权限。

    **表 1**  授予访问桶的权限的参数配置

    <a name="table7531653104420"></a>
    <table><thead align="left"><tr id="row2532105311447"><th class="cellrowborder" valign="top" width="23.189999999999998%" id="mcps1.2.3.1.1"><p id="p16532195364414"><a name="p16532195364414"></a><a name="p16532195364414"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="76.81%" id="mcps1.2.3.1.2"><p id="p15532145310443"><a name="p15532145310443"></a><a name="p15532145310443"></a>取值</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row953216536449"><td class="cellrowborder" valign="top" width="23.189999999999998%" headers="mcps1.2.3.1.1 "><p id="p1653265344417"><a name="p1653265344417"></a><a name="p1653265344417"></a>策略模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.81%" headers="mcps1.2.3.1.2 "><p id="p95328538440"><a name="p95328538440"></a><a name="p95328538440"></a>自定义模式</p>
    </td>
    </tr>
    <tr id="row16532753114417"><td class="cellrowborder" valign="top" width="23.189999999999998%" headers="mcps1.2.3.1.1 "><p id="p353219537448"><a name="p353219537448"></a><a name="p353219537448"></a>效果</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.81%" headers="mcps1.2.3.1.2 "><p id="p5532353104418"><a name="p5532353104418"></a><a name="p5532353104418"></a>Allow</p>
    </td>
    </tr>
    <tr id="row115321753164415"><td class="cellrowborder" valign="top" width="23.189999999999998%" headers="mcps1.2.3.1.1 "><p id="p1553215538449"><a name="p1553215538449"></a><a name="p1553215538449"></a>被授权用户</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.81%" headers="mcps1.2.3.1.2 "><a name="ul136938242519"></a><a name="ul136938242519"></a><ul id="ul136938242519"><li>包含</li><li>当前账号，并选择需要授权的IAM用户</li></ul>
    </td>
    </tr>
    <tr id="row653285374414"><td class="cellrowborder" valign="top" width="23.189999999999998%" headers="mcps1.2.3.1.1 "><p id="p753212538444"><a name="p753212538444"></a><a name="p753212538444"></a>资源</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.81%" headers="mcps1.2.3.1.2 "><a name="ul964933612542"></a><a name="ul964933612542"></a><ul id="ul964933612542"><li>包含</li><li>资源名称不配置</li></ul>
    </td>
    </tr>
    <tr id="row18790945165418"><td class="cellrowborder" valign="top" width="23.189999999999998%" headers="mcps1.2.3.1.1 "><p id="p12791194519544"><a name="p12791194519544"></a><a name="p12791194519544"></a>动作</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.81%" headers="mcps1.2.3.1.2 "><a name="ul815102155519"></a><a name="ul815102155519"></a><ul id="ul815102155519"><li>包含</li><li>ListBucket</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

7.  单击“确定”。
8.  单击“创建桶策略”，系统弹出“创集桶策略”对话框。
9.  配置如下参数，授予IAM用户上传对象的权限。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >授予用户对象操作权限前，需先授予其访问桶的权限。  

    **表 2**  授予上传对象的权限的参数配置

    <a name="table566311261565"></a>
    <table><thead align="left"><tr id="row16664826175610"><th class="cellrowborder" valign="top" width="22.98%" id="mcps1.2.3.1.1"><p id="p1466442615612"><a name="p1466442615612"></a><a name="p1466442615612"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="77.02%" id="mcps1.2.3.1.2"><p id="p1466516269566"><a name="p1466516269566"></a><a name="p1466516269566"></a>取值</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row12665142619562"><td class="cellrowborder" valign="top" width="22.98%" headers="mcps1.2.3.1.1 "><p id="p36664266562"><a name="p36664266562"></a><a name="p36664266562"></a>策略模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.02%" headers="mcps1.2.3.1.2 "><p id="p14666152615562"><a name="p14666152615562"></a><a name="p14666152615562"></a>自定义模式</p>
    </td>
    </tr>
    <tr id="row3667132613567"><td class="cellrowborder" valign="top" width="22.98%" headers="mcps1.2.3.1.1 "><p id="p1866732655612"><a name="p1866732655612"></a><a name="p1866732655612"></a>效果</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.02%" headers="mcps1.2.3.1.2 "><p id="p966982619569"><a name="p966982619569"></a><a name="p966982619569"></a>Allow</p>
    </td>
    </tr>
    <tr id="row666915260561"><td class="cellrowborder" valign="top" width="22.98%" headers="mcps1.2.3.1.1 "><p id="p8670112635619"><a name="p8670112635619"></a><a name="p8670112635619"></a>被授权用户</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.02%" headers="mcps1.2.3.1.2 "><a name="ul1670726135620"></a><a name="ul1670726135620"></a><ul id="ul1670726135620"><li>包含</li><li>当前账号，并选择需要授权的IAM用户</li></ul>
    </td>
    </tr>
    <tr id="row126721226135618"><td class="cellrowborder" valign="top" width="22.98%" headers="mcps1.2.3.1.1 "><p id="p0673122685615"><a name="p0673122685615"></a><a name="p0673122685615"></a>资源</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.02%" headers="mcps1.2.3.1.2 "><a name="ul11674152619564"></a><a name="ul11674152619564"></a><ul id="ul11674152619564"><li>包含</li><li>资源名称：*</li></ul>
    </td>
    </tr>
    <tr id="row167522618569"><td class="cellrowborder" valign="top" width="22.98%" headers="mcps1.2.3.1.1 "><p id="p1367692611568"><a name="p1367692611568"></a><a name="p1367692611568"></a>动作</p>
    </td>
    <td class="cellrowborder" valign="top" width="77.02%" headers="mcps1.2.3.1.2 "><a name="ul176761226135619"></a><a name="ul176761226135619"></a><ul id="ul176761226135619"><li>包含</li><li>PutObject</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

10. 单击“确定”。

## 验证<a name="section162913213812"></a>

使用OBS Browser用来验证以上授权。

1.  在管理控制台上创建被授权用户的AK/SK。
2.  打开OBS Browser，配置已获取到的AK/SK，并设置“访问路径”为授权的桶名称。

    **图 1**  添加新账号-OBS存储<a name="fig3392193510417"></a>  
    ![](figures/添加新账号-OBS存储.png "添加新账号-OBS存储")

3.  当主账号未授权给用户访问桶权限时，用户用OBS Browser访问桶时，被拒绝访问。
4.  主账号配置授予给用户访问桶权限后，用户可以用OBS Browser登录访问桶，桶界面正常显示桶中对象。
5.  此时上传对象到桶中，上传失败。单击页面右上角的![](figures/lwx389318-海量存储PDU-云存储-image-38ab23ca-8c32-4c90-b334-2a71e1013cd9.png)，进入“任务管理”界面，“状态”为“失败”，失败原因为“拒绝访问”。
6.  主账号配置授予给用户上传对象权限后，用户用OBS Browser上传对象成功，对象在对象列表中显示。

