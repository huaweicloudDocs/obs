# 通过临时URL访问OBS<a name="obs_21_0901"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。[接口参考文档](https://obssdk.obs.cn-north-1.myhuaweicloud.com/apidoc/cn/java/index.html)详细介绍了每个接口的参数和使用方法。

OBS客户端支持通过访问密钥、请求方法类型、请求参数等信息生成一个在Query参数中携带鉴权信息的URL，可将该URL提供给其他用户进行临时访问。在生成URL时，您需要指定URL的有效期来限制访客用户的访问时长。

如果您想授予其他用户对桶或对象临时进行其他操作的权限（例如上传或下载对象），则需要生成带对应请求的URL后（例如使用生成PUT请求的URL上传对象），将该URL提供给其他用户。

通过该方式可支持的操作以及相关信息见下表：

<a name="table1281912486367"></a>
<table><thead align="left"><tr id="row15820184813617"><th class="cellrowborder" valign="top" width="18.08%" id="mcps1.1.6.1.1"><p id="p1966411594366"><a name="p1966411594366"></a><a name="p1966411594366"></a><strong id="b173731084386"><a name="b173731084386"></a><a name="b173731084386"></a>操作名</strong></p>
</th>
<th class="cellrowborder" valign="top" width="26.919999999999998%" id="mcps1.1.6.1.2"><p id="p1482034843610"><a name="p1482034843610"></a><a name="p1482034843610"></a><strong id="b14111383381"><a name="b14111383381"></a><a name="b14111383381"></a>HTTP请求方法（OBS Java SDK对应值）</strong></p>
</th>
<th class="cellrowborder" valign="top" width="28.000000000000004%" id="mcps1.1.6.1.3"><p id="p168203489360"><a name="p168203489360"></a><a name="p168203489360"></a><strong id="b941268183818"><a name="b941268183818"></a><a name="b941268183818"></a>特殊操作符（OBS Java SDK对应值）</strong></p>
</th>
<th class="cellrowborder" valign="top" width="13%" id="mcps1.1.6.1.4"><p id="p17407122514013"><a name="p17407122514013"></a><a name="p17407122514013"></a><strong id="b1663082218144"><a name="b1663082218144"></a><a name="b1663082218144"></a>是否需要桶名</strong></p>
</th>
<th class="cellrowborder" valign="top" width="14.000000000000002%" id="mcps1.1.6.1.5"><p id="p342713304013"><a name="p342713304013"></a><a name="p342713304013"></a><strong id="b36345229141"><a name="b36345229141"></a><a name="b36345229141"></a>是否需要对象名</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row58205484364"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p0820194833619"><a name="p0820194833619"></a><a name="p0820194833619"></a>创建桶</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p682012484365"><a name="p682012484365"></a><a name="p682012484365"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p18820848163616"><a name="p18820848163616"></a><a name="p18820848163616"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1740762544011"><a name="p1740762544011"></a><a name="p1740762544011"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1342783319405"><a name="p1342783319405"></a><a name="p1342783319405"></a>否</p>
</td>
</tr>
<tr id="row17820114813619"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p88201148173616"><a name="p88201148173616"></a><a name="p88201148173616"></a>获取桶列表</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p438164024218"><a name="p438164024218"></a><a name="p438164024218"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p28205485368"><a name="p28205485368"></a><a name="p28205485368"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p740762554011"><a name="p740762554011"></a><a name="p740762554011"></a>否</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p842713315407"><a name="p842713315407"></a><a name="p842713315407"></a>否</p>
</td>
</tr>
<tr id="row2592353134213"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p10592153204213"><a name="p10592153204213"></a><a name="p10592153204213"></a>删除桶</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p4593153124214"><a name="p4593153124214"></a><a name="p4593153124214"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p5593853134213"><a name="p5593853134213"></a><a name="p5593853134213"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1059311535428"><a name="p1059311535428"></a><a name="p1059311535428"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p459385344219"><a name="p459385344219"></a><a name="p459385344219"></a>否</p>
</td>
</tr>
<tr id="row9452121424311"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1845215144430"><a name="p1845215144430"></a><a name="p1845215144430"></a>列举桶内对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p44526145430"><a name="p44526145430"></a><a name="p44526145430"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p44521214134317"><a name="p44521214134317"></a><a name="p44521214134317"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p15452171413430"><a name="p15452171413430"></a><a name="p15452171413430"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p845261414311"><a name="p845261414311"></a><a name="p845261414311"></a>否</p>
</td>
</tr>
<tr id="row1245131634310"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p12451516104313"><a name="p12451516104313"></a><a name="p12451516104313"></a>列举桶内多版本对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p13451416134314"><a name="p13451416134314"></a><a name="p13451416134314"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p946181611436"><a name="p946181611436"></a><a name="p946181611436"></a>SpecialParamEnum.VERSIONS</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1046191612433"><a name="p1046191612433"></a><a name="p1046191612433"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p2046101604314"><a name="p2046101604314"></a><a name="p2046101604314"></a>否</p>
</td>
</tr>
<tr id="row15886161618433"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p148861816114310"><a name="p148861816114310"></a><a name="p148861816114310"></a>列举分段上传任务</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p198861816144315"><a name="p198861816144315"></a><a name="p198861816144315"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p588651612433"><a name="p588651612433"></a><a name="p588651612433"></a>SpecialParamEnum.UPLOADS</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p158861016154311"><a name="p158861016154311"></a><a name="p158861016154311"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1188612160431"><a name="p1188612160431"></a><a name="p1188612160431"></a>否</p>
</td>
</tr>
<tr id="row961511716431"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p20615111712435"><a name="p20615111712435"></a><a name="p20615111712435"></a>获取桶元数据</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p26157172431"><a name="p26157172431"></a><a name="p26157172431"></a>HttpMethodEnum.HEAD</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p6615101764316"><a name="p6615101764316"></a><a name="p6615101764316"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1861581717431"><a name="p1861581717431"></a><a name="p1861581717431"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p126151017194318"><a name="p126151017194318"></a><a name="p126151017194318"></a>否</p>
</td>
</tr>
<tr id="row8568533134617"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p15568183314615"><a name="p15568183314615"></a><a name="p15568183314615"></a>获取桶区域位置</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p031511535464"><a name="p031511535464"></a><a name="p031511535464"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p13569103314461"><a name="p13569103314461"></a><a name="p13569103314461"></a>SpecialParamEnum.LOCATION</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p456903394615"><a name="p456903394615"></a><a name="p456903394615"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p17579141412319"><a name="p17579141412319"></a><a name="p17579141412319"></a>否</p>
</td>
</tr>
<tr id="row101911535164614"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p151911735204616"><a name="p151911735204616"></a><a name="p151911735204616"></a>获取桶存量信息</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p8578190124718"><a name="p8578190124718"></a><a name="p8578190124718"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p131921735154620"><a name="p131921735154620"></a><a name="p131921735154620"></a>SpecialParamEnum.STORAGEINFO</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1819293515466"><a name="p1819293515466"></a><a name="p1819293515466"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p105796141434"><a name="p105796141434"></a><a name="p105796141434"></a>否</p>
</td>
</tr>
<tr id="row1976635144616"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p59769351462"><a name="p59769351462"></a><a name="p59769351462"></a>设置桶配额</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p2055419154713"><a name="p2055419154713"></a><a name="p2055419154713"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p397615351461"><a name="p397615351461"></a><a name="p397615351461"></a>SpecialParamEnum.QUOTA</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p797633584620"><a name="p797633584620"></a><a name="p797633584620"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p15805141339"><a name="p15805141339"></a><a name="p15805141339"></a>否</p>
</td>
</tr>
<tr id="row207121136124618"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p127121536114614"><a name="p127121536114614"></a><a name="p127121536114614"></a>获取桶配额</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p9741618174719"><a name="p9741618174719"></a><a name="p9741618174719"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p771253611464"><a name="p771253611464"></a><a name="p771253611464"></a>SpecialParamEnum.QUOTA</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p10712123654614"><a name="p10712123654614"></a><a name="p10712123654614"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p85807141234"><a name="p85807141234"></a><a name="p85807141234"></a>否</p>
</td>
</tr>
<tr id="row11242102819462"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p5314153634518"><a name="p5314153634518"></a><a name="p5314153634518"></a>设置桶存储类型</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p155751847466"><a name="p155751847466"></a><a name="p155751847466"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p62441428164618"><a name="p62441428164618"></a><a name="p62441428164618"></a>SpecialParamEnum.STORAGEPOLICY</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1041831134615"><a name="p1041831134615"></a><a name="p1041831134615"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1742081113463"><a name="p1742081113463"></a><a name="p1742081113463"></a>否</p>
</td>
</tr>
<tr id="row144565308466"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p6802113818455"><a name="p6802113818455"></a><a name="p6802113818455"></a>获取桶存储类型</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p35811141469"><a name="p35811141469"></a><a name="p35811141469"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p747710584715"><a name="p747710584715"></a><a name="p747710584715"></a>SpecialParamEnum.STORAGEPOLICY</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p142419118465"><a name="p142419118465"></a><a name="p142419118465"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p742771112464"><a name="p742771112464"></a><a name="p742771112464"></a>否</p>
</td>
</tr>
<tr id="row1548015372463"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p94801937104611"><a name="p94801937104611"></a><a name="p94801937104611"></a>设置桶访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p20276152674710"><a name="p20276152674710"></a><a name="p20276152674710"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p18480183716460"><a name="p18480183716460"></a><a name="p18480183716460"></a>SpecialParamEnum.ACL</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p144801137184612"><a name="p144801137184612"></a><a name="p144801137184612"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p5580171417312"><a name="p5580171417312"></a><a name="p5580171417312"></a>否</p>
</td>
</tr>
<tr id="row430983894616"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1030915388464"><a name="p1030915388464"></a><a name="p1030915388464"></a>获取桶访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p929794244715"><a name="p929794244715"></a><a name="p929794244715"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p530963804612"><a name="p530963804612"></a><a name="p530963804612"></a>SpecialParamEnum.ACL</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1330993834612"><a name="p1330993834612"></a><a name="p1330993834612"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p7580181415314"><a name="p7580181415314"></a><a name="p7580181415314"></a>否</p>
</td>
</tr>
<tr id="row563782585412"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p463713254542"><a name="p463713254542"></a><a name="p463713254542"></a>开启/关闭桶日志</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p57857075913"><a name="p57857075913"></a><a name="p57857075913"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p5637142517548"><a name="p5637142517548"></a><a name="p5637142517548"></a>SpecialParamEnum.LOGGING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1163710259549"><a name="p1163710259549"></a><a name="p1163710259549"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1058010148312"><a name="p1058010148312"></a><a name="p1058010148312"></a>否</p>
</td>
</tr>
<tr id="row15750144519565"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p47503459564"><a name="p47503459564"></a><a name="p47503459564"></a>查看桶日志</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p18630183616594"><a name="p18630183616594"></a><a name="p18630183616594"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1775015456561"><a name="p1775015456561"></a><a name="p1775015456561"></a>SpecialParamEnum.LOGGING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p675064505614"><a name="p675064505614"></a><a name="p675064505614"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1470852011310"><a name="p1470852011310"></a><a name="p1470852011310"></a>否</p>
</td>
</tr>
<tr id="row234785965613"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p134715594567"><a name="p134715594567"></a><a name="p134715594567"></a>设置桶策略</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1314991525915"><a name="p1314991525915"></a><a name="p1314991525915"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1534745918563"><a name="p1534745918563"></a><a name="p1534745918563"></a>SpecialParamEnum.POLICY</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p103471759145611"><a name="p103471759145611"></a><a name="p103471759145611"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p270810201238"><a name="p270810201238"></a><a name="p270810201238"></a>否</p>
</td>
</tr>
<tr id="row130812755713"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p12308147125712"><a name="p12308147125712"></a><a name="p12308147125712"></a>查看桶策略</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p591863465915"><a name="p591863465915"></a><a name="p591863465915"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p203091372573"><a name="p203091372573"></a><a name="p203091372573"></a>SpecialParamEnum.POLICY</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1730920712572"><a name="p1730920712572"></a><a name="p1730920712572"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p117083201636"><a name="p117083201636"></a><a name="p117083201636"></a>否</p>
</td>
</tr>
<tr id="row0965113105715"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1096571325710"><a name="p1096571325710"></a><a name="p1096571325710"></a>删除桶策略</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p10360357165912"><a name="p10360357165912"></a><a name="p10360357165912"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p17965151312572"><a name="p17965151312572"></a><a name="p17965151312572"></a>SpecialParamEnum.POLICY</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p10965171355716"><a name="p10965171355716"></a><a name="p10965171355716"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p470816205310"><a name="p470816205310"></a><a name="p470816205310"></a>否</p>
</td>
</tr>
<tr id="row1751254415474"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p185129448471"><a name="p185129448471"></a><a name="p185129448471"></a>设置生命周期规则</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1422872920484"><a name="p1422872920484"></a><a name="p1422872920484"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p65124441473"><a name="p65124441473"></a><a name="p65124441473"></a>SpecialParamEnum.LIFECYCLE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p6512844114713"><a name="p6512844114713"></a><a name="p6512844114713"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p87084208310"><a name="p87084208310"></a><a name="p87084208310"></a>否</p>
</td>
</tr>
<tr id="row15369532174814"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p16799113811487"><a name="p16799113811487"></a><a name="p16799113811487"></a>查看生命周期规则</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1736917320488"><a name="p1736917320488"></a><a name="p1736917320488"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p163693326485"><a name="p163693326485"></a><a name="p163693326485"></a>SpecialParamEnum.LIFECYCLE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1536973284815"><a name="p1536973284815"></a><a name="p1536973284815"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p16708420536"><a name="p16708420536"></a><a name="p16708420536"></a>否</p>
</td>
</tr>
<tr id="row852151464913"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p20521314164910"><a name="p20521314164910"></a><a name="p20521314164910"></a>删除生命周期规则</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p01721437018"><a name="p01721437018"></a><a name="p01721437018"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1253141434912"><a name="p1253141434912"></a><a name="p1253141434912"></a>SpecialParamEnum.LIFECYCLE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p195313149494"><a name="p195313149494"></a><a name="p195313149494"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p27094201935"><a name="p27094201935"></a><a name="p27094201935"></a>否</p>
</td>
</tr>
<tr id="row81305426499"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p81301142184914"><a name="p81301142184914"></a><a name="p81301142184914"></a>设置托管配置</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p18753194945119"><a name="p18753194945119"></a><a name="p18753194945119"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p7130164224910"><a name="p7130164224910"></a><a name="p7130164224910"></a>SpecialParamEnum.WEBSITE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p713084217493"><a name="p713084217493"></a><a name="p713084217493"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1280419267318"><a name="p1280419267318"></a><a name="p1280419267318"></a>否</p>
</td>
</tr>
<tr id="row1489067185010"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1089087125020"><a name="p1089087125020"></a><a name="p1089087125020"></a>查看托管配置</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p3890678505"><a name="p3890678505"></a><a name="p3890678505"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p58919735018"><a name="p58919735018"></a><a name="p58919735018"></a>SpecialParamEnum.WEBSITE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1589297125011"><a name="p1589297125011"></a><a name="p1589297125011"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p583419263315"><a name="p583419263315"></a><a name="p583419263315"></a>否</p>
</td>
</tr>
<tr id="row1190412167508"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p8904201611500"><a name="p8904201611500"></a><a name="p8904201611500"></a>清除托管配置</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p92681052016"><a name="p92681052016"></a><a name="p92681052016"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p290491611505"><a name="p290491611505"></a><a name="p290491611505"></a>SpecialParamEnum.WEBSITE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p390481685016"><a name="p390481685016"></a><a name="p390481685016"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1883632617319"><a name="p1883632617319"></a><a name="p1883632617319"></a>否</p>
</td>
</tr>
<tr id="row1055493525016"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1255414353502"><a name="p1255414353502"></a><a name="p1255414353502"></a>设置桶多版本状态</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1956845219513"><a name="p1956845219513"></a><a name="p1956845219513"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p3554835105012"><a name="p3554835105012"></a><a name="p3554835105012"></a>SpecialParamEnum.VERSIONING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p5554735185020"><a name="p5554735185020"></a><a name="p5554735185020"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p9838726839"><a name="p9838726839"></a><a name="p9838726839"></a>否</p>
</td>
</tr>
<tr id="row184335105013"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p384365185011"><a name="p384365185011"></a><a name="p384365185011"></a>查看桶多版本状态</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p198431151145018"><a name="p198431151145018"></a><a name="p198431151145018"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p98438518509"><a name="p98438518509"></a><a name="p98438518509"></a>SpecialParamEnum.VERSIONING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p36231001235"><a name="p36231001235"></a><a name="p36231001235"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1684062618317"><a name="p1684062618317"></a><a name="p1684062618317"></a>否</p>
</td>
</tr>
<tr id="row6720257165110"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p172015713513"><a name="p172015713513"></a><a name="p172015713513"></a>设置跨域规则</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p74652518590"><a name="p74652518590"></a><a name="p74652518590"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1072045711514"><a name="p1072045711514"></a><a name="p1072045711514"></a>SpecialParamEnum.CORS</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p186261201532"><a name="p186261201532"></a><a name="p186261201532"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p168417261438"><a name="p168417261438"></a><a name="p168417261438"></a>否</p>
</td>
</tr>
<tr id="row419781435219"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p9197191413527"><a name="p9197191413527"></a><a name="p9197191413527"></a>查看跨域规则</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p12844041115912"><a name="p12844041115912"></a><a name="p12844041115912"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p019781405211"><a name="p019781405211"></a><a name="p019781405211"></a>SpecialParamEnum.CORS</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p5628904319"><a name="p5628904319"></a><a name="p5628904319"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p78437261336"><a name="p78437261336"></a><a name="p78437261336"></a>否</p>
</td>
</tr>
<tr id="row163182320521"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p54172319524"><a name="p54172319524"></a><a name="p54172319524"></a>删除跨域规则</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p15209207"><a name="p15209207"></a><a name="p15209207"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p9432385214"><a name="p9432385214"></a><a name="p9432385214"></a>SpecialParamEnum.CORS</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p162915018316"><a name="p162915018316"></a><a name="p162915018316"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p68462263311"><a name="p68462263311"></a><a name="p68462263311"></a>否</p>
</td>
</tr>
<tr id="row1728513297527"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p7285172995215"><a name="p7285172995215"></a><a name="p7285172995215"></a>设置/关闭事件通知</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1755618269598"><a name="p1755618269598"></a><a name="p1755618269598"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p162851229105219"><a name="p162851229105219"></a><a name="p162851229105219"></a>SpecialParamEnum.NOTIFICATION</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p16631101535"><a name="p16631101535"></a><a name="p16631101535"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p14848826037"><a name="p14848826037"></a><a name="p14848826037"></a>否</p>
</td>
</tr>
<tr id="row9764181818532"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p16741226185313"><a name="p16741226185313"></a><a name="p16741226185313"></a>查看事件通知</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1369817437599"><a name="p1369817437599"></a><a name="p1369817437599"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p57648187537"><a name="p57648187537"></a><a name="p57648187537"></a>SpecialParamEnum.NOTIFICATION</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p2632110435"><a name="p2632110435"></a><a name="p2632110435"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1185110266310"><a name="p1185110266310"></a><a name="p1185110266310"></a>否</p>
</td>
</tr>
<tr id="row10441845175315"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p34404515311"><a name="p34404515311"></a><a name="p34404515311"></a>设置桶标签</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p15972828195918"><a name="p15972828195918"></a><a name="p15972828195918"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p174484519536"><a name="p174484519536"></a><a name="p174484519536"></a>SpecialParamEnum.TAGGING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p14635101737"><a name="p14635101737"></a><a name="p14635101737"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p118551626637"><a name="p118551626637"></a><a name="p118551626637"></a>否</p>
</td>
</tr>
<tr id="row343535535312"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p193831758185310"><a name="p193831758185310"></a><a name="p193831758185310"></a>查看桶标签</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1868104412596"><a name="p1868104412596"></a><a name="p1868104412596"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p17436205518535"><a name="p17436205518535"></a><a name="p17436205518535"></a>SpecialParamEnum.TAGGING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p196371501634"><a name="p196371501634"></a><a name="p196371501634"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p0858182615314"><a name="p0858182615314"></a><a name="p0858182615314"></a>否</p>
</td>
</tr>
<tr id="row10837193115419"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p178371832547"><a name="p178371832547"></a><a name="p178371832547"></a>删除桶标签</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p144361111906"><a name="p144361111906"></a><a name="p144361111906"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1783723185415"><a name="p1783723185415"></a><a name="p1783723185415"></a>SpecialParamEnum.TAGGING</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p166407011312"><a name="p166407011312"></a><a name="p166407011312"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p38602269312"><a name="p38602269312"></a><a name="p38602269312"></a>否</p>
</td>
</tr>
<tr id="row550722913313"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p55076291335"><a name="p55076291335"></a><a name="p55076291335"></a>上传对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p19741165887"><a name="p19741165887"></a><a name="p19741165887"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1216511587916"><a name="p1216511587916"></a><a name="p1216511587916"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p177642421892"><a name="p177642421892"></a><a name="p177642421892"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p16881746698"><a name="p16881746698"></a><a name="p16881746698"></a>是</p>
</td>
</tr>
<tr id="row678105794610"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p134481531476"><a name="p134481531476"></a><a name="p134481531476"></a>追加上传</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p94521037473"><a name="p94521037473"></a><a name="p94521037473"></a>HttpMethodEnum.POST</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p5456331474"><a name="p5456331474"></a><a name="p5456331474"></a>SpecialParamEnum.APPEND</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1046003174710"><a name="p1046003174710"></a><a name="p1046003174710"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p746413104718"><a name="p746413104718"></a><a name="p746413104718"></a>是</p>
</td>
</tr>
<tr id="row151571118514"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p351516111650"><a name="p351516111650"></a><a name="p351516111650"></a>下载对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p1052711193815"><a name="p1052711193815"></a><a name="p1052711193815"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p168895581497"><a name="p168895581497"></a><a name="p168895581497"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p679284217914"><a name="p679284217914"></a><a name="p679284217914"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p28846461690"><a name="p28846461690"></a><a name="p28846461690"></a>是</p>
</td>
</tr>
<tr id="row11126525555"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p212620257516"><a name="p212620257516"></a><a name="p212620257516"></a>复制对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p33401228789"><a name="p33401228789"></a><a name="p33401228789"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p131397121013"><a name="p131397121013"></a><a name="p131397121013"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p4794442798"><a name="p4794442798"></a><a name="p4794442798"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p38861146590"><a name="p38861146590"></a><a name="p38861146590"></a>是</p>
</td>
</tr>
<tr id="row938611301253"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p43873301459"><a name="p43873301459"></a><a name="p43873301459"></a>删除对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p125999297812"><a name="p125999297812"></a><a name="p125999297812"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p840651721016"><a name="p840651721016"></a><a name="p840651721016"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p679616421493"><a name="p679616421493"></a><a name="p679616421493"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p198899460918"><a name="p198899460918"></a><a name="p198899460918"></a>是</p>
</td>
</tr>
<tr id="row1864113411519"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p186421634453"><a name="p186421634453"></a><a name="p186421634453"></a>批量删除对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p182757371984"><a name="p182757371984"></a><a name="p182757371984"></a>HttpMethodEnum.POST</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p136425341451"><a name="p136425341451"></a><a name="p136425341451"></a>SpecialParamEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1797842495"><a name="p1797842495"></a><a name="p1797842495"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p16892194611911"><a name="p16892194611911"></a><a name="p16892194611911"></a>是</p>
</td>
</tr>
<tr id="row29757399512"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p497511397519"><a name="p497511397519"></a><a name="p497511397519"></a>获取对象属性</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p125232040087"><a name="p125232040087"></a><a name="p125232040087"></a>HttpMethodEnum.HEAD</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p053212481016"><a name="p053212481016"></a><a name="p053212481016"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p8800242895"><a name="p8800242895"></a><a name="p8800242895"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p389417460914"><a name="p389417460914"></a><a name="p389417460914"></a>是</p>
</td>
</tr>
<tr id="row181781248959"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p21787484510"><a name="p21787484510"></a><a name="p21787484510"></a>设置对象访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p19421644888"><a name="p19421644888"></a><a name="p19421644888"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p81783481153"><a name="p81783481153"></a><a name="p81783481153"></a>SpecialParamEnum.ACL</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p10802204218913"><a name="p10802204218913"></a><a name="p10802204218913"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p168961146698"><a name="p168961146698"></a><a name="p168961146698"></a>是</p>
</td>
</tr>
<tr id="row1241141618619"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1541116162614"><a name="p1541116162614"></a><a name="p1541116162614"></a>查看对象访问权限</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p2193104616810"><a name="p2193104616810"></a><a name="p2193104616810"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p541116166620"><a name="p541116166620"></a><a name="p541116166620"></a>SpecialParamEnum.ACL</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p5804842398"><a name="p5804842398"></a><a name="p5804842398"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p789918469917"><a name="p789918469917"></a><a name="p789918469917"></a>是</p>
</td>
</tr>
<tr id="row1221613237611"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p12216172314618"><a name="p12216172314618"></a><a name="p12216172314618"></a>初始化分段上传任务</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p03025317815"><a name="p03025317815"></a><a name="p03025317815"></a>HttpMethodEnum.POST</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1821615231769"><a name="p1821615231769"></a><a name="p1821615231769"></a>SpecialParamEnum.UPLOADS</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p38065421196"><a name="p38065421196"></a><a name="p38065421196"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p09018461998"><a name="p09018461998"></a><a name="p09018461998"></a>是</p>
</td>
</tr>
<tr id="row15957123218619"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p1958173220617"><a name="p1958173220617"></a><a name="p1958173220617"></a>上传段</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p18952356485"><a name="p18952356485"></a><a name="p18952356485"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p11958143217612"><a name="p11958143217612"></a><a name="p11958143217612"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p14807042196"><a name="p14807042196"></a><a name="p14807042196"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p4904204615913"><a name="p4904204615913"></a><a name="p4904204615913"></a>是</p>
</td>
</tr>
<tr id="row1936493913613"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p03644391562"><a name="p03644391562"></a><a name="p03644391562"></a>复制段</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p4669133693"><a name="p4669133693"></a><a name="p4669133693"></a>HttpMethodEnum.PUT</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p16364173912611"><a name="p16364173912611"></a><a name="p16364173912611"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p580994217914"><a name="p580994217914"></a><a name="p580994217914"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p89073461295"><a name="p89073461295"></a><a name="p89073461295"></a>是</p>
</td>
</tr>
<tr id="row88561144369"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p68578446613"><a name="p68578446613"></a><a name="p68578446613"></a>列举已上传的段</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p353765190"><a name="p353765190"></a><a name="p353765190"></a>HttpMethodEnum.GET</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p108573441969"><a name="p108573441969"></a><a name="p108573441969"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p9811204217915"><a name="p9811204217915"></a><a name="p9811204217915"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p209091461495"><a name="p209091461495"></a><a name="p209091461495"></a>是</p>
</td>
</tr>
<tr id="row649695218617"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p049685220618"><a name="p049685220618"></a><a name="p049685220618"></a>合并段</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p89410126919"><a name="p89410126919"></a><a name="p89410126919"></a>HttpMethodEnum.POST</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p849718521267"><a name="p849718521267"></a><a name="p849718521267"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p17814164215918"><a name="p17814164215918"></a><a name="p17814164215918"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p191113461191"><a name="p191113461191"></a><a name="p191113461191"></a>是</p>
</td>
</tr>
<tr id="row14913195611611"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p8913195613615"><a name="p8913195613615"></a><a name="p8913195613615"></a>取消分段上传任务</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p12628815193"><a name="p12628815193"></a><a name="p12628815193"></a>HttpMethodEnum.DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p1591317561863"><a name="p1591317561863"></a><a name="p1591317561863"></a>N/A</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p2816842493"><a name="p2816842493"></a><a name="p2816842493"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p1991416461391"><a name="p1991416461391"></a><a name="p1991416461391"></a>是</p>
</td>
</tr>
<tr id="row179724910718"><td class="cellrowborder" valign="top" width="18.08%" headers="mcps1.1.6.1.1 "><p id="p29731692714"><a name="p29731692714"></a><a name="p29731692714"></a>取回归档存储对象</p>
</td>
<td class="cellrowborder" valign="top" width="26.919999999999998%" headers="mcps1.1.6.1.2 "><p id="p71517295913"><a name="p71517295913"></a><a name="p71517295913"></a>HttpMethodEnum.POST</p>
</td>
<td class="cellrowborder" valign="top" width="28.000000000000004%" headers="mcps1.1.6.1.3 "><p id="p15973179976"><a name="p15973179976"></a><a name="p15973179976"></a>SpecialParamEnum.RESTORE</p>
</td>
<td class="cellrowborder" valign="top" width="13%" headers="mcps1.1.6.1.4 "><p id="p1882004211910"><a name="p1882004211910"></a><a name="p1882004211910"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="14.000000000000002%" headers="mcps1.1.6.1.5 "><p id="p109191465919"><a name="p109191465919"></a><a name="p109191465919"></a>是</p>
</td>
</tr>
</tbody>
</table>

