# API概览<a name="ZH-CN_TOPIC_0100846747"></a>

## 桶基础操作接口<a name="section23599591419"></a>

**表 1**  桶基础操作接口

<a name="table1255720201424"></a>
<table><thead align="left"><tr id="row3576720428"><th class="cellrowborder" valign="top" width="39.61%" id="mcps1.2.3.1.1"><p id="p659812206210"><a name="p659812206210"></a><a name="p659812206210"></a>接口</p>
</th>
<th class="cellrowborder" valign="top" width="60.39%" id="mcps1.2.3.1.2"><p id="p27521233191612"><a name="p27521233191612"></a><a name="p27521233191612"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row136091220422"><td class="cellrowborder" valign="top" width="39.61%" headers="mcps1.2.3.1.1 "><p id="p3618142011217"><a name="p3618142011217"></a><a name="p3618142011217"></a><a href="获取桶列表.md">获取桶列表</a></p>
</td>
<td class="cellrowborder" valign="top" width="60.39%" headers="mcps1.2.3.1.2 "><p id="p575353312164"><a name="p575353312164"></a><a name="p575353312164"></a>查询自己创建的桶列表。</p>
</td>
</tr>
<tr id="row162814201210"><td class="cellrowborder" valign="top" width="39.61%" headers="mcps1.2.3.1.1 "><p id="p463782010220"><a name="p463782010220"></a><a name="p463782010220"></a><a href="创建桶.md">创建桶</a></p>
</td>
<td class="cellrowborder" valign="top" width="60.39%" headers="mcps1.2.3.1.2 "><p id="p675343311164"><a name="p675343311164"></a><a name="p675343311164"></a>创建一个新桶。可以在创建时添加不同的请求消息头来指定桶的区域、权限控制策略、存储类型等信息。</p>
</td>
</tr>
<tr id="row16642920222"><td class="cellrowborder" valign="top" width="39.61%" headers="mcps1.2.3.1.1 "><p id="p126521620523"><a name="p126521620523"></a><a name="p126521620523"></a><a href="列举桶内对象.md">列举桶内对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="60.39%" headers="mcps1.2.3.1.2 "><p id="p117534339163"><a name="p117534339163"></a><a name="p117534339163"></a>获取桶内对象列表。可以在创建时添加不同的请求消息头来获取符合指定前缀、标识符等要求的对象。</p>
</td>
</tr>
<tr id="row15656520821"><td class="cellrowborder" valign="top" width="39.61%" headers="mcps1.2.3.1.1 "><p id="p7666520126"><a name="p7666520126"></a><a name="p7666520126"></a><a href="获取桶元数据.md">获取桶元数据</a></p>
</td>
<td class="cellrowborder" valign="top" width="60.39%" headers="mcps1.2.3.1.2 "><p id="p175383321619"><a name="p175383321619"></a><a name="p175383321619"></a>查询桶元数据是否存在。可以查询桶的区域、存储类型、OBS服务版本号、企业项目id、CORS配置等信息。</p>
</td>
</tr>
<tr id="row1669020726"><td class="cellrowborder" valign="top" width="39.61%" headers="mcps1.2.3.1.1 "><p id="p196825201627"><a name="p196825201627"></a><a name="p196825201627"></a><a href="获取桶区域位置.md">获取桶区域位置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60.39%" headers="mcps1.2.3.1.2 "><p id="p147531633171617"><a name="p147531633171617"></a><a name="p147531633171617"></a>获取桶区域位置信息。</p>
</td>
</tr>
<tr id="row9685320623"><td class="cellrowborder" valign="top" width="39.61%" headers="mcps1.2.3.1.1 "><p id="p669612015212"><a name="p669612015212"></a><a name="p669612015212"></a><a href="删除桶.md">删除桶</a></p>
</td>
<td class="cellrowborder" valign="top" width="60.39%" headers="mcps1.2.3.1.2 "><p id="p1375316339165"><a name="p1375316339165"></a><a name="p1375316339165"></a>删除指定的桶。删除之前需要确保桶内无对象。</p>
</td>
</tr>
</tbody>
</table>

## 桶高级配置接口<a name="section222510319219"></a>

**表 2**  桶高级配置接口

