# OBS控制台监控指标<a name="obs_03_0009"></a>

您可在OBS管理控制台上查看桶的流量统计和请求次数，方便您及时了解目前资源的使用状况、并合理规划使用计划。

## 操作步骤<a name="section124333398423"></a>

1.  在桶列表中单击待操作的桶，进入“概览”页面。
2.  在“基础数据统计”下可查看桶的流量监控信息，如[图1](#fig2848684117471)所示。

    **图 1**  查看桶的监控信息<a name="fig2848684117471"></a>  
    ![](figures/查看桶的监控信息.png "查看桶的监控信息")

    桶级监控可以统计本月和上月的请求次数和流量。

    **表 1**  桶的监控数据参数说明

    <a name="table1034862635715"></a>
    <table><thead align="left"><tr id="row135142612570"><th class="cellrowborder" valign="top" width="28.999999999999996%" id="mcps1.2.3.1.1"><p id="p2351182620575"><a name="p2351182620575"></a><a name="p2351182620575"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="71%" id="mcps1.2.3.1.2"><p id="p1735219265577"><a name="p1735219265577"></a><a name="p1735219265577"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row335362611573"><td class="cellrowborder" valign="top" width="28.999999999999996%" headers="mcps1.2.3.1.1 "><p id="p1335417269573"><a name="p1335417269573"></a><a name="p1335417269573"></a>存储用量</p>
    </td>
    <td class="cellrowborder" valign="top" width="71%" headers="mcps1.2.3.1.2 "><p id="p63819601786"><a name="p63819601786"></a><a name="p63819601786"></a>桶中存储的对象占用的存储空间。</p>
    <p id="p41001540162115"><a name="p41001540162115"></a><a name="p41001540162115"></a>桶的存储空间默认情况下是没有配额限制的，您也可以通过设置桶配额来设置桶的存储空间，详情请参见<a href="https://support.huaweicloud.com/api-obs/zh-cn_topic_0100846743.html" target="_blank" rel="noopener noreferrer">设置桶配额</a>。</p>
    </td>
    </tr>
    <tr id="row4356142614579"><td class="cellrowborder" valign="top" width="28.999999999999996%" headers="mcps1.2.3.1.1 "><p id="p6357926195717"><a name="p6357926195717"></a><a name="p6357926195717"></a>对象数量</p>
    </td>
    <td class="cellrowborder" valign="top" width="71%" headers="mcps1.2.3.1.2 "><p id="p321290821786"><a name="p321290821786"></a><a name="p321290821786"></a>桶中存储的对象数量，为最新版本和历史版本的对象总和。</p>
    </td>
    </tr>
    <tr id="row143591326135715"><td class="cellrowborder" rowspan="2" valign="top" width="28.999999999999996%" headers="mcps1.2.3.1.1 "><p id="p1736214267570"><a name="p1736214267570"></a><a name="p1736214267570"></a>请求次数</p>
    </td>
    <td class="cellrowborder" valign="top" width="71%" headers="mcps1.2.3.1.2 "><p id="p336402614579"><a name="p336402614579"></a><a name="p336402614579"></a>PUT：所选当月时间，向桶及桶中对象发起的PUT/POST/DELETE请求次数。</p>
    </td>
    </tr>
    <tr id="row153601126125711"><td class="cellrowborder" valign="top" headers="mcps1.2.3.1.1 "><p id="p10364192665715"><a name="p10364192665715"></a><a name="p10364192665715"></a>GET：所选当月时间，向桶及桶中对象发起的GET/HEAD/OPTIONS请求次数。</p>
    </td>
    </tr>
    <tr id="row10362172615718"><td class="cellrowborder" rowspan="2" valign="top" width="28.999999999999996%" headers="mcps1.2.3.1.1 "><p id="p173601026105713"><a name="p173601026105713"></a><a name="p173601026105713"></a>内网流量统计</p>
    </td>
    <td class="cellrowborder" valign="top" width="71%" headers="mcps1.2.3.1.2 "><p id="p14360132619570"><a name="p14360132619570"></a><a name="p14360132619570"></a>内网流出：所选当月时间，桶的所有流出华为云流量。</p>
    </td>
    </tr>
    <tr id="row1836417267577"><td class="cellrowborder" valign="top" headers="mcps1.2.3.1.1 "><p id="p43621526175713"><a name="p43621526175713"></a><a name="p43621526175713"></a>内网流入：所选当月时间，桶的所有流入华为云流量。</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >以上统计数据非实时数据，大约存在一个小时左右的延迟，仅供参考。  


