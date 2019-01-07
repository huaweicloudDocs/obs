# Cloud Eye控制台监控指标<a name="obs_03_0010"></a>

云监控（Cloud Eye）管理控制台支持监控桶的上传流量、下载流量、GET类请求次数、PUT类请求次数、GET类请求首字节平均时延、4xx异常次数和5xx异常次数。

**图 1**  云监控示意图<a name="fig203414262328"></a>  
![](figures/云监控示意图.png "云监控示意图")

**表 1**  OBS监控指标

<a name="table128512311216"></a>
<table><thead align="left"><tr id="row208519234123"><th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.1"><p id="p138520239123"><a name="p138520239123"></a><a name="p138520239123"></a>指标名称</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.2"><p id="p18562312121"><a name="p18562312121"></a><a name="p18562312121"></a>含义</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="p98513232128"><a name="p98513232128"></a><a name="p98513232128"></a>取值范围</p>
</th>
</tr>
</thead>
<tbody><tr id="row785132321213"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p135517342133"><a name="p135517342133"></a><a name="p135517342133"></a>下载流量</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p13551123419137"><a name="p13551123419137"></a><a name="p13551123419137"></a>该指标用于统计所有桶的所有下载请求响应的字节数，包括http body体。以字节为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p2055143410132"><a name="p2055143410132"></a><a name="p2055143410132"></a>≥ 0 Byte</p>
</td>
</tr>
<tr id="row5101162341218"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p26611342131312"><a name="p26611342131312"></a><a name="p26611342131312"></a>上传流量</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p18661144291318"><a name="p18661144291318"></a><a name="p18661144291318"></a>该指标用于统计所有桶的所有上传请求消息体的字节数，包括http body体。以字节为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p46611421133"><a name="p46611421133"></a><a name="p46611421133"></a>≥ 0 Byte</p>
</td>
</tr>
<tr id="row14101023201219"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p11395165010139"><a name="p11395165010139"></a><a name="p11395165010139"></a>GET类请求次数</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p539575020136"><a name="p539575020136"></a><a name="p539575020136"></a>该指标用于统计所有桶及桶中对象的GET/HEAD/OPTIONS请求次数。以次为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p7395550121314"><a name="p7395550121314"></a><a name="p7395550121314"></a>≥ 0 Counts</p>
</td>
</tr>
<tr id="row410122331215"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p61297585139"><a name="p61297585139"></a><a name="p61297585139"></a>PUT类请求次数</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p15129165831314"><a name="p15129165831314"></a><a name="p15129165831314"></a>该指标用于统计所有桶及桶中对象的PUT/POST/DELETE请求次数。以次为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p18129145812130"><a name="p18129145812130"></a><a name="p18129145812130"></a>≥ 0 Counts</p>
</td>
</tr>
<tr id="row61017239122"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p165555166148"><a name="p165555166148"></a><a name="p165555166148"></a>GET类请求首字节平均时延</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p195553165142"><a name="p195553165142"></a><a name="p195553165142"></a>该指标用于统计GET/HEAD/OPTIONS操作，在一个统计周期内从系统收到完整请求到开始返回响应的耗时平均值。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p9555141612143"><a name="p9555141612143"></a><a name="p9555141612143"></a>≥ 0 ms</p>
</td>
</tr>
<tr id="row374382021417"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p12993172911412"><a name="p12993172911412"></a><a name="p12993172911412"></a>4xx异常次数</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p199931329171414"><a name="p199931329171414"></a><a name="p199931329171414"></a>该指标用于统计服务端响应错误状态码为4xx的请求数。以次为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p149931290144"><a name="p149931290144"></a><a name="p149931290144"></a>≥ 0 Counts</p>
</td>
</tr>
<tr id="row310115233127"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p1726011371143"><a name="p1726011371143"></a><a name="p1726011371143"></a>5xx异常次数</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p22601137181413"><a name="p22601137181413"></a><a name="p22601137181413"></a>该指标用于统计服务端响应错误状态码为5xx的请求数。以次为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p110172351214"><a name="p110172351214"></a><a name="p110172351214"></a>≥ 0 Counts</p>
</td>
</tr>
</tbody>
</table>

## 操作步骤<a name="section29751041119"></a>