<a name="table21787787"></a>
<table><thead align="left"><tr id="row11729601"><th class="cellrowborder" valign="top" width="40%" id="mcps1.2.3.1.1"><p id="p51157822"><a name="p51157822"></a><a name="p51157822"></a>接口</p>
</th>
<th class="cellrowborder" valign="top" width="60%" id="mcps1.2.3.1.2"><p id="p163114411185"><a name="p163114411185"></a><a name="p163114411185"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row50142950"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p20245582"><a name="p20245582"></a><a name="p20245582"></a><a href="设置桶策略.md">设置桶策略</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p19398145175212"><a name="p19398145175212"></a><a name="p19398145175212"></a>创建或者修改一个桶的策略。如果桶已经存在一个策略，那么当前请求中的策略将完全覆盖桶中现存的策略。</p>
</td>
</tr>
<tr id="row47992515"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p4104320"><a name="p4104320"></a><a name="p4104320"></a><a href="获取桶策略.md">获取桶策略</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p2318471813"><a name="p2318471813"></a><a name="p2318471813"></a>获取指定桶的策略信息。</p>
</td>
</tr>
<tr id="row36938882"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p25902344"><a name="p25902344"></a><a name="p25902344"></a><a href="删除桶策略.md">删除桶策略</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p203154101814"><a name="p203154101814"></a><a name="p203154101814"></a>删除一个指定桶上的策略。</p>
</td>
</tr>
<tr id="row31794505"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p29399851"><a name="p29399851"></a><a name="p29399851"></a><a href="设置桶ACL.md">设置桶ACL</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p43314414187"><a name="p43314414187"></a><a name="p43314414187"></a>设置一个指定桶的ACL信息。通过ACL可以控制桶的读写权限。</p>
</td>
</tr>
<tr id="row63272067"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p59713398"><a name="p59713398"></a><a name="p59713398"></a><a href="获取桶ACL.md">获取桶ACL</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p14335481815"><a name="p14335481815"></a><a name="p14335481815"></a>获取一个指定桶的ACL信息。</p>
</td>
</tr>
<tr id="row549671"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p49625342"><a name="p49625342"></a><a name="p49625342"></a><a href="设置桶日志管理配置.md">设置桶日志管理配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p93312419189"><a name="p93312419189"></a><a name="p93312419189"></a>开启或关闭桶的日志管理功能。开启后，桶的每次操作将会产生一条日志，并将多条日志打包成一个日志文件存放在指定的位置。</p>
</td>
</tr>
<tr id="row43974897"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p18295456"><a name="p18295456"></a><a name="p18295456"></a><a href="获取桶日志管理配置.md">获取桶日志管理配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p12332481814"><a name="p12332481814"></a><a name="p12332481814"></a>获取指定桶的日志管理配置信息。</p>
</td>
</tr>
<tr id="row461412618318"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p146159261310"><a name="p146159261310"></a><a name="p146159261310"></a><a href="设置桶的生命周期配置.md">设置桶的生命周期配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p1633748182"><a name="p1633748182"></a><a name="p1633748182"></a>指定规则来实现定时删除或迁移桶中对象。</p>
</td>
</tr>
<tr id="row5886350183216"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p1188810501325"><a name="p1188810501325"></a><a name="p1188810501325"></a><a href="获取桶的生命周期配置.md">获取桶的生命周期配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p333154191816"><a name="p333154191816"></a><a name="p333154191816"></a>获取指定桶已配置的生命周期规则。</p>
</td>
</tr>
<tr id="row49401830133618"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p694013043619"><a name="p694013043619"></a><a name="p694013043619"></a><a href="删除桶的生命周期配置.md">删除桶的生命周期配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p13331344183"><a name="p13331344183"></a><a name="p13331344183"></a>删除指定桶的生命周期配置信息。</p>
</td>
</tr>
<tr id="row30441382"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p9930306"><a name="p9930306"></a><a name="p9930306"></a><a href="设置桶的多版本状态.md">设置桶的多版本状态</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p13313411814"><a name="p13313411814"></a><a name="p13313411814"></a>开启或暂停桶的多版本功能。开启后，可以检索和还原各个版本的对象，在意外操作或应用程序故障时快速恢复数据。</p>
</td>
</tr>
<tr id="row22263891"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p44503567"><a name="p44503567"></a><a name="p44503567"></a><a href="获取桶的多版本状态.md">获取桶的多版本状态</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p933343189"><a name="p933343189"></a><a name="p933343189"></a>获取指定桶的多版本功能状态。</p>
</td>
</tr>
<tr id="row979014491077"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p2067152785"><a name="p2067152785"></a><a name="p2067152785"></a><a href="设置桶的消息通知配置.md">设置桶的消息通知配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p17339401817"><a name="p17339401817"></a><a name="p17339401817"></a>设置桶的消息通知功能，安全、及时的了解发生在桶上的关键事件。</p>
</td>
</tr>
<tr id="row64987789"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p42274750"><a name="p42274750"></a><a name="p42274750"></a><a href="获取桶的消息通知配置.md">获取桶的消息通知配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p43313471818"><a name="p43313471818"></a><a name="p43313471818"></a>获取指定桶的消息通知配置信息。</p>
</td>
</tr>
<tr id="row44928433"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p33324491"><a name="p33324491"></a><a name="p33324491"></a><a href="设置桶默认存储类型.md">设置桶默认存储类型</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p173334111817"><a name="p173334111817"></a><a name="p173334111817"></a>创建或更新桶的默认存储类型配置信息。</p>
</td>
</tr>
<tr id="row31484965"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p11774651"><a name="p11774651"></a><a name="p11774651"></a><a href="获取桶默认存储类型.md">获取桶默认存储类型</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p63334141820"><a name="p63334141820"></a><a name="p63334141820"></a>获取桶的默认存储类型配置信息。</p>
</td>
</tr>
<tr id="row38862996"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p33548891"><a name="p33548891"></a><a name="p33548891"></a><a href="设置桶的跨区域复制配置.md">设置桶的跨区域复制配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p733154121819"><a name="p733154121819"></a><a name="p733154121819"></a>设置桶的跨区域复制功能。<span>通过激活跨区域复制，OBS可将新创建的对象及修改的对象从一个源桶复制到不同区域中的目标桶。</span></p>
</td>
</tr>
<tr id="row33504565"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p41925888"><a name="p41925888"></a><a name="p41925888"></a><a href="获取桶的跨区域复制配置.md">获取桶的跨区域复制配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p11331411184"><a name="p11331411184"></a><a name="p11331411184"></a>获取指定桶的跨区域复制配置信息。</p>
</td>
</tr>
<tr id="row1149592412327"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p2925172593216"><a name="p2925172593216"></a><a name="p2925172593216"></a><a href="删除桶的跨区域复制配置.md">删除桶的跨区域复制配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p103384161815"><a name="p103384161815"></a><a name="p103384161815"></a>删除指定桶的跨区域复制配置信息。</p>
</td>
</tr>
<tr id="row293325416321"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p4935115411325"><a name="p4935115411325"></a><a name="p4935115411325"></a><a href="设置桶标签.md">设置桶标签</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p233104181813"><a name="p233104181813"></a><a name="p233104181813"></a>添加标签至一个已存在的桶。<span>为桶添加标签后，该桶上所有请求产生的计费话单里都会带上这些标签，从而可以针对话单报表做分类筛选，进行更详细的成本分析。</span></p>
</td>
</tr>
<tr id="row16359036133610"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p15359123613616"><a name="p15359123613616"></a><a name="p15359123613616"></a><a href="获取桶标签.md">获取桶标签</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p933164141812"><a name="p933164141812"></a><a name="p933164141812"></a>获取指定桶的标签。</p>
</td>
</tr>
<tr id="row41788676"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p35797191"><a name="p35797191"></a><a name="p35797191"></a><a href="删除桶标签.md">删除桶标签</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p23313416184"><a name="p23313416184"></a><a name="p23313416184"></a>删除指定桶的标签。</p>
</td>
</tr>
<tr id="row53739270"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p60490966"><a name="p60490966"></a><a name="p60490966"></a><a href="设置桶配额.md">设置桶配额</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p23314417181"><a name="p23314417181"></a><a name="p23314417181"></a>设置桶的空间配额，用以限制桶的最大存储容量。</p>
</td>
</tr>
<tr id="row1728134011366"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p11282184017369"><a name="p11282184017369"></a><a name="p11282184017369"></a><a href="获取桶配额.md">获取桶配额</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p1133840184"><a name="p1133840184"></a><a name="p1133840184"></a>获取桶的空间配额。</p>
</td>
</tr>
<tr id="row93371813141816"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p47704802516"><a name="p47704802516"></a><a name="p47704802516"></a><a href="获取桶存量信息.md">获取桶存量信息</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p1833144131810"><a name="p1833144131810"></a><a name="p1833144131810"></a>获取桶中的对象个数及对象占用空间。</p>
</td>
</tr>
<tr id="row671581513918"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p171661510393"><a name="p171661510393"></a><a name="p171661510393"></a><a href="设置桶清单.md">设置桶清单</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p07169158390"><a name="p07169158390"></a><a name="p07169158390"></a>为一个桶配置清单规则。桶清单可以用来帮助您管理桶内对象，它可以定期列举桶内对象，并将对象元数据的相关信息保存在CSV格式的文件中，上传到您指定的桶中。</p>
</td>
</tr>
<tr id="row198981329183914"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p38981329113912"><a name="p38981329113912"></a><a name="p38981329113912"></a><a href="获取桶清单.md">获取桶清单</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p14898429193916"><a name="p14898429193916"></a><a name="p14898429193916"></a>获取指定桶的某个清单规则。</p>
</td>
</tr>
<tr id="row828195163913"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p11281551123914"><a name="p11281551123914"></a><a name="p11281551123914"></a><a href="列举桶清单.md">列举桶清单</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p10281451113910"><a name="p10281451113910"></a><a name="p10281451113910"></a>获取指定桶的所有清单规则。</p>
</td>
</tr>
<tr id="row1122449183910"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p2123154983916"><a name="p2123154983916"></a><a name="p2123154983916"></a><a href="删除桶清单.md">删除桶清单</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p112316495391"><a name="p112316495391"></a><a name="p112316495391"></a>删除指定桶的某个清单规则。</p>
</td>
</tr>
<tr id="row17362143213398"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p10362332203918"><a name="p10362332203918"></a><a name="p10362332203918"></a><a href="设置桶的自定义域名.md">设置桶的自定义域名</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p736283212397"><a name="p736283212397"></a><a name="p736283212397"></a>为桶设置自定义域名。<span>设置成功之后，用户可以通过桶的自定义域名访问桶。</span></p>
</td>
</tr>
<tr id="row1620363515398"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p22031435153916"><a name="p22031435153916"></a><a name="p22031435153916"></a><a href="获取桶的自定义域名.md">获取桶的自定义域名</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p6203173517390"><a name="p6203173517390"></a><a name="p6203173517390"></a>查询桶已设置的自定义域名。</p>
</td>
</tr>
<tr id="row1884093953912"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p11840143953915"><a name="p11840143953915"></a><a name="p11840143953915"></a><a href="删除桶的自定义域名.md">删除桶的自定义域名</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p1884053916398"><a name="p1884053916398"></a><a name="p1884053916398"></a>删除桶已设置的自定义域名。</p>
</td>
</tr>
<tr id="row14569184217390"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p657015421395"><a name="p657015421395"></a><a name="p657015421395"></a><a href="设置桶的加密配置.md">设置桶的加密配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p199653120135"><a name="p199653120135"></a><a name="p199653120135"></a>为桶创建或更新默认服务端加密配置信息。设置桶加密配置后，在该桶中上传对象时，会采用桶的默认加密配置对数据进行加密。</p>
</td>
</tr>
<tr id="row31612477390"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p11664714393"><a name="p11664714393"></a><a name="p11664714393"></a><a href="获取桶的加密配置.md">获取桶的加密配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p7166472397"><a name="p7166472397"></a><a name="p7166472397"></a>查询桶的默认服务端加密配置信息。</p>
</td>
</tr>
<tr id="row4195192718395"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p2195162793919"><a name="p2195162793919"></a><a name="p2195162793919"></a><a href="删除桶的加密配置.md">删除桶的加密配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p1319516275397"><a name="p1319516275397"></a><a name="p1319516275397"></a>删除桶的默认服务端加密配置信息。</p>
</td>
</tr>
<tr id="row618812407575"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p15189134015571"><a name="p15189134015571"></a><a name="p15189134015571"></a><a href="设置桶归档对象直读策略.md">设置桶归档对象直读策略</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p7837122112711"><a name="p7837122112711"></a><a name="p7837122112711"></a>开启或关闭桶的归档对象直读功能。开启后，归档对象不需要取回便可以直接下载。</p>
</td>
</tr>
<tr id="row5426345175713"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p20426154510579"><a name="p20426154510579"></a><a name="p20426154510579"></a><a href="获取桶归档对象直读策略.md">获取桶归档对象直读策略</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p84261145145713"><a name="p84261145145713"></a><a name="p84261145145713"></a>获取指定桶的归档对象直读状态。</p>
</td>
</tr>
<tr id="row29631342125711"><td class="cellrowborder" valign="top" width="40%" headers="mcps1.2.3.1.1 "><p id="p7963442125715"><a name="p7963442125715"></a><a name="p7963442125715"></a><a href="删除桶归档对象直读策略.md">删除桶归档对象直读策略</a></p>
</td>
<td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.3.1.2 "><p id="p8963174210578"><a name="p8963174210578"></a><a name="p8963174210578"></a>删除指定桶的归档对象直读配置信息。</p>
</td>
</tr>
</tbody>
</table>

