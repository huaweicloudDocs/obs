# Cloud Eye控制台监控指标<a name="obs_03_0010"></a>

云监控（Cloud Eye）管理控制台支持监控的OBS指标如[表1](#table128512311216)所示。

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
<tr id="row374382021417"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p12993172911412"><a name="p12993172911412"></a><a name="p12993172911412"></a>4xx错误次数</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="p199931329171414"><a name="p199931329171414"></a><a name="p199931329171414"></a>该指标用于统计服务端响应错误状态码为4xx的请求数。以次为单位。</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p149931290144"><a name="p149931290144"></a><a name="p149931290144"></a>≥ 0 Counts</p>
</td>
</tr>
<tr id="row310115233127"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="p1726011371143"><a name="p1726011371143"></a><a name="p1726011371143"></a>5xx错误次数</p>
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
2.  选择“服务列表\>管理与部署\>云监控”，登录云监控管理控制台。
3.  请参考云监控服务的[创建告警规则](https://support.huaweicloud.com/usermanual-ces/zh-cn_topic_0084572213.html)，配置OBS的云监控。