1.  登录华为云管理控制台。
2.  选择“服务列表\>管理与部署\>云监控服务”，登录云监控管理控制台。
3.  在左侧导航栏单击“告警\>告警规则”。
4.  单击“创建告警规则”，弹出“创建告警规则”。
5.  设置“资源类型”为“对象存储服务”，“维度”为“桶名”，并单击“选择”，选择“监控对象”。

    **表 2**  参数说明

    <a name="table1655818513346"></a>
    <table><thead align="left"><tr id="row85589515345"><th class="cellrowborder" valign="top" width="20.42204220422042%" id="mcps1.2.4.1.1"><p id="p1396575716342"><a name="p1396575716342"></a><a name="p1396575716342"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="46.24462446244625%" id="mcps1.2.4.1.2"><p id="p109651757133411"><a name="p109651757133411"></a><a name="p109651757133411"></a>参数说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="p1296514579345"><a name="p1296514579345"></a><a name="p1296514579345"></a>取值样例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row655865117344"><td class="cellrowborder" valign="top" width="20.42204220422042%" headers="mcps1.2.4.1.1 "><p id="p13541814578"><a name="p13541814578"></a><a name="p13541814578"></a>资源类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="46.24462446244625%" headers="mcps1.2.4.1.2 "><p id="p17354214573"><a name="p17354214573"></a><a name="p17354214573"></a>配置告警规则监控的云服务资源类型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p635401410718"><a name="p635401410718"></a><a name="p635401410718"></a>对象存储服务</p>
    </td>
    </tr>
    <tr id="row105586516347"><td class="cellrowborder" valign="top" width="20.42204220422042%" headers="mcps1.2.4.1.1 "><p id="p17354214475"><a name="p17354214475"></a><a name="p17354214475"></a>维度</p>
    </td>
    <td class="cellrowborder" valign="top" width="46.24462446244625%" headers="mcps1.2.4.1.2 "><p id="p163543141079"><a name="p163543141079"></a><a name="p163543141079"></a>用于指定告警规则对应指标的维度名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p73541114076"><a name="p73541114076"></a><a name="p73541114076"></a>对象存储桶</p>
    </td>
    </tr>
    <tr id="row75581351173415"><td class="cellrowborder" valign="top" width="20.42204220422042%" headers="mcps1.2.4.1.1 "><p id="p1069713517818"><a name="p1069713517818"></a><a name="p1069713517818"></a>监控对象</p>
    </td>
    <td class="cellrowborder" valign="top" width="46.24462446244625%" headers="mcps1.2.4.1.2 "><p id="p26971456811"><a name="p26971456811"></a><a name="p26971456811"></a>用来配置该告警规则针对的具体资源，可以是一个或多个。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p17558195143412"><a name="p17558195143412"></a><a name="p17558195143412"></a>桶</p>
    </td>
    </tr>
    </tbody>
    </table>