## 静态网站托管接口<a name="section13506949424"></a>

**表 3**  静态网站托管接口

<a name="table19980316"></a>
<table><thead align="left"><tr id="row61781656"><th class="cellrowborder" valign="top" width="40.5%" id="mcps1.2.3.1.1"><p id="p11912107"><a name="p11912107"></a><a name="p11912107"></a>接口</p>
</th>
<th class="cellrowborder" valign="top" width="59.5%" id="mcps1.2.3.1.2"><p id="p1310420962620"><a name="p1310420962620"></a><a name="p1310420962620"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row25356585"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p1680854"><a name="p1680854"></a><a name="p1680854"></a><a href="设置桶的网站配置.md">设置桶的网站配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p17104149102614"><a name="p17104149102614"></a><a name="p17104149102614"></a>创建或更新桶的网站配置信息。<span>OBS允许在桶内保存静态的网页资源，如.html网页文件、flash文件、音视频文件等，当客户端通过桶的Website接入点访问这些对象资源时，浏览器可以直接解析出这些支持的网页资源，呈现给最终用户。</span></p>
</td>
</tr>
<tr id="row15127689"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p65870035"><a name="p65870035"></a><a name="p65870035"></a><a href="获取桶的网站配置.md">获取桶的网站配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p1210413922613"><a name="p1210413922613"></a><a name="p1210413922613"></a>获取桶的网站配置信息。</p>
</td>
</tr>
<tr id="row55959406"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p64177416"><a name="p64177416"></a><a name="p64177416"></a><a href="删除桶的网站配置.md">删除桶的网站配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p110419122619"><a name="p110419122619"></a><a name="p110419122619"></a>删除桶的网站配置信息。</p>
</td>
</tr>
<tr id="row40725835"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p41821194"><a name="p41821194"></a><a name="p41821194"></a><a href="设置桶的CORS配置.md">设置桶的CORS配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p91042095267"><a name="p91042095267"></a><a name="p91042095267"></a>设置桶的跨域资源共享配置信息。<span>OBS允许在桶内保存静态的网页资源，在正确的使用下，OBS的桶可以成为网站资源</span><span>。只有进行了适当的CORS配置，OBS中的网站才能响应另一个网站的跨域请求。</span></p>
</td>
</tr>
<tr id="row40846431"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p27744054"><a name="p27744054"></a><a name="p27744054"></a><a href="获取桶的CORS配置.md">获取桶的CORS配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p1010416917268"><a name="p1010416917268"></a><a name="p1010416917268"></a>获取桶的跨域资源共享配置信息。</p>
</td>
</tr>
<tr id="row48369902"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p64221938"><a name="p64221938"></a><a name="p64221938"></a><a href="删除桶的CORS配置.md">删除桶的CORS配置</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p141054915263"><a name="p141054915263"></a><a name="p141054915263"></a>删除桶的跨域资源共享配置信息。</p>
</td>
</tr>
<tr id="row41126533"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p53554153"><a name="p53554153"></a><a name="p53554153"></a><a href="OPTIONS桶.md">OPTIONS桶</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p141056919268"><a name="p141056919268"></a><a name="p141056919268"></a>检测客户端是否具有对服务端进行操作的权限。通常用于跨域访问之前。</p>
</td>
</tr>
<tr id="row12225337"><td class="cellrowborder" valign="top" width="40.5%" headers="mcps1.2.3.1.1 "><p id="p15349330"><a name="p15349330"></a><a name="p15349330"></a><a href="OPTIONS对象.md">OPTIONS对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.5%" headers="mcps1.2.3.1.2 "><p id="p31051896266"><a name="p31051896266"></a><a name="p31051896266"></a>检测客户端是否具有对服务端进行操作的权限。通常用于跨域访问之前。</p>
</td>
</tr>
</tbody>
</table>