通过OBS Java SDK生成临时URL访问OBS的步骤如下：

1.  通过ObsClient.createTemporarySignature生成带签名信息的URL。
2.  使用任意HTTP库发送HTTP/HTTPS请求，访问OBS服务。

>![](public_sys-resources/icon-caution.gif) **注意：** 
>如果遇到跨域报错、签名不匹配问题，请参考以下步骤排查问题：
>1.  未配置跨域，需要在控制台配置CORS规则，请参考[配置桶允许跨域请求](https://support.huaweicloud.com/sdk-browserjs-devg-obs/obs_24_0107.html)。
>2.  签名计算问题，请参考[URL中携带签名](https://support.huaweicloud.com/api-obs/obs_04_0011.html)排查签名参数是否正确；比如上传对象功能，后端将Content-Type参与计算签名生成授权URL，但是前端使用授权URL时没有设置Content-Type字段或者传入错误的值，此时会出现跨域错误。解决方案为：Content-Type字段前后端保持一致。

以下代码展示了如何使用临时URL进行授权访问，包括：创建桶、上传对象、下载对象、列举对象、删除对象。

## 创建桶<a name="section8517109534"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
request.setBucketName("bucketname");
TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
System.out.println("Creating bucket using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());

Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}
// 使用PUT请求创建桶
String location = "your bucket location";
Request httpRequest = builder.url(response.getSignedUrl()).put(RequestBody.create(null, "<CreateBucketConfiguration><Location>" + location + "</Location></CreateBucketConfiguration>".getBytes())).build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 上传对象<a name="section1057571281111"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;

Map<String, String> headers = new HashMap<String, String>();
String contentType = "text/plain";
headers.put("Content-Type", contentType);

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");
request.setHeaders(headers);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("Creating object using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());
Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用PUT请求上传对象
Request httpRequest = builder.url(response.getSignedUrl()).put(RequestBody.create(MediaType.parse(contentType), "Hello OBS".getBytes("UTF-8"))).build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 下载对象<a name="section1382216339118"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;


TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("Getting object using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());
Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用GET请求下载对象
Request httpRequest = builder.url(response.getSignedUrl()).get().build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 列举对象<a name="section20628113717110"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;


TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
request.setBucketName("bucketname");

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("Getting object list using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());
Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用GET请求获取对象列表
Request httpRequest = builder.url(response.getSignedUrl()).get().build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 删除对象<a name="section0796203914111"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;


TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.DELETE, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("Deleting object using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());
Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用DELETE删除对象
Request httpRequest = builder.url(response.getSignedUrl()).delete().build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 初始化分段上传任务<a name="section57571639329"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.POST, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");
request.setSpecialParam(SpecialParamEnum.UPLOADS);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("initiate multipart upload using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());

Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用POST请求初始化分段上传任务
Request httpRequest = builder.url(response.getSignedUrl()).post(RequestBody.create(null, "")).build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 上传段<a name="section43006123611"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");

Map<String, Object> queryParams = new HashMap<String, Object>();
// 设置partNumber请求参数，例如：queryParams.put("partNumber", "1");
queryParams.put("partNumber", "partNumber");
queryParams.put("uploadId", "your uploadId");

request.setQueryParams(queryParams);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("upload part using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());

Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用PUT请求上传段
Request httpRequest = builder.url(response.getSignedUrl()).put(RequestBody.create(null, new byte[6 * 1024 * 1024])).build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 列举已上传段<a name="section14449204412281"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");

Map<String, Object> queryParams = new HashMap<String, Object>();
queryParams.put("uploadId", "your uploadId");
request.setQueryParams(queryParams);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("list parts using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());

Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用GET请求列举已上传段
Request httpRequest = builder.url(response.getSignedUrl()).get().build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 合并段<a name="section27861832937"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.POST, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");

Map<String, String> headers = new HashMap<String, String>();
String contentType = "application/xml";
headers.put("Content-Type", contentType);
request.setHeaders(headers);

Map<String, Object> queryParams = new HashMap<String, Object>();
queryParams.put("uploadId", "your uploadId");
request.setQueryParams(queryParams);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("complete multipart upload using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());

Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

// 以下content为示例代码，需要通过列举已上传段方法的响应结果，拼装以下内容
String content = "<CompleteMultipartUpload>";
content += "<Part>";
content += "<PartNumber>1</PartNumber>";
content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
content += "</Part>";
content += "<Part>";
content += "<PartNumber>2</PartNumber>";
content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
content += "</Part>";
content += "</CompleteMultipartUpload>";

//使用POST请求合并段
Request httpRequest = builder.url(response.getSignedUrl()).post(RequestBody.create(MediaType.parse(contentType), content.getBytes("UTF-8"))).build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

## 获取图片转码的下载链接<a name="section112801918071"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// URL有效期，3600秒
long expireSeconds = 3600L;


TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");

// 设置图片转码参数

Map<String,Object> queryParams = new HashMap<String, Object>();
queryParams.put("x-image-process", "image/resize,m_fixed,w_100,h_100/rotate,100");
request.setQueryParams(queryParams);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
//获取支持图片转码的下载链接
System.out.println("Getting object using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());
res.close();
```

## 下载SSE-C加密类型的对象<a name="section195111828105617"></a>

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

ObsConfiguration config = new ObsConfiguration();
config.setSocketTimeout(30000);
config.setConnectionTimeout(10000);
config.setEndPoint(endPoint);
// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, config);
// URL有效期，3600秒
long expireSeconds = 3600L;

TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
request.setBucketName("bucketname");
request.setObjectKey("objectname");
// 设置SSE-C加密方式的头域信息
Map<String, String> headers = new HashMap<String, String>();
headers.put("x-obs-server-side-encryption-customer-algorithm", "AES256");
// 设置加密使用的密钥，该头域由256-bit的密钥经过base64-encoded得到
headers.put("x-obs-server-side-encryption-customer-key", "your base64 sse-c key generated by AES-256 algorithm");
// 设置加密使用的密钥的MD5值，该头域由密钥的128-bit MD5值经过base64-encoded得到
headers.put("x-obs-server-side-encryption-customer-key-MD5", "the md5 value of your sse-c key");
request.setHeaders(headers);

TemporarySignatureResponse response = obsClient.createTemporarySignature(request);

System.out.println("Getting object using temporary signature url:");
System.out.println("\t" + response.getSignedUrl());
Request.Builder builder = new Request.Builder();
for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
       builder.header(entry.getKey(), entry.getValue());
}

//使用GET请求下载对象
Request httpRequest = builder.url(response.getSignedUrl()).get().build();
OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
              .cache(null).build();

Call c = httpClient.newCall(httpRequest);
Response res = c.execute();
System.out.println("\tStatus:" + res.code());
if (res.body() != null) {
       System.out.println("\tContent:" + res.body().string() + "\n");
}
res.close();
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   HttpMethodEnum是OBS Java SDK定义的枚举类型，代表请求方法类型。
>-   加密秘钥的计算方式，可以参考章节：[如何生成SSE-C方式的加密秘钥](如何生成SSE-C方式的加密秘钥.md)。

