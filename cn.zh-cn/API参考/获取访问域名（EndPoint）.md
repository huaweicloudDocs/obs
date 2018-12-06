# 获取访问域名（EndPoint）<a name="ZH-CN_TOPIC_0136050628"></a>

OBS在每个区域都提供独立的二级域名，访问OBS服务既可以使用OBS提供的域名，也可以使用自定义域名。

OBS已上线全新域名**\*.myhuaweicloud.com**，同时也依然支持老域名**\*.myhwclouds.com**。

推荐您使用新域名访问OBS，新域名请从[地区和终端节点](http://developer.huaweicloud.com/dev/endpoint)获取。本文档的所有示例均使用新域名。

老域名如[表1](#table4541342212)所示。

**表 1**  OBS老域名

<a name="table4541342212"></a>
<table><thead align="left"><tr id="row135611348217"><th class="cellrowborder" valign="top" width="13.089999999999998%" id="mcps1.2.6.1.1"><p id="p195613348212"><a name="p195613348212"></a><a name="p195613348212"></a>区域名称</p>
</th>
<th class="cellrowborder" valign="top" width="14.24%" id="mcps1.2.6.1.2"><p id="p356634521"><a name="p356634521"></a><a name="p356634521"></a>区域</p>
</th>
<th class="cellrowborder" valign="top" width="30.580000000000002%" id="mcps1.2.6.1.3"><p id="p8564341621"><a name="p8564341621"></a><a name="p8564341621"></a>终端节点（Endpoint）</p>
</th>
<th class="cellrowborder" valign="top" width="33.82%" id="mcps1.2.6.1.4"><p id="p55613341324"><a name="p55613341324"></a><a name="p55613341324"></a>静态网站托管域名</p>
</th>
<th class="cellrowborder" valign="top" width="8.27%" id="mcps1.2.6.1.5"><p id="p756173411214"><a name="p756173411214"></a><a name="p756173411214"></a>协议类型</p>
</th>
</tr>
</thead>
<tbody><tr id="row18561234422"><td class="cellrowborder" valign="top" width="13.089999999999998%" headers="mcps1.2.6.1.1 "><p id="p158211204319"><a name="p158211204319"></a><a name="p158211204319"></a>华北-北京一</p>
</td>
<td class="cellrowborder" valign="top" width="14.24%" headers="mcps1.2.6.1.2 "><p id="p68216201831"><a name="p68216201831"></a><a name="p68216201831"></a>cn-north-1</p>
</td>
<td class="cellrowborder" valign="top" width="30.580000000000002%" headers="mcps1.2.6.1.3 "><p id="p082118204319"><a name="p082118204319"></a><a name="p082118204319"></a>obs.cn-north-1.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="33.82%" headers="mcps1.2.6.1.4 "><p id="p15821152014318"><a name="p15821152014318"></a><a name="p15821152014318"></a>obs-website.cn-north-1.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="8.27%" headers="mcps1.2.6.1.5 "><p id="p198212202033"><a name="p198212202033"></a><a name="p198212202033"></a>HTTPS</p>
</td>
</tr>
<tr id="row4561434226"><td class="cellrowborder" valign="top" width="13.089999999999998%" headers="mcps1.2.6.1.1 "><p id="p14821182014311"><a name="p14821182014311"></a><a name="p14821182014311"></a>华东-上海二</p>
</td>
<td class="cellrowborder" valign="top" width="14.24%" headers="mcps1.2.6.1.2 "><p id="p582132017310"><a name="p582132017310"></a><a name="p582132017310"></a>cn-east-2</p>
</td>
<td class="cellrowborder" valign="top" width="30.580000000000002%" headers="mcps1.2.6.1.3 "><p id="p188218209315"><a name="p188218209315"></a><a name="p188218209315"></a>obs.cn-east-2.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="33.82%" headers="mcps1.2.6.1.4 "><p id="p1282120201936"><a name="p1282120201936"></a><a name="p1282120201936"></a>obs-website.cn-east-2.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="8.27%" headers="mcps1.2.6.1.5 "><p id="p6821220739"><a name="p6821220739"></a><a name="p6821220739"></a>HTTPS</p>
</td>
</tr>
<tr id="row1573342213"><td class="cellrowborder" valign="top" width="13.089999999999998%" headers="mcps1.2.6.1.1 "><p id="p282115201934"><a name="p282115201934"></a><a name="p282115201934"></a>华南-广州</p>
</td>
<td class="cellrowborder" valign="top" width="14.24%" headers="mcps1.2.6.1.2 "><p id="p19821220534"><a name="p19821220534"></a><a name="p19821220534"></a>cn-south-1</p>
</td>
<td class="cellrowborder" valign="top" width="30.580000000000002%" headers="mcps1.2.6.1.3 "><p id="p982112013319"><a name="p982112013319"></a><a name="p982112013319"></a>obs.cn-south-1.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="33.82%" headers="mcps1.2.6.1.4 "><p id="p168215202314"><a name="p168215202314"></a><a name="p168215202314"></a>obs-website.cn-south-1.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="8.27%" headers="mcps1.2.6.1.5 "><p id="p8821120437"><a name="p8821120437"></a><a name="p8821120437"></a>HTTPS</p>
</td>
</tr>
<tr id="row185753412218"><td class="cellrowborder" valign="top" width="13.089999999999998%" headers="mcps1.2.6.1.1 "><p id="p382212209310"><a name="p382212209310"></a><a name="p382212209310"></a>亚太-香港</p>
</td>
<td class="cellrowborder" valign="top" width="14.24%" headers="mcps1.2.6.1.2 "><p id="p14822142017313"><a name="p14822142017313"></a><a name="p14822142017313"></a>ap-southeast-1</p>
</td>
<td class="cellrowborder" valign="top" width="30.580000000000002%" headers="mcps1.2.6.1.3 "><p id="p68221202314"><a name="p68221202314"></a><a name="p68221202314"></a>obs.ap-southeast-1.myhwclouds.com</p>
</td>
<td class="cellrowborder" valign="top" width="33.82%" headers="mcps1.2.6.1.4 "><p id="p138224208316"><a name="p138224208316"></a><a name="p138224208316"></a>/</p>
</td>
<td class="cellrowborder" valign="top" width="8.27%" headers="mcps1.2.6.1.5 "><p id="p1382214201531"><a name="p1382214201531"></a><a name="p1382214201531"></a>HTTPS</p>
</td>
</tr>
</tbody>
</table>

