# OBS资源<a name="obs_03_0154"></a>

资源是服务中存在的对象。在OBS中，资源包括桶和对象。您可以在创建自定义策略时，通过指定资源路径来选择特定资源。

**表 1**  OBS的指定资源与对应路径

<a name="table43915131423"></a>
<table><thead align="left"><tr id="row93928131522"><th class="cellrowborder" valign="top" width="15.091509150915092%" id="mcps1.2.4.1.1"><p id="p73922131924"><a name="p73922131924"></a><a name="p73922131924"></a>资源类型</p>
</th>
<th class="cellrowborder" valign="top" width="16.8016801680168%" id="mcps1.2.4.1.2"><p id="p1139261314216"><a name="p1139261314216"></a><a name="p1139261314216"></a>资源名称</p>
</th>
<th class="cellrowborder" valign="top" width="68.10681068106811%" id="mcps1.2.4.1.3"><p id="p23920131721"><a name="p23920131721"></a><a name="p23920131721"></a>资源路径</p>
</th>
</tr>
</thead>
<tbody><tr id="row139215131224"><td class="cellrowborder" valign="top" width="15.091509150915092%" headers="mcps1.2.4.1.1 "><p id="p1839219131525"><a name="p1839219131525"></a><a name="p1839219131525"></a>bucket</p>
</td>
<td class="cellrowborder" valign="top" width="16.8016801680168%" headers="mcps1.2.4.1.2 "><p id="p203927136213"><a name="p203927136213"></a><a name="p203927136213"></a>桶</p>
</td>
<td class="cellrowborder" valign="top" width="68.10681068106811%" headers="mcps1.2.4.1.3 "><p id="p4392013822"><a name="p4392013822"></a><a name="p4392013822"></a><span>【格式】</span></p>
<p id="p9933155311298"><a name="p9933155311298"></a><a name="p9933155311298"></a><span>obs:*:*:bucket:</span><em id="i10194628103313"><a name="i10194628103313"></a><a name="i10194628103313"></a>桶名称</em></p>
<p id="p14703335307"><a name="p14703335307"></a><a name="p14703335307"></a>【说明】</p>
<p id="p9142175873014"><a name="p9142175873014"></a><a name="p9142175873014"></a>对于桶资源，IAM自动生成资源路径前缀<strong id="b19141342315"><a name="b19141342315"></a><a name="b19141342315"></a>obs:*:*:bucket:</strong></p>
<p id="p17463217363"><a name="p17463217363"></a><a name="p17463217363"></a>通过<em id="i27493223610"><a name="i27493223610"></a><a name="i27493223610"></a>桶名称</em>指定具体的资源路径，支持通配符*。例如：</p>
<p id="p129731439193114"><a name="p129731439193114"></a><a name="p129731439193114"></a><strong id="b1226312278384"><a name="b1226312278384"></a><a name="b1226312278384"></a>obs:*:*:bucket:*</strong>表示任意OBS桶。</p>
</td>
</tr>
<tr id="row83923131421"><td class="cellrowborder" valign="top" width="15.091509150915092%" headers="mcps1.2.4.1.1 "><p id="p539218132026"><a name="p539218132026"></a><a name="p539218132026"></a>object</p>
</td>
<td class="cellrowborder" valign="top" width="16.8016801680168%" headers="mcps1.2.4.1.2 "><p id="p539251316215"><a name="p539251316215"></a><a name="p539251316215"></a>对象</p>
</td>
<td class="cellrowborder" valign="top" width="68.10681068106811%" headers="mcps1.2.4.1.3 "><p id="p325619913310"><a name="p325619913310"></a><a name="p325619913310"></a><span>【格式】</span></p>
<p id="p1925689183116"><a name="p1925689183116"></a><a name="p1925689183116"></a><span>obs:*:*:object:</span><em id="i4568022183515"><a name="i4568022183515"></a><a name="i4568022183515"></a>桶名称/对象名称</em></p>
<p id="p182561698314"><a name="p182561698314"></a><a name="p182561698314"></a>【说明】</p>
<p id="p770393763415"><a name="p770393763415"></a><a name="p770393763415"></a>对于对象资源，IAM自动生成资源路径前缀<strong id="b13411134633413"><a name="b13411134633413"></a><a name="b13411134633413"></a>obs:*:*:object:</strong></p>
<p id="p181983113519"><a name="p181983113519"></a><a name="p181983113519"></a>通过<em id="i17951155015352"><a name="i17951155015352"></a><a name="i17951155015352"></a>桶名称/对象名称</em>指定具体的资源路径，支持通配符*。例如：</p>
<p id="p161341247133614"><a name="p161341247133614"></a><a name="p161341247133614"></a><strong id="b768272223816"><a name="b768272223816"></a><a name="b768272223816"></a>obs:*:*:object:my-bucket/my-object/*</strong>表示my-bucket桶下my-object目录下的任意对象。</p>
</td>
</tr>
</tbody>
</table>