6.  单击“下一步”。
7.  设置相关监控指标，监控指标参数说明如[表3](#table046794374713)所示。

    **表 3**  参数说明

    <a name="table046794374713"></a>
    <table><thead align="left"><tr id="row15467134310471"><th class="cellrowborder" colspan="2" valign="top" id="mcps1.2.5.1.1"><p id="p164677438476"><a name="p164677438476"></a><a name="p164677438476"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" id="mcps1.2.5.1.2"><p id="p12467343134717"><a name="p12467343134717"></a><a name="p12467343134717"></a>参数说明</p>
    </th>
    <th class="cellrowborder" valign="top" id="mcps1.2.5.1.3"><p id="p144672433479"><a name="p144672433479"></a><a name="p144672433479"></a>取值样例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1946713433478"><td class="cellrowborder" colspan="2" valign="top" headers="mcps1.2.5.1.1 "><p id="p1195202105011"><a name="p1195202105011"></a><a name="p1195202105011"></a>选择类型</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p141956285018"><a name="p141956285018"></a><a name="p141956285018"></a>支持从模板导入和自定义创建。</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="p5195723504"><a name="p5195723504"></a><a name="p5195723504"></a>-</p>
    </td>
    </tr>
    <tr id="row6467164320472"><td class="cellrowborder" colspan="2" valign="top" headers="mcps1.2.5.1.1 "><p id="p1776835155"><a name="p1776835155"></a><a name="p1776835155"></a>监控指标</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p201956295011"><a name="p201956295011"></a><a name="p201956295011"></a>例如：</p>
    <a name="ul1219562185012"></a><a name="ul1219562185012"></a><ul id="ul1219562185012"><li>下载流量</li><li>上传流量</li><li>GET类请求次数</li><li>PUT类请求次数</li><li>GET类请求首字节平均时延</li><li>4xx异常次数</li><li>5xx异常次数</li></ul>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="p2019514213504"><a name="p2019514213504"></a><a name="p2019514213504"></a>-</p>
    </td>
    </tr>
    <tr id="row204676438477"><td class="cellrowborder" rowspan="3" valign="top" width="16.04%" headers="mcps1.2.5.1.1 "><p id="p219518265018"><a name="p219518265018"></a><a name="p219518265018"></a>告警策略</p>
    </td>
    <td class="cellrowborder" valign="top" width="14.829999999999998%" headers="mcps1.2.5.1.1 "><p id="p1226953141313"><a name="p1226953141313"></a><a name="p1226953141313"></a>阈值</p>
    </td>
    <td class="cellrowborder" valign="top" width="35.5%" headers="mcps1.2.5.1.2 "><p id="p1019518215013"><a name="p1019518215013"></a><a name="p1019518215013"></a>由数据类型（原始值、最大值、最小值、平均值、求和值和方差值）、判断条件（&gt;、≥、&lt;、≤和=）、临界值三部分组成，用来配置告警条件，例如“平均值&gt;80”就是一个告警条件。</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.629999999999995%" headers="mcps1.2.5.1.3 "><p id="p201954275017"><a name="p201954275017"></a><a name="p201954275017"></a>80</p>
    </td>
    </tr>
    <tr id="row8631103319141"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p963116337144"><a name="p963116337144"></a><a name="p963116337144"></a>监控周期</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p14631133311410"><a name="p14631133311410"></a><a name="p14631133311410"></a>告警规则刷新告警状态的周期。</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p186312033101414"><a name="p186312033101414"></a><a name="p186312033101414"></a>5分钟</p>
    </td>
    </tr>
    <tr id="row15467174315475"><td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p826135331313"><a name="p826135331313"></a><a name="p826135331313"></a>连续出现的次数</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.1 "><p id="p104451517508"><a name="p104451517508"></a><a name="p104451517508"></a>触发告警时的采样点数目。 例如： 出现次数配置为n，则告警规则的采样点是连续n个监控周期（原始数据使用5分钟的默认监控周期）的采样点，当这些采样点全部满足阈值中配置的告警条件，告警规则的状态才会刷新为告警。</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1444181505012"><a name="p1444181505012"></a><a name="p1444181505012"></a>3</p>
    </td>
    </tr>
    <tr id="row393417551738"><td class="cellrowborder" colspan="2" valign="top" headers="mcps1.2.5.1.1 "><p id="p95982032446"><a name="p95982032446"></a><a name="p95982032446"></a>告警级别</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p125988322419"><a name="p125988322419"></a><a name="p125988322419"></a>告警的紧急重要程度。</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="p1059810321341"><a name="p1059810321341"></a><a name="p1059810321341"></a>重要</p>
    </td>
    </tr>
    <tr id="row16467134320472"><td class="cellrowborder" colspan="2" valign="top" headers="mcps1.2.5.1.1 "><p id="p244015175012"><a name="p244015175012"></a><a name="p244015175012"></a>发送通知</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.2 "><p id="p1644121595019"><a name="p1644121595019"></a><a name="p1644121595019"></a>配置是否发送邮件、短信通知用户或发送HTTP、HTTPS消息给服务器。</p>
    </td>
    <td class="cellrowborder" valign="top" headers="mcps1.2.5.1.3 "><p id="p244171516501"><a name="p244171516501"></a><a name="p244171516501"></a>-</p>
    </td>
    </tr>
    </tbody>
    </table>

8.  单击“下一步”。
9.  输入“名称”，单击“创建”。告警规则创建完成。

    **表 4**  参数说明

    <a name="table3293121910491"></a>
    <table><thead align="left"><tr id="row15293151924912"><th class="cellrowborder" valign="top" width="25.252525252525253%" id="mcps1.2.4.1.1"><p id="p132931019154915"><a name="p132931019154915"></a><a name="p132931019154915"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="38.38383838383839%" id="mcps1.2.4.1.2"><p id="p329361914916"><a name="p329361914916"></a><a name="p329361914916"></a>参数说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="36.36363636363637%" id="mcps1.2.4.1.3"><p id="p18293319114916"><a name="p18293319114916"></a><a name="p18293319114916"></a>取值样例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row163091419194916"><td class="cellrowborder" valign="top" width="25.252525252525253%" headers="mcps1.2.4.1.1 "><p id="p1309191917493"><a name="p1309191917493"></a><a name="p1309191917493"></a>名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="38.38383838383839%" headers="mcps1.2.4.1.2 "><p id="p83091519144910"><a name="p83091519144910"></a><a name="p83091519144910"></a>系统会随机产生一个名称，用户也可以进行修改。</p>
    </td>
    <td class="cellrowborder" valign="top" width="36.36363636363637%" headers="mcps1.2.4.1.3 "><p id="p6309121912495"><a name="p6309121912495"></a><a name="p6309121912495"></a>alarm-b6al</p>
    </td>
    </tr>
    <tr id="row20309151944910"><td class="cellrowborder" valign="top" width="25.252525252525253%" headers="mcps1.2.4.1.1 "><p id="p530912199493"><a name="p530912199493"></a><a name="p530912199493"></a>描述</p>
    </td>
    <td class="cellrowborder" valign="top" width="38.38383838383839%" headers="mcps1.2.4.1.2 "><p id="p1830991919494"><a name="p1830991919494"></a><a name="p1830991919494"></a>告警规则描述（此参数非必填项）。</p>
    </td>
    <td class="cellrowborder" valign="top" width="36.36363636363637%" headers="mcps1.2.4.1.3 "><p id="p10309141944915"><a name="p10309141944915"></a><a name="p10309141944915"></a>-</p>
    </td>
    </tr>
    </tbody>
    </table>

10. 在左侧导航树选择“云服务监控\>对象存储服务”。
11. 选择要查看的桶所在行，单击“查看监控图标”，可以查看近1小时、近3小时和近12小时的监控数据视图。
12. （可选）单击“设置监控指标”，您可以设置在页面中展示的监控指标视图。

