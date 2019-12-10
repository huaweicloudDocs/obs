# 对象元数据Content-Type介绍<a name="obs_03_0102"></a>

上传到OBS中的对象，会根据对象的文件扩展名，自动匹配Content-Tpye值。使用浏览器访问对象时，会根据Content-Tpye类型来指定应用程序来打开。您可以根据对象的文件扩展来修改Content-Type。

**表 1**  常见的Content-Type类型

<a name="table158781830912"></a>
<table><thead align="left"><tr id="row3878630816"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.1"><p id="p1478218955016"><a name="p1478218955016"></a><a name="p1478218955016"></a>文件扩展名</p>
</th>
<th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.2"><p id="p12782169135010"><a name="p12782169135010"></a><a name="p12782169135010"></a>Content-Type</p>
</th>
<th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.3"><p id="p164218885219"><a name="p164218885219"></a><a name="p164218885219"></a>文件扩展名</p>
</th>
<th class="cellrowborder" valign="top" width="25%" id="mcps1.2.5.1.4"><p id="p126421683522"><a name="p126421683522"></a><a name="p126421683522"></a>Content-Type</p>
</th>
</tr>
</thead>
<tbody><tr id="row487917308119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p5782996508"><a name="p5782996508"></a><a name="p5782996508"></a>.*（ 二进制流，不知道下载文件类型）</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1378216918507"><a name="p1378216918507"></a><a name="p1378216918507"></a>application/octet-stream</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1178211985016"><a name="p1178211985016"></a><a name="p1178211985016"></a>.tif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p07821199507"><a name="p07821199507"></a><a name="p07821199507"></a>image/tiff</p>
</td>
</tr>
<tr id="row1787923017114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p177551226105316"><a name="p177551226105316"></a><a name="p177551226105316"></a>.001</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p157551264538"><a name="p157551264538"></a><a name="p157551264538"></a>application/x-001</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p97552267539"><a name="p97552267539"></a><a name="p97552267539"></a>.301</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p57551326185312"><a name="p57551326185312"></a><a name="p57551326185312"></a>application/x-301</p>
</td>
</tr>
<tr id="row08796305116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p2935163775317"><a name="p2935163775317"></a><a name="p2935163775317"></a>.323</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1793523725319"><a name="p1793523725319"></a><a name="p1793523725319"></a>text/h323</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p4935173712531"><a name="p4935173712531"></a><a name="p4935173712531"></a>.906</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p199351537155314"><a name="p199351537155314"></a><a name="p199351537155314"></a>application/x-906</p>
</td>
</tr>
<tr id="row17879113015115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p2935103716536"><a name="p2935103716536"></a><a name="p2935103716536"></a>.907</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p209362376530"><a name="p209362376530"></a><a name="p209362376530"></a>drawing/907</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p4936143715533"><a name="p4936143715533"></a><a name="p4936143715533"></a>.a11</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p179361037195310"><a name="p179361037195310"></a><a name="p179361037195310"></a>application/x-a11</p>
</td>
</tr>
<tr id="row138791530611"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p89363374539"><a name="p89363374539"></a><a name="p89363374539"></a>.acp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p49361371535"><a name="p49361371535"></a><a name="p49361371535"></a>audio/x-mei-aac</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p19936937115318"><a name="p19936937115318"></a><a name="p19936937115318"></a>.ai</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p17936183716537"><a name="p17936183716537"></a><a name="p17936183716537"></a>application/postscript</p>
</td>
</tr>
<tr id="row988063016112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p109361437175312"><a name="p109361437175312"></a><a name="p109361437175312"></a>.aif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p159361637125311"><a name="p159361637125311"></a><a name="p159361637125311"></a>audio/aiff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1193618378531"><a name="p1193618378531"></a><a name="p1193618378531"></a>.aifc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19936937115313"><a name="p19936937115313"></a><a name="p19936937115313"></a>audio/aiff</p>
</td>
</tr>
<tr id="row20880430416"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p139361037185314"><a name="p139361037185314"></a><a name="p139361037185314"></a>.aiff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1193616378536"><a name="p1193616378536"></a><a name="p1193616378536"></a>audio/aiff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p179366373536"><a name="p179366373536"></a><a name="p179366373536"></a>.anv</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1193623785318"><a name="p1193623785318"></a><a name="p1193623785318"></a>application/x-anv</p>
</td>
</tr>
<tr id="row7880430216"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p11936173745319"><a name="p11936173745319"></a><a name="p11936173745319"></a>.asa</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1693616378534"><a name="p1693616378534"></a><a name="p1693616378534"></a>text/asa</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p99362377538"><a name="p99362377538"></a><a name="p99362377538"></a>.asf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1593633745310"><a name="p1593633745310"></a><a name="p1593633745310"></a>video/x-ms-asf</p>
</td>
</tr>
<tr id="row1888018307117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p5936937185319"><a name="p5936937185319"></a><a name="p5936937185319"></a>.asp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p293633735320"><a name="p293633735320"></a><a name="p293633735320"></a>text/asp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p2093623775318"><a name="p2093623775318"></a><a name="p2093623775318"></a>.asx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9936203715530"><a name="p9936203715530"></a><a name="p9936203715530"></a>video/x-ms-asf</p>
</td>
</tr>
<tr id="row128808304119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p19361737115314"><a name="p19361737115314"></a><a name="p19361737115314"></a>.au</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p12936153713537"><a name="p12936153713537"></a><a name="p12936153713537"></a>audio/basic</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p6937133716535"><a name="p6937133716535"></a><a name="p6937133716535"></a>.avi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p393793755313"><a name="p393793755313"></a><a name="p393793755313"></a>video/avi</p>
</td>
</tr>
<tr id="row688013016110"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p12139164916538"><a name="p12139164916538"></a><a name="p12139164916538"></a>.awf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14139164911530"><a name="p14139164911530"></a><a name="p14139164911530"></a>application/vnd.adobe.workflow</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p12139449185320"><a name="p12139449185320"></a><a name="p12139449185320"></a>.biz</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p5139174910534"><a name="p5139174910534"></a><a name="p5139174910534"></a>text/xml</p>
</td>
</tr>
<tr id="row588033017117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1213912494539"><a name="p1213912494539"></a><a name="p1213912494539"></a>.bmp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p181391949145316"><a name="p181391949145316"></a><a name="p181391949145316"></a>application/x-bmp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p113954917536"><a name="p113954917536"></a><a name="p113954917536"></a>.bot</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19139184918535"><a name="p19139184918535"></a><a name="p19139184918535"></a>application/x-bot</p>
</td>
</tr>
<tr id="row888110303113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1713954919531"><a name="p1713954919531"></a><a name="p1713954919531"></a>.c4t</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p13139124915533"><a name="p13139124915533"></a><a name="p13139124915533"></a>application/x-c4t</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1513984918538"><a name="p1513984918538"></a><a name="p1513984918538"></a>.c90</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p713915496537"><a name="p713915496537"></a><a name="p713915496537"></a>application/x-c90</p>
</td>
</tr>
<tr id="row5881163010119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1713914917534"><a name="p1713914917534"></a><a name="p1713914917534"></a>.cal</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14139184920536"><a name="p14139184920536"></a><a name="p14139184920536"></a>application/x-cals</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15139184995310"><a name="p15139184995310"></a><a name="p15139184995310"></a>.cat</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p913984911539"><a name="p913984911539"></a><a name="p913984911539"></a>application/vnd.ms-pki.seccat</p>
</td>
</tr>
<tr id="row888193012119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p2139349115310"><a name="p2139349115310"></a><a name="p2139349115310"></a>.cdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p121391949145315"><a name="p121391949145315"></a><a name="p121391949145315"></a>application/x-netcdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p3139114918535"><a name="p3139114918535"></a><a name="p3139114918535"></a>.cdr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p17139124995316"><a name="p17139124995316"></a><a name="p17139124995316"></a>application/x-cdr</p>
</td>
</tr>
<tr id="row388112304114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p0139649195310"><a name="p0139649195310"></a><a name="p0139649195310"></a>.cel</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1213934920537"><a name="p1213934920537"></a><a name="p1213934920537"></a>application/x-cel</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1314016498539"><a name="p1314016498539"></a><a name="p1314016498539"></a>.cer</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p191401490530"><a name="p191401490530"></a><a name="p191401490530"></a>application/x-x509-ca-cert</p>
</td>
</tr>
<tr id="row08816301111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p171401249175317"><a name="p171401249175317"></a><a name="p171401249175317"></a>.cg4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p814054914535"><a name="p814054914535"></a><a name="p814054914535"></a>application/x-g4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p814014499530"><a name="p814014499530"></a><a name="p814014499530"></a>.cgm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p191405492534"><a name="p191405492534"></a><a name="p191405492534"></a>application/x-cgm</p>
</td>
</tr>
<tr id="row188819301515"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1214012498530"><a name="p1214012498530"></a><a name="p1214012498530"></a>.cit</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1140849195312"><a name="p1140849195312"></a><a name="p1140849195312"></a>application/x-cit</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15140749135312"><a name="p15140749135312"></a><a name="p15140749135312"></a>.class</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p151401649125311"><a name="p151401649125311"></a><a name="p151401649125311"></a>java/*</p>
</td>
</tr>
<tr id="row158821330719"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p01401749105316"><a name="p01401749105316"></a><a name="p01401749105316"></a>.cml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p81401949105319"><a name="p81401949105319"></a><a name="p81401949105319"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p10140124915311"><a name="p10140124915311"></a><a name="p10140124915311"></a>.cmp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p191401499534"><a name="p191401499534"></a><a name="p191401499534"></a>application/x-cmp</p>
</td>
</tr>
<tr id="row1088253017112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p11140154916538"><a name="p11140154916538"></a><a name="p11140154916538"></a>.cmx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1214017498535"><a name="p1214017498535"></a><a name="p1214017498535"></a>application/x-cmx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p20140184916538"><a name="p20140184916538"></a><a name="p20140184916538"></a>.cot</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p181401749135315"><a name="p181401749135315"></a><a name="p181401749135315"></a>application/x-cot</p>
</td>
</tr>
<tr id="row98829301817"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p10140649145318"><a name="p10140649145318"></a><a name="p10140649145318"></a>.crl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p7140134917537"><a name="p7140134917537"></a><a name="p7140134917537"></a>application/pkix-crl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p514013493538"><a name="p514013493538"></a><a name="p514013493538"></a>.crt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p914004965318"><a name="p914004965318"></a><a name="p914004965318"></a>application/x-x509-ca-cert</p>
</td>
</tr>
<tr id="row588219301610"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p5141134905320"><a name="p5141134905320"></a><a name="p5141134905320"></a>.csi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p81412493531"><a name="p81412493531"></a><a name="p81412493531"></a>application/x-csi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p91411749135316"><a name="p91411749135316"></a><a name="p91411749135316"></a>.css</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p914112498533"><a name="p914112498533"></a><a name="p914112498533"></a>text/css</p>
</td>
</tr>
<tr id="row1688218301117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p106779185415"><a name="p106779185415"></a><a name="p106779185415"></a>.cut</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p2677410548"><a name="p2677410548"></a><a name="p2677410548"></a>application/x-cut</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18677171145419"><a name="p18677171145419"></a><a name="p18677171145419"></a>.dbf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p4677201195417"><a name="p4677201195417"></a><a name="p4677201195417"></a>application/x-dbf</p>
</td>
</tr>
<tr id="row1788220309111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1667715125418"><a name="p1667715125418"></a><a name="p1667715125418"></a>.dbm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1767715165420"><a name="p1767715165420"></a><a name="p1767715165420"></a>application/x-dbm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p567718125420"><a name="p567718125420"></a><a name="p567718125420"></a>.dbx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1767791115410"><a name="p1767791115410"></a><a name="p1767791115410"></a>application/x-dbx</p>
</td>
</tr>
<tr id="row7882330912"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p15677151175415"><a name="p15677151175415"></a><a name="p15677151175415"></a>.dcd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p156772116545"><a name="p156772116545"></a><a name="p156772116545"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1267715117547"><a name="p1267715117547"></a><a name="p1267715117547"></a>.dcx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2678141185413"><a name="p2678141185413"></a><a name="p2678141185413"></a>application/x-dcx</p>
</td>
</tr>
<tr id="row28827306111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p11678191175411"><a name="p11678191175411"></a><a name="p11678191175411"></a>.der</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1267812165410"><a name="p1267812165410"></a><a name="p1267812165410"></a>application/x-x509-ca-cert</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18678316542"><a name="p18678316542"></a><a name="p18678316542"></a>.dgn</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p16678161165415"><a name="p16678161165415"></a><a name="p16678161165415"></a>application/x-dgn</p>
</td>
</tr>
<tr id="row588263019117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p3678311545"><a name="p3678311545"></a><a name="p3678311545"></a>.dib</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p15678111135412"><a name="p15678111135412"></a><a name="p15678111135412"></a>application/x-dib</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1367816110548"><a name="p1367816110548"></a><a name="p1367816110548"></a>.dll</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p367851165412"><a name="p367851165412"></a><a name="p367851165412"></a>application/x-msdownload</p>
</td>
</tr>
<tr id="row138823304112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1667815116541"><a name="p1667815116541"></a><a name="p1667815116541"></a>.doc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p116781015547"><a name="p116781015547"></a><a name="p116781015547"></a>application/msword</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p86783165416"><a name="p86783165416"></a><a name="p86783165416"></a>.dot</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p367818115542"><a name="p367818115542"></a><a name="p367818115542"></a>application/msword</p>
</td>
</tr>
<tr id="row28836301519"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1678519540"><a name="p1678519540"></a><a name="p1678519540"></a>.drw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p4678117541"><a name="p4678117541"></a><a name="p4678117541"></a>application/x-drw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1167812119548"><a name="p1167812119548"></a><a name="p1167812119548"></a>.dtd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p36798175411"><a name="p36798175411"></a><a name="p36798175411"></a>text/xml</p>
</td>
</tr>
<tr id="row58833301218"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p12679111195412"><a name="p12679111195412"></a><a name="p12679111195412"></a>.dwf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p156795145416"><a name="p156795145416"></a><a name="p156795145416"></a>Model/vnd.dwf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p13679141105412"><a name="p13679141105412"></a><a name="p13679141105412"></a>.dwf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p467911105411"><a name="p467911105411"></a><a name="p467911105411"></a>application/x-dwf</p>
</td>
</tr>
<tr id="row5883030913"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p14840181235418"><a name="p14840181235418"></a><a name="p14840181235418"></a>.dwg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1684161245418"><a name="p1684161245418"></a><a name="p1684161245418"></a>application/x-dwg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p5841111214546"><a name="p5841111214546"></a><a name="p5841111214546"></a>.dxb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p168411112105413"><a name="p168411112105413"></a><a name="p168411112105413"></a>application/x-dxb</p>
</td>
</tr>
<tr id="row48835301414"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p15841412155410"><a name="p15841412155410"></a><a name="p15841412155410"></a>.dxf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1084191275419"><a name="p1084191275419"></a><a name="p1084191275419"></a>application/x-dxf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p19841191295418"><a name="p19841191295418"></a><a name="p19841191295418"></a>.edn</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p0841312155416"><a name="p0841312155416"></a><a name="p0841312155416"></a>application/vnd.adobe.edn</p>
</td>
</tr>
<tr id="row68831330217"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p284171255412"><a name="p284171255412"></a><a name="p284171255412"></a>.emf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p108411912195410"><a name="p108411912195410"></a><a name="p108411912195410"></a>application/x-emf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1841912165416"><a name="p1841912165416"></a><a name="p1841912165416"></a>.eml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p178411012185417"><a name="p178411012185417"></a><a name="p178411012185417"></a>message/rfc822</p>
</td>
</tr>
<tr id="row168832308116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p17841171218548"><a name="p17841171218548"></a><a name="p17841171218548"></a>.ent</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1841181245415"><a name="p1841181245415"></a><a name="p1841181245415"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p7841912165411"><a name="p7841912165411"></a><a name="p7841912165411"></a>.epi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1084111245415"><a name="p1084111245415"></a><a name="p1084111245415"></a>application/x-epi</p>
</td>
</tr>
<tr id="row118831301118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p198411512145414"><a name="p198411512145414"></a><a name="p198411512145414"></a>.eps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p17841812195420"><a name="p17841812195420"></a><a name="p17841812195420"></a>application/x-ps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p3841412145420"><a name="p3841412145420"></a><a name="p3841412145420"></a>.eps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p178411512125419"><a name="p178411512125419"></a><a name="p178411512125419"></a>application/postscript</p>
</td>
</tr>
<tr id="row108836301617"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p58414125549"><a name="p58414125549"></a><a name="p58414125549"></a>.etd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p4841712105414"><a name="p4841712105414"></a><a name="p4841712105414"></a>application/x-ebx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p17841111235418"><a name="p17841111235418"></a><a name="p17841111235418"></a>.exe</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1884171285411"><a name="p1884171285411"></a><a name="p1884171285411"></a>application/x-msdownload</p>
</td>
</tr>
<tr id="row2088312301711"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p12841111212542"><a name="p12841111212542"></a><a name="p12841111212542"></a>.fax</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p9841212135415"><a name="p9841212135415"></a><a name="p9841212135415"></a>image/fax</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18841161210542"><a name="p18841161210542"></a><a name="p18841161210542"></a>.fdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p14842112105412"><a name="p14842112105412"></a><a name="p14842112105412"></a>application/vnd.fdf</p>
</td>
</tr>
<tr id="row58834302110"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p784214121542"><a name="p784214121542"></a><a name="p784214121542"></a>.fif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1842141245416"><a name="p1842141245416"></a><a name="p1842141245416"></a>application/fractals</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1484231205411"><a name="p1484231205411"></a><a name="p1484231205411"></a>.fo</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2842141218548"><a name="p2842141218548"></a><a name="p2842141218548"></a>text/xml</p>
</td>
</tr>
<tr id="row98841301419"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p984216126545"><a name="p984216126545"></a><a name="p984216126545"></a>.frm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p178429126542"><a name="p178429126542"></a><a name="p178429126542"></a>application/x-frm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1842201216544"><a name="p1842201216544"></a><a name="p1842201216544"></a>.g4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p188423122542"><a name="p188423122542"></a><a name="p188423122542"></a>application/x-g4</p>
</td>
</tr>
<tr id="row488414301513"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p384217125546"><a name="p384217125546"></a><a name="p384217125546"></a>.gbr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1184281214542"><a name="p1184281214542"></a><a name="p1184281214542"></a>application/x-gbr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1484231255415"><a name="p1484231255415"></a><a name="p1484231255415"></a>.</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p18842161275415"><a name="p18842161275415"></a><a name="p18842161275415"></a>application/x-</p>
</td>
</tr>
<tr id="row138849301818"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1784271225411"><a name="p1784271225411"></a><a name="p1784271225411"></a>.gif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p13842201255417"><a name="p13842201255417"></a><a name="p13842201255417"></a>image/gif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p188428123540"><a name="p188428123540"></a><a name="p188428123540"></a>.gl2</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9842151265418"><a name="p9842151265418"></a><a name="p9842151265418"></a>application/x-gl2</p>
</td>
</tr>
<tr id="row198847306119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p11842111275419"><a name="p11842111275419"></a><a name="p11842111275419"></a>.gp4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p68421012195419"><a name="p68421012195419"></a><a name="p68421012195419"></a>application/x-gp4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p78421112175415"><a name="p78421112175415"></a><a name="p78421112175415"></a>.hgl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p18842512105419"><a name="p18842512105419"></a><a name="p18842512105419"></a>application/x-hgl</p>
</td>
</tr>
<tr id="row188433011120"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p9842191219540"><a name="p9842191219540"></a><a name="p9842191219540"></a>.hmr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1784211285413"><a name="p1784211285413"></a><a name="p1784211285413"></a>application/x-hmr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p158421712115411"><a name="p158421712115411"></a><a name="p158421712115411"></a>.hpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p7842181295412"><a name="p7842181295412"></a><a name="p7842181295412"></a>application/x-hpgl</p>
</td>
</tr>
<tr id="row88842302112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p15842131219547"><a name="p15842131219547"></a><a name="p15842131219547"></a>.hpl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p3843131245417"><a name="p3843131245417"></a><a name="p3843131245417"></a>application/x-hpl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p16843151255410"><a name="p16843151255410"></a><a name="p16843151255410"></a>.hqx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1584321255415"><a name="p1584321255415"></a><a name="p1584321255415"></a>application/mac-binhex40</p>
</td>
</tr>
<tr id="row78843309112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p484391275417"><a name="p484391275417"></a><a name="p484391275417"></a>.hrf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p5843141235412"><a name="p5843141235412"></a><a name="p5843141235412"></a>application/x-hrf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1384331265410"><a name="p1384331265410"></a><a name="p1384331265410"></a>.hta</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1384371225413"><a name="p1384371225413"></a><a name="p1384371225413"></a>application/hta</p>
</td>
</tr>
<tr id="row488519307116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p984391215544"><a name="p984391215544"></a><a name="p984391215544"></a>.htc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p18843171235414"><a name="p18843171235414"></a><a name="p18843171235414"></a>text/x-component</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18843111219548"><a name="p18843111219548"></a><a name="p18843111219548"></a>.htm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p4843121213540"><a name="p4843121213540"></a><a name="p4843121213540"></a>text/html</p>
</td>
</tr>
<tr id="row19885183020113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1986065995412"><a name="p1986065995412"></a><a name="p1986065995412"></a>.html</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p58603599543"><a name="p58603599543"></a><a name="p58603599543"></a>text/html</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p586018593543"><a name="p586018593543"></a><a name="p586018593543"></a>.htt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p98603599545"><a name="p98603599545"></a><a name="p98603599545"></a>text/webviewhtml</p>
</td>
</tr>
<tr id="row13885630513"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p18861175985412"><a name="p18861175985412"></a><a name="p18861175985412"></a>.htx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p16861145935416"><a name="p16861145935416"></a><a name="p16861145935416"></a>text/html</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p68612059125410"><a name="p68612059125410"></a><a name="p68612059125410"></a>.icb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p11861185910549"><a name="p11861185910549"></a><a name="p11861185910549"></a>application/x-icb</p>
</td>
</tr>
<tr id="row488583012112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p186165915544"><a name="p186165915544"></a><a name="p186165915544"></a>.ico</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p686114594543"><a name="p686114594543"></a><a name="p686114594543"></a>image/x-icon</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p48611559115414"><a name="p48611559115414"></a><a name="p48611559115414"></a>.ico</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2861125915544"><a name="p2861125915544"></a><a name="p2861125915544"></a>application/x-ico</p>
</td>
</tr>
<tr id="row5885630616"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p486145917547"><a name="p486145917547"></a><a name="p486145917547"></a>.iff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p586175985416"><a name="p586175985416"></a><a name="p586175985416"></a>application/x-iff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p5861459185410"><a name="p5861459185410"></a><a name="p5861459185410"></a>.ig4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p4861105985414"><a name="p4861105985414"></a><a name="p4861105985414"></a>application/x-g4</p>
</td>
</tr>
<tr id="row16885173019116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p5861105925413"><a name="p5861105925413"></a><a name="p5861105925413"></a>.igs</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1286245911546"><a name="p1286245911546"></a><a name="p1286245911546"></a>application/x-igs</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1386245925418"><a name="p1386245925418"></a><a name="p1386245925418"></a>.iii</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p11862195925416"><a name="p11862195925416"></a><a name="p11862195925416"></a>application/x-iphone</p>
</td>
</tr>
<tr id="row1885143020118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p48622592545"><a name="p48622592545"></a><a name="p48622592545"></a>.img</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1586215925415"><a name="p1586215925415"></a><a name="p1586215925415"></a>application/x-img</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p13862135919549"><a name="p13862135919549"></a><a name="p13862135919549"></a>.ins</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p986215965418"><a name="p986215965418"></a><a name="p986215965418"></a>application/x-internet-signup</p>
</td>
</tr>
<tr id="row1888520301016"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p12862105915547"><a name="p12862105915547"></a><a name="p12862105915547"></a>.isp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p286215914542"><a name="p286215914542"></a><a name="p286215914542"></a>application/x-internet-signup</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1186217594549"><a name="p1186217594549"></a><a name="p1186217594549"></a>.IVF</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p128627596541"><a name="p128627596541"></a><a name="p128627596541"></a>video/x-ivf</p>
</td>
</tr>
<tr id="row11886103011116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1586395915540"><a name="p1586395915540"></a><a name="p1586395915540"></a>.java</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p586335925412"><a name="p586335925412"></a><a name="p586335925412"></a>java/*</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p186315910542"><a name="p186315910542"></a><a name="p186315910542"></a>.jfif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p11863145995416"><a name="p11863145995416"></a><a name="p11863145995416"></a>image/jpeg</p>
</td>
</tr>
<tr id="row788610303111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p14863105912544"><a name="p14863105912544"></a><a name="p14863105912544"></a>.jpe</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1864859175414"><a name="p1864859175414"></a><a name="p1864859175414"></a>image/jpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1186455916545"><a name="p1186455916545"></a><a name="p1186455916545"></a>.jpe</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9864115911547"><a name="p9864115911547"></a><a name="p9864115911547"></a>application/x-jpe</p>
</td>
</tr>
<tr id="row28863309116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p168646593542"><a name="p168646593542"></a><a name="p168646593542"></a>.jpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p7864195985411"><a name="p7864195985411"></a><a name="p7864195985411"></a>image/jpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1186410595549"><a name="p1186410595549"></a><a name="p1186410595549"></a>.jpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p16864859105411"><a name="p16864859105411"></a><a name="p16864859105411"></a>image/jpeg</p>
</td>
</tr>
<tr id="row988618302111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1864105911542"><a name="p1864105911542"></a><a name="p1864105911542"></a>.jpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1386485935410"><a name="p1386485935410"></a><a name="p1386485935410"></a>application/x-jpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18864175955411"><a name="p18864175955411"></a><a name="p18864175955411"></a>.js</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p148641659125414"><a name="p148641659125414"></a><a name="p148641659125414"></a>application/x-javascript</p>
</td>
</tr>
<tr id="row148863300115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p386465913541"><a name="p386465913541"></a><a name="p386465913541"></a>.jsp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p2864105913541"><a name="p2864105913541"></a><a name="p2864105913541"></a>text/html</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18641659105412"><a name="p18641659105412"></a><a name="p18641659105412"></a>.la1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p18864559115413"><a name="p18864559115413"></a><a name="p18864559115413"></a>audio/x-liquid-file</p>
</td>
</tr>
<tr id="row1188673014116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p20865185912548"><a name="p20865185912548"></a><a name="p20865185912548"></a>.lar</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p158651559155410"><a name="p158651559155410"></a><a name="p158651559155410"></a>application/x-laplayer-reg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p4865559105412"><a name="p4865559105412"></a><a name="p4865559105412"></a>.latex</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p138651359155418"><a name="p138651359155418"></a><a name="p138651359155418"></a>application/x-latex</p>
</td>
</tr>
<tr id="row288612302015"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p2603010205716"><a name="p2603010205716"></a><a name="p2603010205716"></a>.lavs</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p160315103576"><a name="p160315103576"></a><a name="p160315103576"></a>audio/x-liquid-secure</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p14603101055717"><a name="p14603101055717"></a><a name="p14603101055717"></a>.lbm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1360321014579"><a name="p1360321014579"></a><a name="p1360321014579"></a>application/x-lbm</p>
</td>
</tr>
<tr id="row12887113017111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p560371015712"><a name="p560371015712"></a><a name="p560371015712"></a>.lmsff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p3603121075711"><a name="p3603121075711"></a><a name="p3603121075711"></a>audio/x-la-lms</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p166033102573"><a name="p166033102573"></a><a name="p166033102573"></a>.ls</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p7603151013577"><a name="p7603151013577"></a><a name="p7603151013577"></a>application/x-javascript</p>
</td>
</tr>
<tr id="row12887330518"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p960351065719"><a name="p960351065719"></a><a name="p960351065719"></a>.ltr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1560319105578"><a name="p1560319105578"></a><a name="p1560319105578"></a>application/x-ltr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p8603161035719"><a name="p8603161035719"></a><a name="p8603161035719"></a>.m1v</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p126033103571"><a name="p126033103571"></a><a name="p126033103571"></a>video/x-mpeg</p>
</td>
</tr>
<tr id="row388715308111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p176035107571"><a name="p176035107571"></a><a name="p176035107571"></a>.m2v</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1260481025719"><a name="p1260481025719"></a><a name="p1260481025719"></a>video/x-mpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p8604710195714"><a name="p8604710195714"></a><a name="p8604710195714"></a>.m3u</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p36045107573"><a name="p36045107573"></a><a name="p36045107573"></a>audio/mpegurl</p>
</td>
</tr>
<tr id="row288714301810"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p0604121075711"><a name="p0604121075711"></a><a name="p0604121075711"></a>.m4e</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p460412103574"><a name="p460412103574"></a><a name="p460412103574"></a>video/mpeg4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p46042108579"><a name="p46042108579"></a><a name="p46042108579"></a>.mac</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p14604121035712"><a name="p14604121035712"></a><a name="p14604121035712"></a>application/x-mac</p>
</td>
</tr>
<tr id="row118874306113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p5604131018571"><a name="p5604131018571"></a><a name="p5604131018571"></a>.man</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1860451018574"><a name="p1860451018574"></a><a name="p1860451018574"></a>application/x-troff-man</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1560471018574"><a name="p1560471018574"></a><a name="p1560471018574"></a>.math</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p136041103579"><a name="p136041103579"></a><a name="p136041103579"></a>text/xml</p>
</td>
</tr>
<tr id="row7887183013113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p17604121012573"><a name="p17604121012573"></a><a name="p17604121012573"></a>.mdb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1360411065716"><a name="p1360411065716"></a><a name="p1360411065716"></a>application/msaccess</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p136041103570"><a name="p136041103570"></a><a name="p136041103570"></a>.mdb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p5604181045715"><a name="p5604181045715"></a><a name="p5604181045715"></a>application/x-mdb</p>
</td>
</tr>
<tr id="row5887203015117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p46041910175715"><a name="p46041910175715"></a><a name="p46041910175715"></a>.mfp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p96044100578"><a name="p96044100578"></a><a name="p96044100578"></a>application/x-shockwave-flash</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p860491075714"><a name="p860491075714"></a><a name="p860491075714"></a>.mht</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1160511107576"><a name="p1160511107576"></a><a name="p1160511107576"></a>message/rfc822</p>
</td>
</tr>
<tr id="row388716301110"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p19605310185712"><a name="p19605310185712"></a><a name="p19605310185712"></a>.mhtml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p186051610175716"><a name="p186051610175716"></a><a name="p186051610175716"></a>message/rfc822</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p12605210125713"><a name="p12605210125713"></a><a name="p12605210125713"></a>.mi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p96055108571"><a name="p96055108571"></a><a name="p96055108571"></a>application/x-mi</p>
</td>
</tr>
<tr id="row38877303111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p186052107578"><a name="p186052107578"></a><a name="p186052107578"></a>.mid</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1960521085711"><a name="p1960521085711"></a><a name="p1960521085711"></a>audio/mid</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18605510195718"><a name="p18605510195718"></a><a name="p18605510195718"></a>.midi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p260516108572"><a name="p260516108572"></a><a name="p260516108572"></a>audio/mid</p>
</td>
</tr>
<tr id="row1688814306115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p196051410185716"><a name="p196051410185716"></a><a name="p196051410185716"></a>.mil</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p46051210115715"><a name="p46051210115715"></a><a name="p46051210115715"></a>application/x-mil</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p156059101577"><a name="p156059101577"></a><a name="p156059101577"></a>.mml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p116056106577"><a name="p116056106577"></a><a name="p116056106577"></a>text/xml</p>
</td>
</tr>
<tr id="row1088817307118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p960501012574"><a name="p960501012574"></a><a name="p960501012574"></a>.mnd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p10605201018574"><a name="p10605201018574"></a><a name="p10605201018574"></a>audio/x-musicnet-download</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p96051710175712"><a name="p96051710175712"></a><a name="p96051710175712"></a>.mns</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p260501095716"><a name="p260501095716"></a><a name="p260501095716"></a>audio/x-musicnet-stream</p>
</td>
</tr>
<tr id="row15888330117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p860541015572"><a name="p860541015572"></a><a name="p860541015572"></a>.mocha</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p460581085713"><a name="p460581085713"></a><a name="p460581085713"></a>application/x-javascript</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p660619105578"><a name="p660619105578"></a><a name="p660619105578"></a>.movie</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19606710165717"><a name="p19606710165717"></a><a name="p19606710165717"></a>video/x-sgi-movie</p>
</td>
</tr>
<tr id="row19888193019118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p9606010105710"><a name="p9606010105710"></a><a name="p9606010105710"></a>.mp1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p146061110145710"><a name="p146061110145710"></a><a name="p146061110145710"></a>audio/mp1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p560661005719"><a name="p560661005719"></a><a name="p560661005719"></a>.mp2</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2606171016572"><a name="p2606171016572"></a><a name="p2606171016572"></a>audio/mp2</p>
</td>
</tr>
<tr id="row8888530415"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1460681018577"><a name="p1460681018577"></a><a name="p1460681018577"></a>.mp2v</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p56061210155714"><a name="p56061210155714"></a><a name="p56061210155714"></a>video/mpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p17606191013576"><a name="p17606191013576"></a><a name="p17606191013576"></a>.mp3</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p17606131017578"><a name="p17606131017578"></a><a name="p17606131017578"></a>audio/mp3</p>
</td>
</tr>
<tr id="row188843013113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p166061104578"><a name="p166061104578"></a><a name="p166061104578"></a>.mp4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p26063104571"><a name="p26063104571"></a><a name="p26063104571"></a>video/mpeg4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p36061910105710"><a name="p36061910105710"></a><a name="p36061910105710"></a>.mpa</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p660631005712"><a name="p660631005712"></a><a name="p660631005712"></a>video/x-mpg</p>
</td>
</tr>
<tr id="row16888113018110"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p96063109579"><a name="p96063109579"></a><a name="p96063109579"></a>.mpd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14606310115720"><a name="p14606310115720"></a><a name="p14606310115720"></a>application/vnd.ms-project</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15606161075711"><a name="p15606161075711"></a><a name="p15606161075711"></a>.mpe</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p860714103576"><a name="p860714103576"></a><a name="p860714103576"></a>video/x-mpeg</p>
</td>
</tr>
<tr id="row11888330311"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p360718107579"><a name="p360718107579"></a><a name="p360718107579"></a>.mpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1660711017570"><a name="p1660711017570"></a><a name="p1660711017570"></a>video/mpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p160721012572"><a name="p160721012572"></a><a name="p160721012572"></a>.mpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2607310145716"><a name="p2607310145716"></a><a name="p2607310145716"></a>video/mpg</p>
</td>
</tr>
<tr id="row188853017116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p18607161055718"><a name="p18607161055718"></a><a name="p18607161055718"></a>.mpga</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p3607310105710"><a name="p3607310105710"></a><a name="p3607310105710"></a>audio/rn-mpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p96071210205719"><a name="p96071210205719"></a><a name="p96071210205719"></a>.mpp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p56071810115719"><a name="p56071810115719"></a><a name="p56071810115719"></a>application/vnd.ms-project</p>
</td>
</tr>
<tr id="row1088817304111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p186071100578"><a name="p186071100578"></a><a name="p186071100578"></a>.mps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p126071410135716"><a name="p126071410135716"></a><a name="p126071410135716"></a>video/x-mpeg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p16607181025717"><a name="p16607181025717"></a><a name="p16607181025717"></a>.mpt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9607101075717"><a name="p9607101075717"></a><a name="p9607101075717"></a>application/vnd.ms-project</p>
</td>
</tr>
<tr id="row128891130916"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p2608131015716"><a name="p2608131015716"></a><a name="p2608131015716"></a>.mpv</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p126081210185711"><a name="p126081210185711"></a><a name="p126081210185711"></a>video/mpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p5608310125719"><a name="p5608310125719"></a><a name="p5608310125719"></a>.mpv2</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1760812106571"><a name="p1760812106571"></a><a name="p1760812106571"></a>video/mpeg</p>
</td>
</tr>
<tr id="row288915308114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p13608410125715"><a name="p13608410125715"></a><a name="p13608410125715"></a>.mpw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1960891025714"><a name="p1960891025714"></a><a name="p1960891025714"></a>application/vnd.ms-project</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p760851019578"><a name="p760851019578"></a><a name="p760851019578"></a>.mpx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p46081710185718"><a name="p46081710185718"></a><a name="p46081710185718"></a>application/vnd.ms-project</p>
</td>
</tr>
<tr id="row1188918301618"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1160831075713"><a name="p1160831075713"></a><a name="p1160831075713"></a>.mtx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p7608121010574"><a name="p7608121010574"></a><a name="p7608121010574"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p4608141010570"><a name="p4608141010570"></a><a name="p4608141010570"></a>.mxp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p560814106579"><a name="p560814106579"></a><a name="p560814106579"></a>application/x-mmxp</p>
</td>
</tr>
<tr id="row138897305120"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1260881085720"><a name="p1260881085720"></a><a name="p1260881085720"></a>.net</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p36089108576"><a name="p36089108576"></a><a name="p36089108576"></a>image/pnetvue</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p166081910125714"><a name="p166081910125714"></a><a name="p166081910125714"></a>.nrf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p960851016579"><a name="p960851016579"></a><a name="p960851016579"></a>application/x-nrf</p>
</td>
</tr>
<tr id="row178901030711"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p89751930125715"><a name="p89751930125715"></a><a name="p89751930125715"></a>.nws</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p12975930175711"><a name="p12975930175711"></a><a name="p12975930175711"></a>message/rfc822</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p8975133035712"><a name="p8975133035712"></a><a name="p8975133035712"></a>.odc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9975530125710"><a name="p9975530125710"></a><a name="p9975530125710"></a>text/x-ms-odc</p>
</td>
</tr>
<tr id="row889011301515"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p19975330165715"><a name="p19975330165715"></a><a name="p19975330165715"></a>.out</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p9975113015710"><a name="p9975113015710"></a><a name="p9975113015710"></a>application/x-out</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1497513045716"><a name="p1497513045716"></a><a name="p1497513045716"></a>.p10</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19975130195719"><a name="p19975130195719"></a><a name="p19975130195719"></a>application/pkcs10</p>
</td>
</tr>
<tr id="row188901730218"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1897533016571"><a name="p1897533016571"></a><a name="p1897533016571"></a>.p12</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1497593095716"><a name="p1497593095716"></a><a name="p1497593095716"></a>application/x-pkcs12</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p69761730145717"><a name="p69761730145717"></a><a name="p69761730145717"></a>.p7b</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p397693025718"><a name="p397693025718"></a><a name="p397693025718"></a>application/x-pkcs7-certificates</p>
</td>
</tr>
<tr id="row68909301212"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1697611309577"><a name="p1697611309577"></a><a name="p1697611309577"></a>.p7c</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p18976193085713"><a name="p18976193085713"></a><a name="p18976193085713"></a>application/pkcs7-mime</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p6976173011576"><a name="p6976173011576"></a><a name="p6976173011576"></a>.p7m</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p18976173025713"><a name="p18976173025713"></a><a name="p18976173025713"></a>application/pkcs7-mime</p>
</td>
</tr>
<tr id="row178901830317"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p99761230105715"><a name="p99761230105715"></a><a name="p99761230105715"></a>.p7r</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p99761530165718"><a name="p99761530165718"></a><a name="p99761530165718"></a>application/x-pkcs7-certreqresp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p6976193010573"><a name="p6976193010573"></a><a name="p6976193010573"></a>.p7s</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1297663095720"><a name="p1297663095720"></a><a name="p1297663095720"></a>application/pkcs7-signature</p>
</td>
</tr>
<tr id="row16891143013113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1297683045719"><a name="p1297683045719"></a><a name="p1297683045719"></a>.pc5</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p2097653016579"><a name="p2097653016579"></a><a name="p2097653016579"></a>application/x-pc5</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18976113015719"><a name="p18976113015719"></a><a name="p18976113015719"></a>.pci</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1097653005712"><a name="p1097653005712"></a><a name="p1097653005712"></a>application/x-pci</p>
</td>
</tr>
<tr id="row188917301712"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p189761830115711"><a name="p189761830115711"></a><a name="p189761830115711"></a>.pcl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1997603035716"><a name="p1997603035716"></a><a name="p1997603035716"></a>application/x-pcl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p897603016577"><a name="p897603016577"></a><a name="p897603016577"></a>.pcx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p6976113017577"><a name="p6976113017577"></a><a name="p6976113017577"></a>application/x-pcx</p>
</td>
</tr>
<tr id="row68911230217"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p149771630115718"><a name="p149771630115718"></a><a name="p149771630115718"></a>.pdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14977123016573"><a name="p14977123016573"></a><a name="p14977123016573"></a>application/pdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p16977123025720"><a name="p16977123025720"></a><a name="p16977123025720"></a>.pdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p159771330145711"><a name="p159771330145711"></a><a name="p159771330145711"></a>application/pdf</p>
</td>
</tr>
<tr id="row18891203016116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p139771530135718"><a name="p139771530135718"></a><a name="p139771530135718"></a>.pdx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p19977183011576"><a name="p19977183011576"></a><a name="p19977183011576"></a>application/vnd.adobe.pdx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p7977133045711"><a name="p7977133045711"></a><a name="p7977133045711"></a>.pfx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1397710304573"><a name="p1397710304573"></a><a name="p1397710304573"></a>application/x-pkcs12</p>
</td>
</tr>
<tr id="row108918301212"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p9977193010570"><a name="p9977193010570"></a><a name="p9977193010570"></a>.pgl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p5977203065717"><a name="p5977203065717"></a><a name="p5977203065717"></a>application/x-pgl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p797711309579"><a name="p797711309579"></a><a name="p797711309579"></a>.pic</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p797716304573"><a name="p797716304573"></a><a name="p797716304573"></a>application/x-pic</p>
</td>
</tr>
<tr id="row1189123012114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p199771130165710"><a name="p199771130165710"></a><a name="p199771130165710"></a>.pko</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1977173017575"><a name="p1977173017575"></a><a name="p1977173017575"></a>application/vnd.ms-pki.pko</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p99771230125718"><a name="p99771230125718"></a><a name="p99771230125718"></a>.pl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p997793085717"><a name="p997793085717"></a><a name="p997793085717"></a>application/x-perl</p>
</td>
</tr>
<tr id="row989115304118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p10977630115719"><a name="p10977630115719"></a><a name="p10977630115719"></a>.plg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1497783013579"><a name="p1497783013579"></a><a name="p1497783013579"></a>text/html</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1197743045711"><a name="p1197743045711"></a><a name="p1197743045711"></a>.pls</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p297733045711"><a name="p297733045711"></a><a name="p297733045711"></a>audio/scpls</p>
</td>
</tr>
<tr id="row1889118303117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1597718304572"><a name="p1597718304572"></a><a name="p1597718304572"></a>.plt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p169779309571"><a name="p169779309571"></a><a name="p169779309571"></a>application/x-plt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1197814306576"><a name="p1197814306576"></a><a name="p1197814306576"></a>.png</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2978830185717"><a name="p2978830185717"></a><a name="p2978830185717"></a>image/png</p>
</td>
</tr>
<tr id="row148921130013"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p199781630125710"><a name="p199781630125710"></a><a name="p199781630125710"></a>.png</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14978183055715"><a name="p14978183055715"></a><a name="p14978183055715"></a>application/x-png</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p11978133011571"><a name="p11978133011571"></a><a name="p11978133011571"></a>.pot</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p7978113015711"><a name="p7978113015711"></a><a name="p7978113015711"></a>application/vnd.ms-powerpoint</p>
</td>
</tr>
<tr id="row08920301516"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p16978113095714"><a name="p16978113095714"></a><a name="p16978113095714"></a>.ppa</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1978930105711"><a name="p1978930105711"></a><a name="p1978930105711"></a>application/vnd.ms-powerpoint</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1978183012574"><a name="p1978183012574"></a><a name="p1978183012574"></a>.ppm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p797893005713"><a name="p797893005713"></a><a name="p797893005713"></a>application/x-ppm</p>
</td>
</tr>
<tr id="row38929301116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p19978630175716"><a name="p19978630175716"></a><a name="p19978630175716"></a>.pps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p197833017579"><a name="p197833017579"></a><a name="p197833017579"></a>application/vnd.ms-powerpoint</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p13978113075710"><a name="p13978113075710"></a><a name="p13978113075710"></a>.ppt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p79782305570"><a name="p79782305570"></a><a name="p79782305570"></a>application/vnd.ms-powerpoint</p>
</td>
</tr>
<tr id="row118921830919"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1497873010573"><a name="p1497873010573"></a><a name="p1497873010573"></a>.ppt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p397810309573"><a name="p397810309573"></a><a name="p397810309573"></a>application/x-ppt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p2978133035710"><a name="p2978133035710"></a><a name="p2978133035710"></a>.pr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p159781730125715"><a name="p159781730125715"></a><a name="p159781730125715"></a>application/x-pr</p>
</td>
</tr>
<tr id="row88921730115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p10978113018577"><a name="p10978113018577"></a><a name="p10978113018577"></a>.prf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p39781430105718"><a name="p39781430105718"></a><a name="p39781430105718"></a>application/pics-rules</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p197833015717"><a name="p197833015717"></a><a name="p197833015717"></a>.prn</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p5978143035711"><a name="p5978143035711"></a><a name="p5978143035711"></a>application/x-prn</p>
</td>
</tr>
<tr id="row15892153019117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p8978133095719"><a name="p8978133095719"></a><a name="p8978133095719"></a>.prt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p497820300574"><a name="p497820300574"></a><a name="p497820300574"></a>application/x-prt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p297863075712"><a name="p297863075712"></a><a name="p297863075712"></a>.ps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p16978183016574"><a name="p16978183016574"></a><a name="p16978183016574"></a>application/x-ps</p>
</td>
</tr>
<tr id="row3892163014118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p29801530165710"><a name="p29801530165710"></a><a name="p29801530165710"></a>.ps</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p798016306573"><a name="p798016306573"></a><a name="p798016306573"></a>application/postscript</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15980113014577"><a name="p15980113014577"></a><a name="p15980113014577"></a>.ptn</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1398013019573"><a name="p1398013019573"></a><a name="p1398013019573"></a>application/x-ptn</p>
</td>
</tr>
<tr id="row1189217305118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1798043015575"><a name="p1798043015575"></a><a name="p1798043015575"></a>.pwz</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p498014302575"><a name="p498014302575"></a><a name="p498014302575"></a>application/vnd.ms-powerpoint</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p179802308573"><a name="p179802308573"></a><a name="p179802308573"></a>.r3t</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2981103010570"><a name="p2981103010570"></a><a name="p2981103010570"></a>text/vnd.rn-realtext3d</p>
</td>
</tr>
<tr id="row16892230514"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p36962565818"><a name="p36962565818"></a><a name="p36962565818"></a>.ra</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p12614152785910"><a name="p12614152785910"></a><a name="p12614152785910"></a>audio/vnd.rn-realaudio</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p09811930165715"><a name="p09811930165715"></a><a name="p09811930165715"></a>.ram</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19145317016"><a name="p19145317016"></a><a name="p19145317016"></a>audio/x-pn-realaudio</p>
</td>
</tr>
<tr id="row689312305113"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p43331940426"><a name="p43331940426"></a><a name="p43331940426"></a>.ras</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p183331401826"><a name="p183331401826"></a><a name="p183331401826"></a>application/x-ras</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p633374020217"><a name="p633374020217"></a><a name="p633374020217"></a>.rat</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p153331401227"><a name="p153331401227"></a><a name="p153331401227"></a>application/rat-file</p>
</td>
</tr>
<tr id="row11893103019114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p933414402214"><a name="p933414402214"></a><a name="p933414402214"></a>.rdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p143341640129"><a name="p143341640129"></a><a name="p143341640129"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1633416401721"><a name="p1633416401721"></a><a name="p1633416401721"></a>.rec</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p83349401726"><a name="p83349401726"></a><a name="p83349401726"></a>application/vnd.rn-recording</p>
</td>
</tr>
<tr id="row1489373012114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1033417401026"><a name="p1033417401026"></a><a name="p1033417401026"></a>.red</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p2033417401720"><a name="p2033417401720"></a><a name="p2033417401720"></a>application/x-red</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15334194020218"><a name="p15334194020218"></a><a name="p15334194020218"></a>.rgb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p173341540824"><a name="p173341540824"></a><a name="p173341540824"></a>application/x-rgb</p>
</td>
</tr>
<tr id="row189314301515"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p03343401523"><a name="p03343401523"></a><a name="p03343401523"></a>.rjs</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p3334240928"><a name="p3334240928"></a><a name="p3334240928"></a>application/vnd.rn-realsystem-rjs</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p17334154010214"><a name="p17334154010214"></a><a name="p17334154010214"></a>.rjt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p10334144010211"><a name="p10334144010211"></a><a name="p10334144010211"></a>application/vnd.rn-realsystem-rjt</p>
</td>
</tr>
<tr id="row1689315303117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p833414407211"><a name="p833414407211"></a><a name="p833414407211"></a>.rlc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1233420405218"><a name="p1233420405218"></a><a name="p1233420405218"></a>application/x-rlc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p833474018214"><a name="p833474018214"></a><a name="p833474018214"></a>.rle</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p173342404216"><a name="p173342404216"></a><a name="p173342404216"></a>application/x-rle</p>
</td>
</tr>
<tr id="row8893830013"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p93345406216"><a name="p93345406216"></a><a name="p93345406216"></a>.rm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1333413408215"><a name="p1333413408215"></a><a name="p1333413408215"></a>application/vnd.rn-realmedia</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1733404010216"><a name="p1733404010216"></a><a name="p1733404010216"></a>.rmf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p173341640526"><a name="p173341640526"></a><a name="p173341640526"></a>application/vnd.adobe.rmf</p>
</td>
</tr>
<tr id="row9893430719"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p163346400220"><a name="p163346400220"></a><a name="p163346400220"></a>.rmi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p173348401625"><a name="p173348401625"></a><a name="p173348401625"></a>audio/mid</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1033413401222"><a name="p1033413401222"></a><a name="p1033413401222"></a>.rmj</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p133342404214"><a name="p133342404214"></a><a name="p133342404214"></a>application/vnd.rn-realsystem-rmj</p>
</td>
</tr>
<tr id="row5893163019115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p733494017220"><a name="p733494017220"></a><a name="p733494017220"></a>.rmm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p103345401325"><a name="p103345401325"></a><a name="p103345401325"></a>audio/x-pn-realaudio</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p033420400219"><a name="p033420400219"></a><a name="p033420400219"></a>.rmp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1233414401723"><a name="p1233414401723"></a><a name="p1233414401723"></a>application/vnd.rn-rn_music_package</p>
</td>
</tr>
<tr id="row28936301118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p533454012213"><a name="p533454012213"></a><a name="p533454012213"></a>.rms</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p73344401421"><a name="p73344401421"></a><a name="p73344401421"></a>application/vnd.rn-realmedia-secure</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p4334134010213"><a name="p4334134010213"></a><a name="p4334134010213"></a>.rmvb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1233510401823"><a name="p1233510401823"></a><a name="p1233510401823"></a>application/vnd.rn-realmedia-vbr</p>
</td>
</tr>
<tr id="row108931930419"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1933512403214"><a name="p1933512403214"></a><a name="p1933512403214"></a>.rmx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p143352040622"><a name="p143352040622"></a><a name="p143352040622"></a>application/vnd.rn-realsystem-rmx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p13335104017217"><a name="p13335104017217"></a><a name="p13335104017217"></a>.rnx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p933518401122"><a name="p933518401122"></a><a name="p933518401122"></a>application/vnd.rn-realplayer</p>
</td>
</tr>
<tr id="row6894430619"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p533516403214"><a name="p533516403214"></a><a name="p533516403214"></a>.rp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p2033510401422"><a name="p2033510401422"></a><a name="p2033510401422"></a>image/vnd.rn-realpix</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p163353401926"><a name="p163353401926"></a><a name="p163353401926"></a>.rpm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p033516401227"><a name="p033516401227"></a><a name="p033516401227"></a>audio/x-pn-realaudio-plugin</p>
</td>
</tr>
<tr id="row1789411300120"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p18335144013219"><a name="p18335144013219"></a><a name="p18335144013219"></a>.rsml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p2335640124"><a name="p2335640124"></a><a name="p2335640124"></a>application/vnd.rn-rsml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p93358401328"><a name="p93358401328"></a><a name="p93358401328"></a>.rt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p133516401626"><a name="p133516401626"></a><a name="p133516401626"></a>text/vnd.rn-realtext</p>
</td>
</tr>
<tr id="row189415308119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1733514406218"><a name="p1733514406218"></a><a name="p1733514406218"></a>.rtf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p10335440023"><a name="p10335440023"></a><a name="p10335440023"></a>application/msword</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p113359402212"><a name="p113359402212"></a><a name="p113359402212"></a>.rtf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1333514401329"><a name="p1333514401329"></a><a name="p1333514401329"></a>application/x-rtf</p>
</td>
</tr>
<tr id="row389411308117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p83351640428"><a name="p83351640428"></a><a name="p83351640428"></a>.rv</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p133514020211"><a name="p133514020211"></a><a name="p133514020211"></a>video/vnd.rn-realvideo</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p7335184018210"><a name="p7335184018210"></a><a name="p7335184018210"></a>.sam</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p33351340829"><a name="p33351340829"></a><a name="p33351340829"></a>application/x-sam</p>
</td>
</tr>
<tr id="row1489418309116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p143351406211"><a name="p143351406211"></a><a name="p143351406211"></a>.sat</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p173358404219"><a name="p173358404219"></a><a name="p173358404219"></a>application/x-sat</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p14335174018210"><a name="p14335174018210"></a><a name="p14335174018210"></a>.sdp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p833511401214"><a name="p833511401214"></a><a name="p833511401214"></a>application/sdp</p>
</td>
</tr>
<tr id="row589414301513"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p73351340822"><a name="p73351340822"></a><a name="p73351340822"></a>.sdw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p183357401022"><a name="p183357401022"></a><a name="p183357401022"></a>application/x-sdw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p133513408215"><a name="p133513408215"></a><a name="p133513408215"></a>.sit</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p23356401225"><a name="p23356401225"></a><a name="p23356401225"></a>application/x-stuffit</p>
</td>
</tr>
<tr id="row138949305114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p2033511401822"><a name="p2033511401822"></a><a name="p2033511401822"></a>.slb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p133359402213"><a name="p133359402213"></a><a name="p133359402213"></a>application/x-slb</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1133644013215"><a name="p1133644013215"></a><a name="p1133644013215"></a>.sld</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p3336140824"><a name="p3336140824"></a><a name="p3336140824"></a>application/x-sld</p>
</td>
</tr>
<tr id="row98947304117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1433617407217"><a name="p1433617407217"></a><a name="p1433617407217"></a>.slk</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p14336940920"><a name="p14336940920"></a><a name="p14336940920"></a>drawing/x-slk</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p9336134016216"><a name="p9336134016216"></a><a name="p9336134016216"></a>.smi</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1433612404216"><a name="p1433612404216"></a><a name="p1433612404216"></a>application/smil</p>
</td>
</tr>
<tr id="row4895130618"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1333614408212"><a name="p1333614408212"></a><a name="p1333614408212"></a>.smil</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p633615403211"><a name="p633615403211"></a><a name="p633615403211"></a>application/smil</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p163361440220"><a name="p163361440220"></a><a name="p163361440220"></a>.smk</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1433618405210"><a name="p1433618405210"></a><a name="p1433618405210"></a>application/x-smk</p>
</td>
</tr>
<tr id="row58955301312"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p23361740929"><a name="p23361740929"></a><a name="p23361740929"></a>.snd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1333664016210"><a name="p1333664016210"></a><a name="p1333664016210"></a>audio/basic</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p633620401828"><a name="p633620401828"></a><a name="p633620401828"></a>.sol</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p93376401225"><a name="p93376401225"></a><a name="p93376401225"></a>text/plain</p>
</td>
</tr>
<tr id="row1789583015115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p533719406213"><a name="p533719406213"></a><a name="p533719406213"></a>.sor</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p633710403213"><a name="p633710403213"></a><a name="p633710403213"></a>text/plain</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p173371940421"><a name="p173371940421"></a><a name="p173371940421"></a>.spc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1033716401528"><a name="p1033716401528"></a><a name="p1033716401528"></a>application/x-pkcs7-certificates</p>
</td>
</tr>
<tr id="row19895930213"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1533719401127"><a name="p1533719401127"></a><a name="p1533719401127"></a>.spl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p13375401219"><a name="p13375401219"></a><a name="p13375401219"></a>application/futuresplash</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1433717407217"><a name="p1433717407217"></a><a name="p1433717407217"></a>.spp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p113371840921"><a name="p113371840921"></a><a name="p113371840921"></a>text/xml</p>
</td>
</tr>
<tr id="row19895153013112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p143376405218"><a name="p143376405218"></a><a name="p143376405218"></a>.ssm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p8337240220"><a name="p8337240220"></a><a name="p8337240220"></a>application/streamingmedia</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p833744011214"><a name="p833744011214"></a><a name="p833744011214"></a>.sst</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p10337134014216"><a name="p10337134014216"></a><a name="p10337134014216"></a>application/vnd.ms-pki.certstore</p>
</td>
</tr>
<tr id="row19895203017114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p123378409219"><a name="p123378409219"></a><a name="p123378409219"></a>.stl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p533715401822"><a name="p533715401822"></a><a name="p533715401822"></a>application/vnd.ms-pki.stl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1333724018215"><a name="p1333724018215"></a><a name="p1333724018215"></a>.stm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p10337134019215"><a name="p10337134019215"></a><a name="p10337134019215"></a>text/html</p>
</td>
</tr>
<tr id="row1489515302018"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p53371840427"><a name="p53371840427"></a><a name="p53371840427"></a>.sty</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p633717401122"><a name="p633717401122"></a><a name="p633717401122"></a>application/x-sty</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1133719401928"><a name="p1133719401928"></a><a name="p1133719401928"></a>.svg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p17337640923"><a name="p17337640923"></a><a name="p17337640923"></a>text/xml</p>
</td>
</tr>
<tr id="row15895130715"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p53374401923"><a name="p53374401923"></a><a name="p53374401923"></a>.swf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p533711404210"><a name="p533711404210"></a><a name="p533711404210"></a>application/x-shockwave-flash</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p633814408215"><a name="p633814408215"></a><a name="p633814408215"></a>.tdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p4338640922"><a name="p4338640922"></a><a name="p4338640922"></a>application/x-tdf</p>
</td>
</tr>
<tr id="row189523013117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1433814017213"><a name="p1433814017213"></a><a name="p1433814017213"></a>.tg4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p5338144020214"><a name="p5338144020214"></a><a name="p5338144020214"></a>application/x-tg4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p14338194014213"><a name="p14338194014213"></a><a name="p14338194014213"></a>.tga</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p533810401022"><a name="p533810401022"></a><a name="p533810401022"></a>application/x-tga</p>
</td>
</tr>
<tr id="row98957305118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p203383401526"><a name="p203383401526"></a><a name="p203383401526"></a>.tif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p12338114017219"><a name="p12338114017219"></a><a name="p12338114017219"></a>image/tiff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15338164018213"><a name="p15338164018213"></a><a name="p15338164018213"></a>.tif</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p5338174020216"><a name="p5338174020216"></a><a name="p5338174020216"></a>application/x-tif</p>
</td>
</tr>
<tr id="row1189612301813"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1533874013215"><a name="p1533874013215"></a><a name="p1533874013215"></a>.tiff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1933814011217"><a name="p1933814011217"></a><a name="p1933814011217"></a>image/tiff</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p113381407219"><a name="p113381407219"></a><a name="p113381407219"></a>.tld</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p183383401620"><a name="p183383401620"></a><a name="p183383401620"></a>text/xml</p>
</td>
</tr>
<tr id="row1089610301617"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1733816401029"><a name="p1733816401029"></a><a name="p1733816401029"></a>.top</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1933818407216"><a name="p1933818407216"></a><a name="p1933818407216"></a>drawing/x-top</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p133894014213"><a name="p133894014213"></a><a name="p133894014213"></a>.torrent</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9338740221"><a name="p9338740221"></a><a name="p9338740221"></a>application/x-bittorrent</p>
</td>
</tr>
<tr id="row16896530914"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p0338340624"><a name="p0338340624"></a><a name="p0338340624"></a>.tsd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p8338154010215"><a name="p8338154010215"></a><a name="p8338154010215"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p43388401623"><a name="p43388401623"></a><a name="p43388401623"></a>.txt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p533819401421"><a name="p533819401421"></a><a name="p533819401421"></a>text/plain</p>
</td>
</tr>
<tr id="row289616301218"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1933834013219"><a name="p1933834013219"></a><a name="p1933834013219"></a>.uin</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1933816406214"><a name="p1933816406214"></a><a name="p1933816406214"></a>application/x-icq</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p173382040823"><a name="p173382040823"></a><a name="p173382040823"></a>.uls</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p123381040427"><a name="p123381040427"></a><a name="p123381040427"></a>text/iuls</p>
</td>
</tr>
<tr id="row20896153013116"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p233811405216"><a name="p233811405216"></a><a name="p233811405216"></a>.vcf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p123381440121"><a name="p123381440121"></a><a name="p123381440121"></a>text/x-vcard</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p53384400218"><a name="p53384400218"></a><a name="p53384400218"></a>.vda</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p4338174018218"><a name="p4338174018218"></a><a name="p4338174018218"></a>application/x-vda</p>
</td>
</tr>
<tr id="row2089683010117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1033813401323"><a name="p1033813401323"></a><a name="p1033813401323"></a>.vdx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p173391940829"><a name="p173391940829"></a><a name="p173391940829"></a>application/vnd.visio</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p5339184012211"><a name="p5339184012211"></a><a name="p5339184012211"></a>.vml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1833915401223"><a name="p1833915401223"></a><a name="p1833915401223"></a>text/xml</p>
</td>
</tr>
<tr id="row9896430912"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p478710584218"><a name="p478710584218"></a><a name="p478710584218"></a>.vpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p10787758424"><a name="p10787758424"></a><a name="p10787758424"></a>application/x-vpeg005</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p37876581622"><a name="p37876581622"></a><a name="p37876581622"></a>.vsd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p2787125812213"><a name="p2787125812213"></a><a name="p2787125812213"></a>application/vnd.visio</p>
</td>
</tr>
<tr id="row68961930319"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p978885819218"><a name="p978885819218"></a><a name="p978885819218"></a>.vsd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p37881458527"><a name="p37881458527"></a><a name="p37881458527"></a>application/x-vsd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p157881586212"><a name="p157881586212"></a><a name="p157881586212"></a>.vss</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p37888585219"><a name="p37888585219"></a><a name="p37888585219"></a>application/vnd.visio</p>
</td>
</tr>
<tr id="row15896133020111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p8788115818220"><a name="p8788115818220"></a><a name="p8788115818220"></a>.vst</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1978811581325"><a name="p1978811581325"></a><a name="p1978811581325"></a>application/vnd.visio</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p478855816216"><a name="p478855816216"></a><a name="p478855816216"></a>.vst</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p17889584216"><a name="p17889584216"></a><a name="p17889584216"></a>application/x-vst</p>
</td>
</tr>
<tr id="row1989611301013"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p478865813211"><a name="p478865813211"></a><a name="p478865813211"></a>.vsw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1178817584210"><a name="p1178817584210"></a><a name="p1178817584210"></a>application/vnd.visio</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p187881758824"><a name="p187881758824"></a><a name="p187881758824"></a>.vsx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p9788195817215"><a name="p9788195817215"></a><a name="p9788195817215"></a>application/vnd.visio</p>
</td>
</tr>
<tr id="row289713010111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1878815581925"><a name="p1878815581925"></a><a name="p1878815581925"></a>.vtx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p47881058522"><a name="p47881058522"></a><a name="p47881058522"></a>application/vnd.visio</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p978805820214"><a name="p978805820214"></a><a name="p978805820214"></a>.vxml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p878817584216"><a name="p878817584216"></a><a name="p878817584216"></a>text/xml</p>
</td>
</tr>
<tr id="row178971230211"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1378865815219"><a name="p1378865815219"></a><a name="p1378865815219"></a>.wav</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1778812581028"><a name="p1778812581028"></a><a name="p1778812581028"></a>audio/wav</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p178815811214"><a name="p178815811214"></a><a name="p178815811214"></a>.wax</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1178875818219"><a name="p1178875818219"></a><a name="p1178875818219"></a>audio/x-ms-wax</p>
</td>
</tr>
<tr id="row889710302112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p6788145811218"><a name="p6788145811218"></a><a name="p6788145811218"></a>.wb1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1878813581526"><a name="p1878813581526"></a><a name="p1878813581526"></a>application/x-wb1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p167882581821"><a name="p167882581821"></a><a name="p167882581821"></a>.wb2</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1788158020"><a name="p1788158020"></a><a name="p1788158020"></a>application/x-wb2</p>
</td>
</tr>
<tr id="row389716301312"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p117884581223"><a name="p117884581223"></a><a name="p117884581223"></a>.wb3</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p27880583210"><a name="p27880583210"></a><a name="p27880583210"></a>application/x-wb3</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p12788125817212"><a name="p12788125817212"></a><a name="p12788125817212"></a>.wbmp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1478810581222"><a name="p1478810581222"></a><a name="p1478810581222"></a>image/vnd.wap.wbmp</p>
</td>
</tr>
<tr id="row20897030819"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1778815589218"><a name="p1778815589218"></a><a name="p1778815589218"></a>.wiz</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p97887586210"><a name="p97887586210"></a><a name="p97887586210"></a>application/msword</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1578945819212"><a name="p1578945819212"></a><a name="p1578945819212"></a>.wk3</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p67897588219"><a name="p67897588219"></a><a name="p67897588219"></a>application/x-wk3</p>
</td>
</tr>
<tr id="row3897730219"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p187891658123"><a name="p187891658123"></a><a name="p187891658123"></a>.wk4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p15789658123"><a name="p15789658123"></a><a name="p15789658123"></a>application/x-wk4</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p12789858926"><a name="p12789858926"></a><a name="p12789858926"></a>.wkq</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p167891558725"><a name="p167891558725"></a><a name="p167891558725"></a>application/x-wkq</p>
</td>
</tr>
<tr id="row089773019112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1978955816214"><a name="p1978955816214"></a><a name="p1978955816214"></a>.wks</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p578915582211"><a name="p578915582211"></a><a name="p578915582211"></a>application/x-wks</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p17789205815217"><a name="p17789205815217"></a><a name="p17789205815217"></a>.wm</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p13789115815218"><a name="p13789115815218"></a><a name="p13789115815218"></a>video/x-ms-wm</p>
</td>
</tr>
<tr id="row8897630815"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p978925812220"><a name="p978925812220"></a><a name="p978925812220"></a>.wma</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p177899583214"><a name="p177899583214"></a><a name="p177899583214"></a>audio/x-ms-wma</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p378915810214"><a name="p378915810214"></a><a name="p378915810214"></a>.wmd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p7789115817213"><a name="p7789115817213"></a><a name="p7789115817213"></a>application/x-ms-wmd</p>
</td>
</tr>
<tr id="row789753013112"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p107891658226"><a name="p107891658226"></a><a name="p107891658226"></a>.wmf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1978911587213"><a name="p1978911587213"></a><a name="p1978911587213"></a>application/x-wmf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p478995812213"><a name="p478995812213"></a><a name="p478995812213"></a>.wml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1078919587218"><a name="p1078919587218"></a><a name="p1078919587218"></a>text/vnd.wap.wml</p>
</td>
</tr>
<tr id="row208971301918"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p17895586214"><a name="p17895586214"></a><a name="p17895586214"></a>.wmv</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1678985820215"><a name="p1678985820215"></a><a name="p1678985820215"></a>video/x-ms-wmv</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p07891758229"><a name="p07891758229"></a><a name="p07891758229"></a>.wmx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p47891058621"><a name="p47891058621"></a><a name="p47891058621"></a>video/x-ms-wmx</p>
</td>
</tr>
<tr id="row188981030518"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p13789175816214"><a name="p13789175816214"></a><a name="p13789175816214"></a>.wmz</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1378919581024"><a name="p1378919581024"></a><a name="p1378919581024"></a>application/x-ms-wmz</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p177891580212"><a name="p177891580212"></a><a name="p177891580212"></a>.wp6</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1878911581928"><a name="p1878911581928"></a><a name="p1878911581928"></a>application/x-wp6</p>
</td>
</tr>
<tr id="row5898530514"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p47893581828"><a name="p47893581828"></a><a name="p47893581828"></a>.wpd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1978925818218"><a name="p1978925818218"></a><a name="p1978925818218"></a>application/x-wpd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1478915589219"><a name="p1478915589219"></a><a name="p1478915589219"></a>.wpg</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1789165810218"><a name="p1789165810218"></a><a name="p1789165810218"></a>application/x-wpg</p>
</td>
</tr>
<tr id="row289813301414"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1379055812214"><a name="p1379055812214"></a><a name="p1379055812214"></a>.wpl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p57909580212"><a name="p57909580212"></a><a name="p57909580212"></a>application/vnd.ms-wpl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p2079015581222"><a name="p2079015581222"></a><a name="p2079015581222"></a>.wq1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p16790258520"><a name="p16790258520"></a><a name="p16790258520"></a>application/x-wq1</p>
</td>
</tr>
<tr id="row889810301616"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p12790758825"><a name="p12790758825"></a><a name="p12790758825"></a>.wr1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p17901658625"><a name="p17901658625"></a><a name="p17901658625"></a>application/x-wr1</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p87900581221"><a name="p87900581221"></a><a name="p87900581221"></a>.wri</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p579005811216"><a name="p579005811216"></a><a name="p579005811216"></a>application/x-wri</p>
</td>
</tr>
<tr id="row789893017119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p27908589213"><a name="p27908589213"></a><a name="p27908589213"></a>.wrk</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p87908583218"><a name="p87908583218"></a><a name="p87908583218"></a>application/x-wrk</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p14790958129"><a name="p14790958129"></a><a name="p14790958129"></a>.ws</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p157901758523"><a name="p157901758523"></a><a name="p157901758523"></a>application/x-ws</p>
</td>
</tr>
<tr id="row1489823015119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p37905589212"><a name="p37905589212"></a><a name="p37905589212"></a>.ws2</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1279013581524"><a name="p1279013581524"></a><a name="p1279013581524"></a>application/x-ws</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p37906581327"><a name="p37906581327"></a><a name="p37906581327"></a>.wsc</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p579010581720"><a name="p579010581720"></a><a name="p579010581720"></a>text/scriptlet</p>
</td>
</tr>
<tr id="row4898163012118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p207901458221"><a name="p207901458221"></a><a name="p207901458221"></a>.wsdl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p879013581321"><a name="p879013581321"></a><a name="p879013581321"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p679015817212"><a name="p679015817212"></a><a name="p679015817212"></a>.wvx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p679014581029"><a name="p679014581029"></a><a name="p679014581029"></a>video/x-ms-wvx</p>
</td>
</tr>
<tr id="row889818301915"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p187937108312"><a name="p187937108312"></a><a name="p187937108312"></a>.xdp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p179314101320"><a name="p179314101320"></a><a name="p179314101320"></a>application/vnd.adobe.xdp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p177931310438"><a name="p177931310438"></a><a name="p177931310438"></a>.xdr</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p77936101234"><a name="p77936101234"></a><a name="p77936101234"></a>text/xml</p>
</td>
</tr>
<tr id="row1389853018117"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p147931101631"><a name="p147931101631"></a><a name="p147931101631"></a>.xfd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p27930101134"><a name="p27930101134"></a><a name="p27930101134"></a>application/vnd.adobe.xfd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p87931110830"><a name="p87931110830"></a><a name="p87931110830"></a>.xfdf</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p679318100312"><a name="p679318100312"></a><a name="p679318100312"></a>application/vnd.adobe.xfdf</p>
</td>
</tr>
<tr id="row1489813019111"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p17931910536"><a name="p17931910536"></a><a name="p17931910536"></a>.xhtml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1079310101935"><a name="p1079310101935"></a><a name="p1079310101935"></a>text/html</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p4794610236"><a name="p4794610236"></a><a name="p4794610236"></a>.xls</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p979418102316"><a name="p979418102316"></a><a name="p979418102316"></a>application/vnd.ms-excel</p>
</td>
</tr>
<tr id="row389915304118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p37942104319"><a name="p37942104319"></a><a name="p37942104319"></a>.xls</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p079481017317"><a name="p079481017317"></a><a name="p079481017317"></a>application/x-xls</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1579410101631"><a name="p1579410101631"></a><a name="p1579410101631"></a>.xlw</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p107948101531"><a name="p107948101531"></a><a name="p107948101531"></a>application/x-xlw</p>
</td>
</tr>
<tr id="row38995301413"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1579413101319"><a name="p1579413101319"></a><a name="p1579413101319"></a>.xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p137942108318"><a name="p137942108318"></a><a name="p137942108318"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p117947104318"><a name="p117947104318"></a><a name="p117947104318"></a>.xpl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p17794510236"><a name="p17794510236"></a><a name="p17794510236"></a>audio/scpls</p>
</td>
</tr>
<tr id="row19899123010118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p5794111018319"><a name="p5794111018319"></a><a name="p5794111018319"></a>.xq</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1179416104318"><a name="p1179416104318"></a><a name="p1179416104318"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p167941010937"><a name="p167941010937"></a><a name="p167941010937"></a>.xql</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19794191014314"><a name="p19794191014314"></a><a name="p19794191014314"></a>text/xml</p>
</td>
</tr>
<tr id="row489920300118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p179418101638"><a name="p179418101638"></a><a name="p179418101638"></a>.xquery</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p9794101017312"><a name="p9794101017312"></a><a name="p9794101017312"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18794310639"><a name="p18794310639"></a><a name="p18794310639"></a>.xsd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p19794101014314"><a name="p19794101014314"></a><a name="p19794101014314"></a>text/xml</p>
</td>
</tr>
<tr id="row16899630518"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p77946101737"><a name="p77946101737"></a><a name="p77946101737"></a>.xsl</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p1879417108314"><a name="p1879417108314"></a><a name="p1879417108314"></a>text/xml</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p479410104317"><a name="p479410104317"></a><a name="p479410104317"></a>.xslt</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p187947101337"><a name="p187947101337"></a><a name="p187947101337"></a>text/xml</p>
</td>
</tr>
<tr id="row8899730912"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p16794710537"><a name="p16794710537"></a><a name="p16794710537"></a>.xwd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p197941110137"><a name="p197941110137"></a><a name="p197941110137"></a>application/x-xwd</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p15794181018318"><a name="p15794181018318"></a><a name="p15794181018318"></a>.x_b</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p1379410101310"><a name="p1379410101310"></a><a name="p1379410101310"></a>application/x-x_b</p>
</td>
</tr>
<tr id="row789920308118"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p17948101733"><a name="p17948101733"></a><a name="p17948101733"></a>.sis</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p879420103312"><a name="p879420103312"></a><a name="p879420103312"></a>application/vnd.symbian.install</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p18794191010318"><a name="p18794191010318"></a><a name="p18794191010318"></a>.sisx</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p11795910139"><a name="p11795910139"></a><a name="p11795910139"></a>application/vnd.symbian.install</p>
</td>
</tr>
<tr id="row589913011115"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p1079541011313"><a name="p1079541011313"></a><a name="p1079541011313"></a>.x_t</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p197951810536"><a name="p197951810536"></a><a name="p197951810536"></a>application/x-x_t</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1979561018311"><a name="p1979561018311"></a><a name="p1979561018311"></a>.ipa</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p97954104320"><a name="p97954104320"></a><a name="p97954104320"></a>application/vnd.iphone</p>
</td>
</tr>
<tr id="row18899183018119"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.1 "><p id="p11795161012310"><a name="p11795161012310"></a><a name="p11795161012310"></a>.apk</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.2 "><p id="p177952101331"><a name="p177952101331"></a><a name="p177952101331"></a>application/vnd.android.package-archive</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.3 "><p id="p1179571010316"><a name="p1179571010316"></a><a name="p1179571010316"></a>.xap</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.5.1.4 "><p id="p479516105319"><a name="p479516105319"></a><a name="p479516105319"></a>application/x-silverlight-app</p>
</td>
</tr>
</tbody>
</table>

