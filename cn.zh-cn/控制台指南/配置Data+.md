# 配置Data+<a name="obs_03_0353"></a>

## 操作场景<a name="section9114740162419"></a>

当需要使用OBS提供的Data+服务对OBS内存储的数据，自动进行多项复杂任务（如解析、转码、截图等）处理时，可按照本节指导进行配置。

1.  您需要先[创建工作流](#section34825242413)，工作流可以自定义任务处理流程。
2.  再为工作流[创建事件触发器](#section187831529172915)，事件触发器为工作流设置执行条件，指定桶内什么数据在执行某类操作后开始执行工作流。

## 约束与限制<a name="section737030132316"></a>

请参见[Data+简介](Data+简介.md)。

## 创建工作流<a name="section34825242413"></a>

1.  在OBS管理控制台左侧导航栏选择“对象存储“。
2.  在桶列表单击待操作的桶，进入“概览”页面。
3.  在左侧导航栏选中“Data+”，进入“事件触发器”页面。
4.  单击列表上方的“创建工作流”，进入“工作流”页面。
5.  单击界面右上角的“创建工作流”，进入“工作流编排”页面。
6.  将左侧预置的模板或自定义的函数拖拽至编排区域，同时在右侧属性面板配置基本属性和动态参数，配置完成后图标将由白色填充变为蓝色填充。

    Data+目前提供三种视频处理模板（视频解析、抽帧截图、媒资转码）和一种消息通知模板（SMN消息通知），同时也支持事件延迟和用户自定义函数，满足用户的各种定制需求。

    -   视频解析

        模板作用：用于新建视频解析任务，以解析视频元数据。该模板实际调用的是MPC服务的[新建视频解析任务接口](https://support.huaweicloud.com/api-mpc/mpc_04_0061.html)。

        **表 1**  视频解析属性配置说明

        <a name="table17357102620414"></a>
        <table><thead align="left"><tr id="row16358172654115"><th class="cellrowborder" valign="top" width="15%" id="mcps1.2.4.1.1"><p id="p19358122619410"><a name="p19358122619410"></a><a name="p19358122619410"></a>属性类别</p>
        </th>
        <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.2"><p id="p113581267415"><a name="p113581267415"></a><a name="p113581267415"></a>参数名称</p>
        </th>
        <th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p18358172619414"><a name="p18358172619414"></a><a name="p18358172619414"></a>参数说明</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row1435812266412"><td class="cellrowborder" rowspan="4" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p103581826194119"><a name="p103581826194119"></a><a name="p103581826194119"></a>基本属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p335862614415"><a name="p335862614415"></a><a name="p335862614415"></a>名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p035819261412"><a name="p035819261412"></a><a name="p035819261412"></a>任务的名称，修改后将体现在工作流编排区域。</p>
        <a name="ul1186594422410"></a><a name="ul1186594422410"></a><ul id="ul1186594422410"><li>必须以字母或数字开头</li><li>只能由字母、数字、下划线和中划线组成</li><li>长度范围为1~20个字符</li><li>不能和同一工作流中的其他任务重名</li></ul>
        </td>
        </tr>
        <tr id="row15358112644113"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p435813269412"><a name="p435813269412"></a><a name="p435813269412"></a>超时(秒)</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p18697112611212"><a name="p18697112611212"></a><a name="p18697112611212"></a>任务超时时间，即任务执行的最长时间。</p>
        <p id="p93582026164118"><a name="p93582026164118"></a><a name="p93582026164118"></a>支持设置0~300秒的超时时间，如果设置为0，则表示超时时间为默认值30秒。</p>
        </td>
        </tr>
        <tr id="row93584268412"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p235872654116"><a name="p235872654116"></a><a name="p235872654116"></a>动作提供方</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p20358192624115"><a name="p20358192624115"></a><a name="p20358192624115"></a>函数模板的提供方。</p>
        </td>
        </tr>
        <tr id="row3358926124116"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p3358162613415"><a name="p3358162613415"></a><a name="p3358162613415"></a>错误处理</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p6358152615419"><a name="p6358152615419"></a><a name="p6358152615419"></a>可定义不同类型错误发生时的重试次数、重试间隔，以及重试失败后跳转到的目标任务。</p>
        <p id="p1690418154910"><a name="p1690418154910"></a><a name="p1690418154910"></a>错误类型包括：匹配所有、执行失败、权限不合法、参数不合法、函数不存在、请求太频繁、函数不可用、函数异常</p>
        </td>
        </tr>
        <tr id="row14358102618419"><td class="cellrowborder" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p8358126174110"><a name="p8358126174110"></a><a name="p8358126174110"></a>动态参数</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p14358172611419"><a name="p14358172611419"></a><a name="p14358172611419"></a>视频解析同步处理</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p7358102613417"><a name="p7358102613417"></a><a name="p7358102613417"></a>是否同步处理，只能为0或1。</p>
        <a name="ul1865415376472"></a><a name="ul1865415376472"></a><ul id="ul1865415376472"><li>0：排队处理。查询后仅返回任务ID，还需进一步调用<a href="https://support.huaweicloud.com/api-mpc/mpc_04_0062.html" target="_blank" rel="noopener noreferrer">查询视频解析任务接口</a>才能获取到视频元数据。</li><li>1：同步处理。查询后将直接返回视频元数据。</li></ul>
        </td>
        </tr>
        </tbody>
        </table>

    -   **抽帧截图**

        模板作用：用于新建视频截图任务，截取视频第2秒的图片。该模板实际调用的是MPC服务的[新建截图任务接口](https://support.huaweicloud.com/api-mpc/mpc_04_0034.html)。

        **表 2**  抽帧截图属性配置说明

        <a name="table149655216525"></a>
        <table><thead align="left"><tr id="row189655210522"><th class="cellrowborder" valign="top" width="15%" id="mcps1.2.4.1.1"><p id="p196592185210"><a name="p196592185210"></a><a name="p196592185210"></a>属性类别</p>
        </th>
        <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.2"><p id="p2096512215212"><a name="p2096512215212"></a><a name="p2096512215212"></a>参数名称</p>
        </th>
        <th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p29651295214"><a name="p29651295214"></a><a name="p29651295214"></a>参数说明</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row119655212525"><td class="cellrowborder" rowspan="4" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p1996518295213"><a name="p1996518295213"></a><a name="p1996518295213"></a>基本属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p1396518216528"><a name="p1396518216528"></a><a name="p1396518216528"></a>名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p396512245213"><a name="p396512245213"></a><a name="p396512245213"></a>任务的名称，修改后将体现在工作流编排区域。</p>
        <a name="ul1661574918244"></a><a name="ul1661574918244"></a><ul id="ul1661574918244"><li>必须以字母或数字开头</li><li>只能由字母、数字、下划线和中划线组成</li><li>长度范围为1~20个字符</li><li>不能和同一工作流中的其他任务重名</li></ul>
        </td>
        </tr>
        <tr id="row18965124526"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1965172175214"><a name="p1965172175214"></a><a name="p1965172175214"></a>超时(秒)</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p396542155212"><a name="p396542155212"></a><a name="p396542155212"></a>任务超时时间，即任务执行的最长时间。</p>
        <p id="p527851695716"><a name="p527851695716"></a><a name="p527851695716"></a>支持设置0~300秒的超时时间，如果设置为0，则表示超时时间为默认值30秒。</p>
        </td>
        </tr>
        <tr id="row1965628521"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p209654245217"><a name="p209654245217"></a><a name="p209654245217"></a>动作提供方</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p16965132165210"><a name="p16965132165210"></a><a name="p16965132165210"></a>函数模板的提供方。</p>
        </td>
        </tr>
        <tr id="row109651628528"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p59655235213"><a name="p59655235213"></a><a name="p59655235213"></a>错误处理</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1996511210522"><a name="p1996511210522"></a><a name="p1996511210522"></a>可定义不同类型错误发生时的重试次数、重试间隔，以及重试失败后跳转到的目标任务。</p>
        <p id="p1596515265210"><a name="p1596515265210"></a><a name="p1596515265210"></a>错误类型包括：匹配所有、执行失败、权限不合法、参数不合法、函数不存在、请求太频繁、函数不可用、函数异常</p>
        </td>
        </tr>
        <tr id="row1996522105210"><td class="cellrowborder" rowspan="2" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p49657216525"><a name="p49657216525"></a><a name="p49657216525"></a>动态参数</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p15965129525"><a name="p15965129525"></a><a name="p15965129525"></a>视频截图输出桶</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p396512212526"><a name="p396512212526"></a><a name="p396512212526"></a>使用MPC服务进行视频截图后，用于保存截图的OBS桶名。</p>
        <p id="p1842918239249"><a name="p1842918239249"></a><a name="p1842918239249"></a>输出桶需要和Data+工作流在同一区域，工作流所属区域为创建工作流的桶所属区域。例如工作流A是在桶A中创建的，则桶A的区域即为工作流A的区域。</p>
        </td>
        </tr>
        <tr id="row1844720290433"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p944792912434"><a name="p944792912434"></a><a name="p944792912434"></a>视频截图输出路径</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p79251558153014"><a name="p79251558153014"></a><a name="p79251558153014"></a>视频截图输出桶中存放视频截图的OBS桶的具体路径。</p>
        <p id="p64471329144320"><a name="p64471329144320"></a><a name="p64471329144320"></a>例如：输入abc或abc/，均表示截图存放在abc文件夹下，如果文件夹不存在，会自动新建。输出路径为空表示存放在桶的根目录。</p>
        </td>
        </tr>
        </tbody>
        </table>

    -   **媒资转码**

        模板作用：执行MPC服务的预置转码模板“DASH\_H.265\_4K\_低码\_1入9出”，将片源转为4K、2K、1080等码率的视频。该模板实际调用的是MPC服务的[新建转码任务接口](https://support.huaweicloud.com/api-mpc/mpc_04_0017.html)。

        **图 1**  转码模板<a name="fig4661163992118"></a>  
        ![](figures/转码模板.png "转码模板")

        **表 3**  媒资转码属性配置说明

        <a name="table173479835215"></a>
        <table><thead align="left"><tr id="row434713855217"><th class="cellrowborder" valign="top" width="15%" id="mcps1.2.4.1.1"><p id="p1734717875217"><a name="p1734717875217"></a><a name="p1734717875217"></a>属性类别</p>
        </th>
        <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.2"><p id="p11347158175218"><a name="p11347158175218"></a><a name="p11347158175218"></a>参数名称</p>
        </th>
        <th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p53476814523"><a name="p53476814523"></a><a name="p53476814523"></a>参数说明</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row133483818522"><td class="cellrowborder" rowspan="4" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p193483810522"><a name="p193483810522"></a><a name="p193483810522"></a>基本属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p12348158195211"><a name="p12348158195211"></a><a name="p12348158195211"></a>名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p5741615595"><a name="p5741615595"></a><a name="p5741615595"></a>任务的名称，修改后将体现在工作流编排区域。</p>
        <a name="ul14715163599"></a><a name="ul14715163599"></a><ul id="ul14715163599"><li>必须以字母或数字开头</li><li>只能由字母、数字、下划线和中划线组成</li><li>长度范围为1~20个字符</li><li>不能和同一工作流中的其他任务重名</li></ul>
        </td>
        </tr>
        <tr id="row1034868205211"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p103481825210"><a name="p103481825210"></a><a name="p103481825210"></a>超时(秒)</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p157191612594"><a name="p157191612594"></a><a name="p157191612594"></a>任务超时时间，即任务执行的最长时间。</p>
        <p id="p17516135910"><a name="p17516135910"></a><a name="p17516135910"></a>支持设置0~300秒的超时时间，如果设置为0，则表示超时时间为默认值30秒。</p>
        </td>
        </tr>
        <tr id="row134810819526"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1734817815213"><a name="p1734817815213"></a><a name="p1734817815213"></a>动作提供方</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p207816185919"><a name="p207816185919"></a><a name="p207816185919"></a>函数模板的提供方。</p>
        </td>
        </tr>
        <tr id="row103486811524"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p93481386528"><a name="p93481386528"></a><a name="p93481386528"></a>错误处理</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p47191615592"><a name="p47191615592"></a><a name="p47191615592"></a>可定义不同类型错误发生时的重试次数、重试间隔，以及重试失败后跳转到的目标任务。</p>
        <p id="p13714161597"><a name="p13714161597"></a><a name="p13714161597"></a>错误类型包括：匹配所有、执行失败、权限不合法、参数不合法、函数不存在、请求太频繁、函数不可用、函数异常</p>
        </td>
        </tr>
        <tr id="row1434811835216"><td class="cellrowborder" rowspan="2" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p20348118165212"><a name="p20348118165212"></a><a name="p20348118165212"></a>动态参数</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p1256132043018"><a name="p1256132043018"></a><a name="p1256132043018"></a>视频转码输出桶</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p45652073011"><a name="p45652073011"></a><a name="p45652073011"></a>使用MPC服务进行媒资转码后，用于保存转码后视频文件的OBS桶名。</p>
        <p id="p85612083016"><a name="p85612083016"></a><a name="p85612083016"></a>输出桶需要和Data+工作流在同一区域，工作流所属区域为创建工作流的桶所属区域。例如工作流A是在桶A中创建的，则桶A的区域即为工作流A的区域。</p>
        </td>
        </tr>
        <tr id="row142101952163317"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p135613206302"><a name="p135613206302"></a><a name="p135613206302"></a>视频转码输出路径</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1656132019309"><a name="p1656132019309"></a><a name="p1656132019309"></a>视频转码输出桶中存放转码后视频文件的OBS桶的具体路径。</p>
        <p id="p856820203018"><a name="p856820203018"></a><a name="p856820203018"></a>例如：输入abc或abc/，均表示截图存放在abc文件夹下，如果文件夹不存在，会自动新建。输出路径为空表示存放在桶的根目录。</p>
        </td>
        </tr>
        </tbody>
        </table>

    -   **SMN消息通知**

        模板作用：可用于在执行某项任务后，向SMN主题的订阅者发送通知。您可以在工作流的任意位置添加SMN消息通知，将上一个函数的执行结果发送给订阅者。

        **表 4**  SMN消息通知属性配置说明

        <a name="table129081812155210"></a>
        <table><thead align="left"><tr id="row09081012115218"><th class="cellrowborder" valign="top" width="15%" id="mcps1.2.4.1.1"><p id="p1908112155220"><a name="p1908112155220"></a><a name="p1908112155220"></a>属性类别</p>
        </th>
        <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.2"><p id="p9908151265214"><a name="p9908151265214"></a><a name="p9908151265214"></a>参数名称</p>
        </th>
        <th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p19088123520"><a name="p19088123520"></a><a name="p19088123520"></a>参数说明</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row109081712105213"><td class="cellrowborder" rowspan="4" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p3908161275217"><a name="p3908161275217"></a><a name="p3908161275217"></a>基本属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p59085126529"><a name="p59085126529"></a><a name="p59085126529"></a>名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p148615238597"><a name="p148615238597"></a><a name="p148615238597"></a>任务的名称，修改后将体现在工作流编排区域。</p>
        <a name="ul7861112355919"></a><a name="ul7861112355919"></a><ul id="ul7861112355919"><li>必须以字母或数字开头</li><li>只能由字母、数字、下划线和中划线组成</li><li>长度范围为1~20个字符</li><li>不能和同一工作流中的其他任务重名</li></ul>
        </td>
        </tr>
        <tr id="row139081012155212"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p189081121528"><a name="p189081121528"></a><a name="p189081121528"></a>超时(秒)</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p586172385912"><a name="p586172385912"></a><a name="p586172385912"></a>任务超时时间，即任务执行的最长时间。</p>
        <p id="p1686142375914"><a name="p1686142375914"></a><a name="p1686142375914"></a>支持设置0~300秒的超时时间，如果设置为0，则表示超时时间为默认值30秒。</p>
        </td>
        </tr>
        <tr id="row6908712115212"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p7908171215521"><a name="p7908171215521"></a><a name="p7908171215521"></a>动作提供方</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p886182315598"><a name="p886182315598"></a><a name="p886182315598"></a>函数模板的提供方。</p>
        </td>
        </tr>
        <tr id="row590810124526"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1590871265213"><a name="p1590871265213"></a><a name="p1590871265213"></a>错误处理</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p486132325915"><a name="p486132325915"></a><a name="p486132325915"></a>可定义不同类型错误发生时的重试次数、重试间隔，以及重试失败后跳转到的目标任务。</p>
        <p id="p68611223195915"><a name="p68611223195915"></a><a name="p68611223195915"></a>错误类型包括：匹配所有、执行失败、权限不合法、参数不合法、函数不存在、请求太频繁、函数不可用、函数异常</p>
        </td>
        </tr>
        <tr id="row29081125524"><td class="cellrowborder" rowspan="2" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p1590814123520"><a name="p1590814123520"></a><a name="p1590814123520"></a>动态参数</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p89081121528"><a name="p89081121528"></a><a name="p89081121528"></a>SMN topic唯一标识</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1790995353519"><a name="p1790995353519"></a><a name="p1790995353519"></a>选择已授权给OBS发布消息的SMN主题，以便向主题订阅者发送消息。SMN主题需通过SMN页面创建。</p>
        <p class="NotesTextinTable" id="p15314145320"><a name="p15314145320"></a><a name="p15314145320"></a>SMN服务的操作指导请参见《消息通知服务用户指南》中“<a href="https://support.huaweicloud.com/usermanual-smn/zh-cn_topic_0043961401.html" target="_blank" rel="noopener noreferrer">创建主题</a>”、“<a href="https://support.huaweicloud.com/usermanual-smn/zh-cn_topic_0043394891.html" target="_blank" rel="noopener noreferrer">设置主题策略</a>”和“<a href="https://support.huaweicloud.com/usermanual-smn/zh-cn_topic_0043961402.html" target="_blank" rel="noopener noreferrer">订阅主题</a>”章节的内容。</p>
        <div class="note" id="note21218627"><a name="note21218627"></a><a name="note21218627"></a><span class="notetitle"> 说明： </span><div class="notebody"><p class="NotesTextinTable" id="p18816234317"><a name="p18816234317"></a><a name="p18816234317"></a>SMN主题配置成功后，请不要随意删除与OBS Data+工作流相关联的主题，也不要取消主题对OBS的授权。若与OBS Data+工作流相关联的主题被删除或取消该主题对OBS的授权，可能会导致对应主题的订阅者无法收到消息。</p>
        </div></div>
        <p id="p131061323135217"><a name="p131061323135217"></a><a name="p131061323135217"></a>下拉列表中仅展示与Data+工作流同区域且同项目的SMN主题。工作流所属区域为创建工作流的桶所属区域。例如工作流A是在桶A中创建的，则桶A的区域即为工作流A的区域。</p>
        </td>
        </tr>
        <tr id="row8863213517"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p12861221165115"><a name="p12861221165115"></a><a name="p12861221165115"></a>SMN topic主题名称</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p35831063390"><a name="p35831063390"></a><a name="p35831063390"></a>发布消息的标题，给邮箱订阅者发送邮件时作为邮件主题。</p>
        </td>
        </tr>
        </tbody>
        </table>

    -   **事件延迟**

        模板作用：可用于控制工作流两个相邻任务间的等待时长，例如执行任务A后，规定等待一段时间再继续执行任务B。

        **表 5**  事件延迟属性配置说明

        <a name="table1333320163529"></a>
        <table><thead align="left"><tr id="row933312165522"><th class="cellrowborder" valign="top" width="15%" id="mcps1.2.4.1.1"><p id="p233316166522"><a name="p233316166522"></a><a name="p233316166522"></a>属性类别</p>
        </th>
        <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.2"><p id="p333316162521"><a name="p333316162521"></a><a name="p333316162521"></a>参数名称</p>
        </th>
        <th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p1733331617523"><a name="p1733331617523"></a><a name="p1733331617523"></a>参数说明</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row133332168528"><td class="cellrowborder" rowspan="2" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p19333916195210"><a name="p19333916195210"></a><a name="p19333916195210"></a>基本属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p433331685215"><a name="p433331685215"></a><a name="p433331685215"></a>名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1333171617521"><a name="p1333171617521"></a><a name="p1333171617521"></a>任务的名称，修改后将体现在工作流编排区域。</p>
        <a name="ul143501337172217"></a><a name="ul143501337172217"></a><ul id="ul143501337172217"><li>必须以字母或数字开头</li><li>只能由字母、数字、下划线和中划线组成</li><li>长度范围为1~20个字符</li><li>不能和同一工作流中的其他任务重名</li></ul>
        </td>
        </tr>
        <tr id="row1233341610526"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p33331166521"><a name="p33331166521"></a><a name="p33331166521"></a>超时(秒)</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p23331416195213"><a name="p23331416195213"></a><a name="p23331416195213"></a>执行下一任务前的等待时长，单位：秒。支持设置的范围为1~86400秒。</p>
        </td>
        </tr>
        </tbody>
        </table>

    -   **自定义**

        用户可自定义函数，满足不同场景的任务定制需求。

        **表 6**  自定义函数属性配置说明

        <a name="table619135816566"></a>
        <table><thead align="left"><tr id="row3191358105612"><th class="cellrowborder" valign="top" width="15%" id="mcps1.2.4.1.1"><p id="p141913585569"><a name="p141913585569"></a><a name="p141913585569"></a>属性类别</p>
        </th>
        <th class="cellrowborder" valign="top" width="25%" id="mcps1.2.4.1.2"><p id="p71918586561"><a name="p71918586561"></a><a name="p71918586561"></a>参数名称</p>
        </th>
        <th class="cellrowborder" valign="top" width="60%" id="mcps1.2.4.1.3"><p id="p11975845614"><a name="p11975845614"></a><a name="p11975845614"></a>参数说明</p>
        </th>
        </tr>
        </thead>
        <tbody><tr id="row131925817560"><td class="cellrowborder" rowspan="3" valign="top" width="15%" headers="mcps1.2.4.1.1 "><p id="p1219125875615"><a name="p1219125875615"></a><a name="p1219125875615"></a>基本属性</p>
        </td>
        <td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.4.1.2 "><p id="p16191458155620"><a name="p16191458155620"></a><a name="p16191458155620"></a>名称</p>
        </td>
        <td class="cellrowborder" valign="top" width="60%" headers="mcps1.2.4.1.3 "><p id="p1619115813567"><a name="p1619115813567"></a><a name="p1619115813567"></a>任务的名称，修改后将体现在工作流编排区域。</p>
        <a name="ul3191581569"></a><a name="ul3191581569"></a><ul id="ul3191581569"><li>必须以字母或数字开头</li><li>只能由字母、数字、下划线和中划线组成</li><li>长度范围为1~20个字符</li><li>不能和同一工作流中的其他任务重名</li></ul>
        </td>
        </tr>
        <tr id="row119115817568"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1319358145610"><a name="p1319358145610"></a><a name="p1319358145610"></a>超时(秒)</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p11192581564"><a name="p11192581564"></a><a name="p11192581564"></a>任务超时时间，即任务执行的最长时间。</p>
        <p id="p62015818562"><a name="p62015818562"></a><a name="p62015818562"></a>支持设置0~300秒的超时时间，如果设置为0，则表示超时时间为默认值30秒。</p>
        </td>
        </tr>
        <tr id="row1720185818565"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p820205825613"><a name="p820205825613"></a><a name="p820205825613"></a>函数唯一标识</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p4486144715585"><a name="p4486144715585"></a><a name="p4486144715585"></a>选择需要执行的FunctionGraph中的函数。函数需通过FunctionGraph页面创建。</p>
        <p id="p76951145832"><a name="p76951145832"></a><a name="p76951145832"></a>FunctionGraph服务的操作指导请参见《函数工作流用户指南》中“<a href="https://support.huaweicloud.com/usermanual-functiongraph/functiongraph_01_0201.html" target="_blank" rel="noopener noreferrer">创建并初始化函数</a>”章节的内容。</p>
        <p id="p15703115555918"><a name="p15703115555918"></a><a name="p15703115555918"></a>下拉列表中仅展示与Data+工作流同区域且同项目的函数。工作流所属区域为创建工作流的桶所属区域。例如工作流A是在桶A中创建的，则桶A的区域即为工作流A的区域。</p>
        </td>
        </tr>
        <tr id="row1620165813569"><td class="cellrowborder" colspan="2" valign="top" headers="mcps1.2.4.1.1 mcps1.2.4.1.2 "><p id="p1520158145612"><a name="p1520158145612"></a><a name="p1520158145612"></a>动态参数</p>
        </td>
        <td class="cellrowborder" valign="top" headers="mcps1.2.4.1.3 "><p id="p1822144455815"><a name="p1822144455815"></a><a name="p1822144455815"></a>若自定义函数中存在动态参数，可以指定动态参数的参数名和取值，作为函数的输入。</p>
        </td>
        </tr>
        </tbody>
        </table>

7.  鼠标单击各流程图标下方的小圆圈并长按拖拽，将工作流完整串联起来。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >当前仅支持串行工作流。

    **图 2**  串联后的完整工作流<a name="fig14971115015466"></a>  
    ![](figures/串联后的完整工作流.png "串联后的完整工作流")

8.  单击右上角的“保存”。
9.  在弹框中输入“工作流名称”并单击“确定”。

    创建完成的所有同区域工作流，都将在工作流列表展示。工作流创建完成后，还需要[创建事件触发器](#section187831529172915)，或通过API触发，工作流才能工作。


## 创建事件触发器<a name="section187831529172915"></a>

1.  在OBS管理控制台左侧导航栏选择“对象存储“。
2.  在桶列表单击待操作的桶，进入“概览”页面。
3.  在左侧导航栏选中“Data+”，进入“事件触发器”页面。
4.  单击列表左上方的“创建事件触发器”，弹出“创建事件触发器”对话框。

    也可以在工作流列表，单击待关联工作流操作列的“创建事件触发器”，此方式无法更改关联工作流。

    **图 3**  创建事件触发器<a name="fig1517412815174"></a>  
    ![](figures/创建事件触发器.png "创建事件触发器")

5.  配置事件触发器参数。

    **表 7**  事件触发器参数说明

    <a name="aobs_console_0039_mmccppss_table01"></a>
    <table><thead align="left"><tr id="row2055942"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.3.1.1"><p id="p32313598"><a name="p32313598"></a><a name="p32313598"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="75%" id="mcps1.2.3.1.2"><p id="p155758"><a name="p155758"></a><a name="p155758"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row12616447"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p15299288"><a name="p15299288"></a><a name="p15299288"></a>触发器名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p31282850"><a name="p31282850"></a><a name="p31282850"></a>事件触发器的名称，用户自定义。同一桶内的触发器名称不允许重复。</p>
    </td>
    </tr>
    <tr id="row1315520182228"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p19156141832219"><a name="p19156141832219"></a><a name="p19156141832219"></a>关联工作流</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p1339514261232"><a name="p1339514261232"></a><a name="p1339514261232"></a>满足该事件触发器条件时，自动执行的工作流。</p>
    <p id="p415651812212"><a name="p415651812212"></a><a name="p415651812212"></a>可选择已有工作流或创建新的工作流，一个事件触发器只能关联一个工作流。</p>
    </td>
    </tr>
    <tr id="row4138175316237"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p141381753122312"><a name="p141381753122312"></a><a name="p141381753122312"></a>事件源存储桶</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p15474041192614"><a name="p15474041192614"></a><a name="p15474041192614"></a>事件发生的源桶，即事件在该桶中发生时，触发关联工作流。</p>
    <p id="p1013805302313"><a name="p1013805302313"></a><a name="p1013805302313"></a>该参数不支持修改，默认为创建事件触发器的桶。</p>
    </td>
    </tr>
    <tr id="row13110201"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p55293359"><a name="p55293359"></a><a name="p55293359"></a>事件源类型</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p49577065"><a name="p49577065"></a><a name="p49577065"></a>使事件触发器生效的事件源类型。目前，OBS支持以下事件源类型：</p>
    <a name="ul43540403"></a><a name="ul43540403"></a><ul id="ul43540403"><li><strong id="b2253084295127"><a name="b2253084295127"></a><a name="b2253084295127"></a>ObjectCreated：</strong>表示所有创建对象的操作，包含Put、Post、Copy对象以及合并段。</li><li><strong id="b21739820154642"><a name="b21739820154642"></a><a name="b21739820154642"></a>Put</strong>：使用Put方法上传对象。</li><li><strong id="b7554011173727"><a name="b7554011173727"></a><a name="b7554011173727"></a>Post</strong>：使用Post方法上传对象。</li><li><strong id="b19295192"><a name="b19295192"></a><a name="b19295192"></a>Copy</strong>：使用copy方法复制对象。</li><li><strong id="b6205384517382"><a name="b6205384517382"></a><a name="b6205384517382"></a>CompleteMultipartUpload</strong>：表示合并分段任务。</li><li><strong id="b4214016595037"><a name="b4214016595037"></a><a name="b4214016595037"></a>ObjectRemoved：</strong>表示删除对象。</li><li><strong id="b28442244"><a name="b28442244"></a><a name="b28442244"></a>Delete</strong>：指定对象版本号删除对象。</li><li><strong id="b22120394"><a name="b22120394"></a><a name="b22120394"></a>DeleteMarkerCreated</strong>：不指定对象版本号删除对象。</li></ul>
    <p id="p64865822"><a name="p64865822"></a><a name="p64865822"></a>多个事件源类型可以作用于同一个目标对象，例如：同时选择“事件源类型”复选框中的<strong id="b46921489"><a name="b46921489"></a><a name="b46921489"></a>Put</strong>、<strong id="b19640220"><a name="b19640220"></a><a name="b19640220"></a>Copy</strong>、<strong id="b42544256"><a name="b42544256"></a><a name="b42544256"></a>Delete</strong>等方法作用于某目标对象，则用户往该桶中上传、复制、删除符合前后缀规则的目标对象时，均会使触发器生效。<strong id="b41674970143835"><a name="b41674970143835"></a><a name="b41674970143835"></a>ObjectCreated</strong>包含了<strong id="b15574064143840"><a name="b15574064143840"></a><a name="b15574064143840"></a>Put</strong>、<strong id="b62119592143845"><a name="b62119592143845"></a><a name="b62119592143845"></a>Post</strong>、<strong id="b7081676143849"><a name="b7081676143849"></a><a name="b7081676143849"></a>Copy</strong>和<strong id="b31607544151827"><a name="b31607544151827"></a><a name="b31607544151827"></a>CompleteMultipartUpload</strong>，如果选择了<strong id="b63678108143857"><a name="b63678108143857"></a><a name="b63678108143857"></a>ObjectCreated</strong>，则不能再选择<strong id="b39981405143910"><a name="b39981405143910"></a><a name="b39981405143910"></a>Put</strong>、<strong id="b17268397143910"><a name="b17268397143910"></a><a name="b17268397143910"></a>Post</strong>、<strong id="b56562934143910"><a name="b56562934143910"></a><a name="b56562934143910"></a>Copy</strong>或<strong id="b59319998143915"><a name="b59319998143915"></a><a name="b59319998143915"></a>CompleteMultipartUpload</strong>。同理如果选择了<strong id="b44527778143920"><a name="b44527778143920"></a><a name="b44527778143920"></a>ObjectRemoved</strong>，则不能再选择<strong id="b57045165143925"><a name="b57045165143925"></a><a name="b57045165143925"></a>Delete</strong>或<strong id="b40642771143930"><a name="b40642771143930"></a><a name="b40642771143930"></a>DeleteMarkerCreated</strong>。</p>
    </td>
    </tr>
    <tr id="row47353991"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p10468038"><a name="p10468038"></a><a name="p10468038"></a>前缀</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p42604738"><a name="p42604738"></a><a name="p42604738"></a>使事件触发器生效的对象前缀。</p>
    <div class="note" id="note13847653113412"><a name="note13847653113412"></a><a name="note13847653113412"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p138481553193416"><a name="p138481553193416"></a><a name="p138481553193416"></a>当前缀和后缀都不配置时，事件触发器将作用于桶中所有对象。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row16547757"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="p65299951"><a name="p65299951"></a><a name="p65299951"></a>后缀</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="p54804702"><a name="p54804702"></a><a name="p54804702"></a>使事件触发器生效的对象后缀。</p>
    <div class="note" id="note64263792115"><a name="note64263792115"></a><a name="note64263792115"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="ul75801343183518"></a><a name="ul75801343183518"></a><ul id="ul75801343183518"><li>文件夹是以“/”结尾的，“/”前的字符为文件夹名称。若要对文件夹进行后缀匹配，后缀必须以“/”结尾。</li><li>当前缀和后缀都不配置时，事件触发器将作用于桶中所有对象。</li></ul>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

6.  单击“确定”，完成事件触发器创建。

    当满足事件触发器规则的条件满足时，将自动执行关联工作流定义的任务。


## 相关操作<a name="section1877985716436"></a>

除了通过事件触发器触发工作流外，还可以通过API触发，实现单个对象粒度的复杂任务处理，可以指定某个对象立即执行某个特定的工作流。