## 对象操作接口<a name="section17527191838"></a>

**表 4**  对象操作接口

<a name="table7792865"></a>
<table><thead align="left"><tr id="row57419561"><th class="cellrowborder" valign="top" width="40.88%" id="mcps1.2.3.1.1"><p id="p47689484"><a name="p47689484"></a><a name="p47689484"></a>接口</p>
</th>
<th class="cellrowborder" valign="top" width="59.12%" id="mcps1.2.3.1.2"><p id="p1295124252711"><a name="p1295124252711"></a><a name="p1295124252711"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row37643023"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p15255933"><a name="p15255933"></a><a name="p15255933"></a><a href="PUT上传.md">PUT上传</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p102951542152717"><a name="p102951542152717"></a><a name="p102951542152717"></a>上传简单对象到指定的桶。</p>
</td>
</tr>
<tr id="row3085673"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p45338652"><a name="p45338652"></a><a name="p45338652"></a><a href="POST上传.md">POST上传</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p1429514422273"><a name="p1429514422273"></a><a name="p1429514422273"></a>基于表单上传对象到指定的桶。</p>
</td>
</tr>
<tr id="row5394690"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p28194798"><a name="p28194798"></a><a name="p28194798"></a><a href="复制对象.md">复制对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p52951742162720"><a name="p52951742162720"></a><a name="p52951742162720"></a>为OBS上已经存在的对象创建一个副本。</p>
</td>
</tr>
<tr id="row52426590"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p37933718"><a name="p37933718"></a><a name="p37933718"></a><a href="获取对象内容.md">获取对象内容</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p429514212716"><a name="p429514212716"></a><a name="p429514212716"></a>下载对象。</p>
</td>
</tr>
<tr id="row5859146"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p55591939"><a name="p55591939"></a><a name="p55591939"></a><a href="获取对象元数据.md">获取对象元数据</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p122951426278"><a name="p122951426278"></a><a name="p122951426278"></a>获取对象的元数据信息。包括对象的过期时间、版本号、CORS配置等信息。</p>
</td>
</tr>
<tr id="row30565404"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p18330024"><a name="p18330024"></a><a name="p18330024"></a><a href="删除对象.md">删除对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p92951642182712"><a name="p92951642182712"></a><a name="p92951642182712"></a>删除指定的对象。也可以携带<span>versionId</span>删除指定版本的对象。</p>
</td>
</tr>
<tr id="row30752495"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p37876676"><a name="p37876676"></a><a name="p37876676"></a><a href="批量删除对象.md">批量删除对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p929574214277"><a name="p929574214277"></a><a name="p929574214277"></a>将一个桶内的一部分对象一次性删除，删除后不可恢复。</p>
</td>
</tr>
<tr id="row5345769"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p42768539"><a name="p42768539"></a><a name="p42768539"></a><a href="取回归档存储对象.md">取回归档存储对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p99055582354"><a name="p99055582354"></a><a name="p99055582354"></a>将归档存储对象的内容取回，取回后才能下载。</p>
</td>
</tr>
<tr id="row49372536"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p65833402"><a name="p65833402"></a><a name="p65833402"></a><a href="追加写对象.md">追加写对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p8295194215277"><a name="p8295194215277"></a><a name="p8295194215277"></a>在指定桶内的一个对象尾追加上传数据，不存在相同对象键值的对象则创建新对象。</p>
</td>
</tr>
<tr id="row55629712"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p48538422"><a name="p48538422"></a><a name="p48538422"></a><a href="设置对象ACL.md">设置对象ACL</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p1129554282719"><a name="p1129554282719"></a><a name="p1129554282719"></a>设置一个指定对象的ACL信息。通过ACL可以控制对象的读写权限。</p>
</td>
</tr>
<tr id="row111314360133"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p913293641310"><a name="p913293641310"></a><a name="p913293641310"></a><a href="获取对象ACL.md">获取对象ACL</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p2791121115375"><a name="p2791121115375"></a><a name="p2791121115375"></a>获取一个指定对象的ACL信息。</p>
</td>
</tr>
<tr id="row425845519482"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p18740181219490"><a name="p18740181219490"></a><a name="p18740181219490"></a><a href="修改对象元数据.md">修改对象元数据</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p1425810552488"><a name="p1425810552488"></a><a name="p1425810552488"></a>添加、修改或删除桶中已经上传的对象的元数据。</p>
</td>
</tr>
<tr id="row99230312496"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p13405131324916"><a name="p13405131324916"></a><a name="p13405131324916"></a><a href="修改写对象.md">修改写对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p39236374910"><a name="p39236374910"></a><a name="p39236374910"></a>将指定并行文件系统内的一个对象从指定位置起修改为其他内容。</p>
</td>
</tr>
<tr id="row1720913144914"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p18251131464915"><a name="p18251131464915"></a><a name="p18251131464915"></a><a href="截断对象.md">截断对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p8209114497"><a name="p8209114497"></a><a name="p8209114497"></a>将指定并行文件系统内的一个对象截断到指定大小。</p>
</td>
</tr>
<tr id="row7735155824811"><td class="cellrowborder" valign="top" width="40.88%" headers="mcps1.2.3.1.1 "><p id="p129488145497"><a name="p129488145497"></a><a name="p129488145497"></a><a href="重命名对象.md">重命名对象</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.12%" headers="mcps1.2.3.1.2 "><p id="p14735135813486"><a name="p14735135813486"></a><a name="p14735135813486"></a>将指定并行文件系统内的一个对象重命名为其他对象名。</p>
</td>
</tr>
</tbody>
</table>

