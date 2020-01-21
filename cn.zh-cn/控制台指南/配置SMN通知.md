# 配置SMN通知<a name="zh-cn_topic_0066088963"></a>

本节介绍如何在OBS控制台配置SMN通知。

## 背景知识<a name="section72855457345"></a>

请参见[SMN通知简介](SMN通知简介.md)。

## 操作步骤<a name="section4422459618019"></a>

1.  在OBS管理控制台左侧导航栏选择“对象存储“。
2.  在桶列表单击待操作的桶，进入“概览”页面。
3.  在“基础配置”下，单击“事件通知”卡片，系统跳转至“事件通知”界面。

    或您可以直接在左侧导航栏单击“基础配置\>事件通知”，进入“事件通知”界面。

4.  单击“创建”，系统弹出“创建事件通知”对话框，如[图1](#fig17847723015)所示。

    **图 1**  创建事件通知<a name="fig17847723015"></a>  
    ![](figures/创建事件通知.png "创建事件通知")

5.  配置事件通知参数，参数说明如[表1](#aobs_console_0039_mmccppss_table01)所示。

    **表 1**  事件通知参数说明

    <a name="aobs_console_0039_mmccppss_table01"></a>
    <table><thead align="left"><tr id="row2055942"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.3.1.1"><p id="p32313598"><a name="p32313598"></a><a name="p32313598"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="75%" id="mcps1.2.3.1.2"><p id="p155758"><a name="p155758"></a><a name="p155758"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row12616447"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p15299288"><a name="p15299288"></a><a name="p15299288"></a>事件通知名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p31282850"><a name="p31282850"></a><a name="p31282850"></a>新增事件的名称，用户自定义。若不填写，系统将默认自动生成一个全局唯一ID作为名称。</p>
    </td>
    </tr>
    <tr id="row13110201"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p55293359"><a name="p55293359"></a><a name="p55293359"></a>事件</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p49577065"><a name="p49577065"></a><a name="p49577065"></a>事件类型。目前，<span id="ph6378153015417"><a name="ph6378153015417"></a><a name="ph6378153015417"></a>OBS</span>支持对以下事件类型进行事件通知。</p>
    <a name="ul43540403"></a><a name="ul43540403"></a><ul id="ul43540403"><li><strong id="b2253084295127"><a name="b2253084295127"></a><a name="b2253084295127"></a>ObjectCreated：</strong>表示所有创建对象的操作，包含Put、Post、Copy对象以及合并段。</li><li><strong id="b21739820154642"><a name="b21739820154642"></a><a name="b21739820154642"></a>Put</strong>：使用Put方法上传对象。</li><li><strong id="b7554011173727"><a name="b7554011173727"></a><a name="b7554011173727"></a>Post</strong>：使用Post方法上传对象。</li><li><strong id="b19295192"><a name="b19295192"></a><a name="b19295192"></a>Copy</strong>：使用copy方法复制对象。</li><li><strong id="b6205384517382"><a name="b6205384517382"></a><a name="b6205384517382"></a>CompleteMultipartUpload</strong>：表示合并分段任务。</li><li><strong id="b4214016595037"><a name="b4214016595037"></a><a name="b4214016595037"></a>ObjectRemoved：</strong>表示删除对象。</li><li><strong id="b28442244"><a name="b28442244"></a><a name="b28442244"></a>Delete</strong>：指定对象版本号删除对象。</li><li><strong id="b22120394"><a name="b22120394"></a><a name="b22120394"></a>DeleteMarkerCreated</strong>：不指定对象版本号删除对象。</li></ul>
    <p id="p64865822"><a name="p64865822"></a><a name="p64865822"></a>多个事件类型可以作用于同一个目标对象，例如：同时选择“事件类型”复选框中的<strong id="b46921489"><a name="b46921489"></a><a name="b46921489"></a>Put</strong>、<strong id="b19640220"><a name="b19640220"></a><a name="b19640220"></a>Copy</strong>、<strong id="b42544256"><a name="b42544256"></a><a name="b42544256"></a>Delete</strong>等方法作用于某目标对象，则用户往该桶中上传、复制、删除符合前后缀规则的目标对象时，均会发送事件通知给用户。<strong id="b41674970143835"><a name="b41674970143835"></a><a name="b41674970143835"></a>ObjectCreated</strong>包含了<strong id="b15574064143840"><a name="b15574064143840"></a><a name="b15574064143840"></a>Put</strong>、<strong id="b62119592143845"><a name="b62119592143845"></a><a name="b62119592143845"></a>Post</strong>、<strong id="b7081676143849"><a name="b7081676143849"></a><a name="b7081676143849"></a>Copy</strong>和<strong id="b31607544151827"><a name="b31607544151827"></a><a name="b31607544151827"></a>CompleteMultipartUpload</strong>，如果选择了<strong id="b63678108143857"><a name="b63678108143857"></a><a name="b63678108143857"></a>ObjectCreated</strong>，则不能再选择<strong id="b39981405143910"><a name="b39981405143910"></a><a name="b39981405143910"></a>Put</strong>、<strong id="b17268397143910"><a name="b17268397143910"></a><a name="b17268397143910"></a>Post</strong>、<strong id="b56562934143910"><a name="b56562934143910"></a><a name="b56562934143910"></a>Copy</strong>或<strong id="b59319998143915"><a name="b59319998143915"></a><a name="b59319998143915"></a>CompleteMultipartUpload</strong>。同理如果选择了<strong id="b44527778143920"><a name="b44527778143920"></a><a name="b44527778143920"></a>ObjectRemoved</strong>，则不能再选择<strong id="b57045165143925"><a name="b57045165143925"></a><a name="b57045165143925"></a>Delete</strong>或<strong id="b40642771143930"><a name="b40642771143930"></a><a name="b40642771143930"></a>DeleteMarkerCreated</strong>。</p>
    </td>
    </tr>
    <tr id="row47353991"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p10468038"><a name="p10468038"></a><a name="p10468038"></a>前缀</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p42604738"><a name="p42604738"></a><a name="p42604738"></a>指定事件作用的目标对象的前缀。</p>
    <div class="note" id="note13847653113412"><a name="note13847653113412"></a><a name="note13847653113412"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p138481553193416"><a name="p138481553193416"></a><a name="p138481553193416"></a>当前缀和后缀都不配置时，事件通知规则将作用于桶中所有对象。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row16547757"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p65299951"><a name="p65299951"></a><a name="p65299951"></a>后缀</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p54804702"><a name="p54804702"></a><a name="p54804702"></a>指定事件作用的目标对象的后缀。</p>
    <div class="note" id="note64263792115"><a name="note64263792115"></a><a name="note64263792115"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul75801343183518"></a><a name="ul75801343183518"></a><ul id="ul75801343183518"><li>文件夹是以“/”结尾的，“/”前的字符为文件夹名称。对文件夹的相关操作做事件通知时，若要匹配后缀，后缀必须以“/”结尾。</li><li>当前缀和后缀都不配置时，事件通知规则将作用于桶中所有对象。</li></ul>
    </div></div>
    </td>
    </tr>
    <tr id="row16019620144324"><td class="cellrowborder" rowspan="2" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p28106203"><a name="p28106203"></a><a name="p28106203"></a>SMN主题</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p28828893173745"><a name="p28828893173745"></a><a name="p28828893173745"></a>项目：选择SMN主题所在的项目。</p>
    <p id="p66230298175226"><a name="p66230298175226"></a><a name="p66230298175226"></a>项目用于管理和分类所有的云资源，包括SMN主题。项目不同，对应的SMN主题也不相同，请先选择项目再选择主题。</p>
    </td>
    </tr>
    <tr id="row13603062"><td class="cellrowborder" valign="top" headers="mcps1.2.3.1.1 "><div class="p" id="p62009948"><a name="p62009948"></a><a name="p62009948"></a>主题：选择已授权给<span id="ph1583915521448"><a name="ph1583915521448"></a><a name="ph1583915521448"></a>OBS</span>发布消息的SMN主题。SMN主题需通过SMN页面创建。<div class="note" id="note21218627"><a name="note21218627"></a><a name="note21218627"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul290173585413"></a><a name="ul290173585413"></a><ul id="ul290173585413"><li class="NotesTextinTable">SMN主题配置成功后，请不要随意删除与<span id="ph3252558141"><a name="ph3252558141"></a><a name="ph3252558141"></a>OBS</span>管理控制台事件相关联的主题，也不要取消与<span id="ph12496511353"><a name="ph12496511353"></a><a name="ph12496511353"></a>OBS</span>管理控制台事件相关联主题对<span id="ph66421261753"><a name="ph66421261753"></a><a name="ph66421261753"></a>OBS</span>的授权。</li><li class="NotesTextinTable">若与<span id="ph630310191850"><a name="ph630310191850"></a><a name="ph630310191850"></a>OBS</span>管理控制台事件相关联的主题被删除或取消该主题对<span id="ph174479151055"><a name="ph174479151055"></a><a name="ph174479151055"></a>OBS</span>的授权，则可能出现以下现象：<p class="NotesTextinTable" id="p162521921105510"><a name="p162521921105510"></a><a name="p162521921105510"></a>a. 对应主题的订阅者无法收到消息。</p>
    <p class="NotesTextinTable" id="p198921517175511"><a name="p198921517175511"></a><a name="p198921517175511"></a>b. 修改当前桶的事件配置，会自动清理不可用主题对应配置。</p>
    </li><li>详细的使用SMN服务的操作指导请参见《消息通知服务用户指南》的“创建主题”、“添加订阅者”和“主题策略”章节的内容。</li></ul>
    </div></div>
    </div>
    </td>
    </tr>
    </tbody>
    </table>

6.  单击“确定”。

## 相关操作<a name="section183921920123113"></a>

您可以单击待操作的事件通知实例后面的“编辑”，编辑修改事件通知；单击“删除”，删除事件通知。

若您要批量删除事件通知，选中待删除的事件通知实例，单击列表上方的“删除”，完成批量删除。