## 多段操作接口<a name="section34583211319"></a>

**表 5**  多段操作接口

<a name="table27242306"></a>
<table><thead align="left"><tr id="row59968749"><th class="cellrowborder" valign="top" width="40.65%" id="mcps1.2.3.1.1"><p id="p62802766"><a name="p62802766"></a><a name="p62802766"></a>接口</p>
</th>
<th class="cellrowborder" valign="top" width="59.35%" id="mcps1.2.3.1.2"><p id="p10296113133019"><a name="p10296113133019"></a><a name="p10296113133019"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row53859287"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p42619108"><a name="p42619108"></a><a name="p42619108"></a><a href="列举桶中已初始化多段任务.md">列举桶中已初始化多段任务</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p118121583383"><a name="p118121583383"></a><a name="p118121583383"></a>查询一个桶中所有的初始化后还未合并以及未取消的多段上传任务。</p>
</td>
</tr>
<tr id="row48027654"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p33322246"><a name="p33322246"></a><a name="p33322246"></a><a href="初始化上传段任务.md">初始化上传段任务</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p172967323016"><a name="p172967323016"></a><a name="p172967323016"></a>使用多段上传特性时，必须首先调用此接口初始化上传段任务，获取全局唯一的多段上传任务号，用于后续的上传段、合并段、列举段等操作。</p>
</td>
</tr>
<tr id="row31464766"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p13467047"><a name="p13467047"></a><a name="p13467047"></a><a href="上传段.md">上传段</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p142960311301"><a name="p142960311301"></a><a name="p142960311301"></a>为特定的任务上传段。</p>
</td>
</tr>
<tr id="row54094565"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p42774091"><a name="p42774091"></a><a name="p42774091"></a><a href="拷贝段.md">拷贝段</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p1056291419425"><a name="p1056291419425"></a><a name="p1056291419425"></a>将已上传对象的一部分或全部拷贝为段。</p>
</td>
</tr>
<tr id="row49422505"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p58136511"><a name="p58136511"></a><a name="p58136511"></a><a href="列举已上传的段.md">列举已上传的段</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p1429613313017"><a name="p1429613313017"></a><a name="p1429613313017"></a>查询一个任务所属的所有段信息。</p>
</td>
</tr>
<tr id="row53466558"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p16056153"><a name="p16056153"></a><a name="p16056153"></a><a href="合并段.md">合并段</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p182961319305"><a name="p182961319305"></a><a name="p182961319305"></a>将指定的段合并成一个完整的对象。</p>
</td>
</tr>
<tr id="row10287649"><td class="cellrowborder" valign="top" width="40.65%" headers="mcps1.2.3.1.1 "><p id="p52856884"><a name="p52856884"></a><a name="p52856884"></a><a href="取消多段上传任务.md">取消多段上传任务</a></p>
</td>
<td class="cellrowborder" valign="top" width="59.35%" headers="mcps1.2.3.1.2 "><p id="p72960363010"><a name="p72960363010"></a><a name="p72960363010"></a>取消一个多段上传的任务。</p>
</td>
</tr>
</tbody>
</table>

