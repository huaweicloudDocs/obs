# REST API介绍<a name="ZH-CN_TOPIC_0136436606"></a>

公有云API符合RESTful API的设计理论。

REST从资源的角度来观察整个网络，提供创建、查询、更新、删掉等方法访问服务的资源。

REST API请求/响应对可以分为如下部分：

-   请求URI
-   请求方法
-   请求消息头
-   请求消息体
-   响应消息头
-   响应消息体

## 请求URI<a name="section1849899574"></a>

OBS根据桶和对象及带的资源参数来确定具体的URI，当需要进行资源操作时，可以使用这个URI地址。

URI的一般格式为（方括号内为可选项）：

**protocol ://hostname\[:port\] \[/bucket\] \[/object\] \[?param\]**

**表 1**  URI中的参数

<a name="table40449485"></a>
<table><thead align="left"><tr id="row6511324"><th class="cellrowborder" valign="top" width="13.13%" id="mcps1.2.4.1.1"><p id="p57655222"><a name="p57655222"></a><a name="p57655222"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="73.74000000000001%" id="mcps1.2.4.1.2"><p id="p39561425"><a name="p39561425"></a><a name="p39561425"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="13.13%" id="mcps1.2.4.1.3"><p id="p50358869"><a name="p50358869"></a><a name="p50358869"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row52536552"><td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.1 "><p id="p27602357"><a name="p27602357"></a><a name="p27602357"></a>protocol</p>
</td>
<td class="cellrowborder" valign="top" width="73.74000000000001%" headers="mcps1.2.4.1.2 "><p id="p21198434"><a name="p21198434"></a><a name="p21198434"></a>请求使用的协议类型，如HTTP、HTTPs。HTTPs表示通过安全的HTTPs访问该资源，对象存储服务支持HTTP，HTTPs两种传输协议。</p>
</td>
<td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.3 "><p id="p39351575"><a name="p39351575"></a><a name="p39351575"></a>必选</p>
</td>
</tr>
<tr id="row18619861"><td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.1 "><p id="p31813738"><a name="p31813738"></a><a name="p31813738"></a>hostname</p>
</td>
<td class="cellrowborder" valign="top" width="73.74000000000001%" headers="mcps1.2.4.1.2 "><p id="p26775963"><a name="p26775963"></a><a name="p26775963"></a>请求使用的主机名，是指存放资源的服务器的域名或IP地址。</p>
</td>
<td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.3 "><p id="p58107106"><a name="p58107106"></a><a name="p58107106"></a>必选</p>
</td>
</tr>
<tr id="row53201908"><td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.1 "><p id="p14387307"><a name="p14387307"></a><a name="p14387307"></a>port</p>
</td>
<td class="cellrowborder" valign="top" width="73.74000000000001%" headers="mcps1.2.4.1.2 "><p id="p24521247"><a name="p24521247"></a><a name="p24521247"></a>请求使用的端口号。根据软件服务器的部署不同而不</p>
<p id="p19364635"><a name="p19364635"></a><a name="p19364635"></a>同。缺省时使用默认端口，各种传输协议都有默认的端</p>
<p id="p40063991"><a name="p40063991"></a><a name="p40063991"></a>口号，如HTTP的默认端口为80，HTTPs的默认端口为443。</p>
<p id="p25031604"><a name="p25031604"></a><a name="p25031604"></a>OBS对象存储服务的http方式访问端口为80，HTTPs方式访问端口为443。</p>
</td>
<td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.3 "><p id="p14294078"><a name="p14294078"></a><a name="p14294078"></a>可选</p>
</td>
</tr>
<tr id="row61537845"><td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.1 "><p id="p18509547"><a name="p18509547"></a><a name="p18509547"></a>bucket</p>
</td>
<td class="cellrowborder" valign="top" width="73.74000000000001%" headers="mcps1.2.4.1.2 "><p id="p22878309"><a name="p22878309"></a><a name="p22878309"></a>请求使用的桶资源路径，在整个系统中唯一标识一个桶。</p>
</td>
<td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.3 "><p id="p41203723"><a name="p41203723"></a><a name="p41203723"></a>可选</p>
</td>
</tr>
<tr id="row35289195"><td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.1 "><p id="p39852543"><a name="p39852543"></a><a name="p39852543"></a>object</p>
</td>
<td class="cellrowborder" valign="top" width="73.74000000000001%" headers="mcps1.2.4.1.2 "><p id="p6830580"><a name="p6830580"></a><a name="p6830580"></a>请求使用的对象资源路径。</p>
</td>
<td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.3 "><p id="p16406130"><a name="p16406130"></a><a name="p16406130"></a>可选</p>
</td>
</tr>
<tr id="row13437443"><td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.1 "><p id="p14691104"><a name="p14691104"></a><a name="p14691104"></a>param</p>
</td>
<td class="cellrowborder" valign="top" width="73.74000000000001%" headers="mcps1.2.4.1.2 "><p id="p49128794"><a name="p49128794"></a><a name="p49128794"></a>请求使用的桶和对象的具体资源，缺省默认为请求桶或对象自身资源。</p>
</td>
<td class="cellrowborder" valign="top" width="13.13%" headers="mcps1.2.4.1.3 "><p id="p45866588"><a name="p45866588"></a><a name="p45866588"></a>可选</p>
</td>
</tr>
</tbody>
</table>

## 请求方法<a name="section580035055419"></a>

HTTP方法（也称为操作或动词），它告诉服务你正在请求什么类型的操作。

**表 2**  对象存储支持的REST请求方法

<a name="table1123134922518"></a>
<table><thead align="left"><tr id="row65706590"><th class="cellrowborder" valign="top" width="15.15%" id="mcps1.2.3.1.1"><p id="p20633546"><a name="p20633546"></a><a name="p20633546"></a>方法</p>
</th>
<th class="cellrowborder" valign="top" width="84.85000000000001%" id="mcps1.2.3.1.2"><p id="p60704555"><a name="p60704555"></a><a name="p60704555"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row18121961"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p58592747"><a name="p58592747"></a><a name="p58592747"></a>GET</p>
</td>
<td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p48392090"><a name="p48392090"></a><a name="p48392090"></a>请求服务器返回指定资源，如获取桶列表、下载对象等。</p>
</td>
</tr>
<tr id="row32875629"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p45680330"><a name="p45680330"></a><a name="p45680330"></a>PUT</p>
</td>
<td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p9119239"><a name="p9119239"></a><a name="p9119239"></a>请求服务器存储指定资源，如创建桶、上传对象等。</p>
</td>
</tr>
<tr id="row14964289"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p4147890"><a name="p4147890"></a><a name="p4147890"></a>POST</p>
</td>
<td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p434775"><a name="p434775"></a><a name="p434775"></a>请求服务器存储特殊的资源或执行特殊操作，如初始化上传段任务、合并段等。</p>
</td>
</tr>
<tr id="row35216792"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p33987935"><a name="p33987935"></a><a name="p33987935"></a>DELETE</p>
</td>
<td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p1559313"><a name="p1559313"></a><a name="p1559313"></a>请求服务器删除指定资源，如删除对象等。</p>
</td>
</tr>
<tr id="row14033823"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p62997855"><a name="p62997855"></a><a name="p62997855"></a>HEAD</p>
</td>
<td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p2552640"><a name="p2552640"></a><a name="p2552640"></a>请求服务器返回指定资源的概要，如获取对象元数据等。</p>
</td>
</tr>
<tr id="row22973764"><td class="cellrowborder" valign="top" width="15.15%" headers="mcps1.2.3.1.1 "><p id="p48935609"><a name="p48935609"></a><a name="p48935609"></a>OPTIONS</p>
</td>
<td class="cellrowborder" valign="top" width="84.85000000000001%" headers="mcps1.2.3.1.2 "><p id="p4361378"><a name="p4361378"></a><a name="p4361378"></a>请求服务器检查是否具有某个资源的操作权限，需要桶配置CORS。</p>
</td>
</tr>
</tbody>
</table>

## 请求消息头<a name="section1454211155819"></a>

可选的附加请求头字段，如指定的URI和HTTP方法所要求的字段。详细的公共请求消息头字段请参见[表3](#table25197309)。

**表 3**  公共请求消息头

<a name="table25197309"></a>
<table><thead align="left"><tr id="row56260471"><th class="cellrowborder" valign="top" width="20.380000000000003%" id="mcps1.2.4.1.1"><p id="p60804269"><a name="p60804269"></a><a name="p60804269"></a>消息头名称</p>
</th>
<th class="cellrowborder" valign="top" width="58.87%" id="mcps1.2.4.1.2"><p id="p26198756"><a name="p26198756"></a><a name="p26198756"></a>描述</p>
</th>
<th class="cellrowborder" valign="top" width="20.75%" id="mcps1.2.4.1.3"><p id="p41724483"><a name="p41724483"></a><a name="p41724483"></a>是否必选</p>
</th>
</tr>
</thead>
<tbody><tr id="row24239987"><td class="cellrowborder" valign="top" width="20.380000000000003%" headers="mcps1.2.4.1.1 "><p id="p17281948"><a name="p17281948"></a><a name="p17281948"></a>Authorization</p>
</td>
<td class="cellrowborder" valign="top" width="58.87%" headers="mcps1.2.4.1.2 "><p id="p57660517"><a name="p57660517"></a><a name="p57660517"></a>请求消息中可带的签名信息。</p>
<p id="p49182605"><a name="p49182605"></a><a name="p49182605"></a>类型：字符串。</p>
<p id="p39990262"><a name="p39990262"></a><a name="p39990262"></a>默认值：无。</p>
<p id="p24368041"><a name="p24368041"></a><a name="p24368041"></a>条件：匿名请求不需要带，其他请求必选。</p>
</td>
<td class="cellrowborder" valign="top" width="20.75%" headers="mcps1.2.4.1.3 "><p id="p27654330"><a name="p27654330"></a><a name="p27654330"></a>有条件必选</p>
</td>
</tr>
<tr id="row47562386"><td class="cellrowborder" valign="top" width="20.380000000000003%" headers="mcps1.2.4.1.1 "><p id="p27348077"><a name="p27348077"></a><a name="p27348077"></a>Content-Length</p>
</td>
<td class="cellrowborder" valign="top" width="58.87%" headers="mcps1.2.4.1.2 "><p id="p601777"><a name="p601777"></a><a name="p601777"></a>RFC 2616中定义的消息（不包含消息头）长度。</p>
<p id="p5415993"><a name="p5415993"></a><a name="p5415993"></a>类型：字符串。</p>
<p id="p48743940"><a name="p48743940"></a><a name="p48743940"></a>默认值：无。</p>
<p id="p36042284"><a name="p36042284"></a><a name="p36042284"></a>条件：PUT操作和加载XML的操作必须带。</p>
</td>
<td class="cellrowborder" valign="top" width="20.75%" headers="mcps1.2.4.1.3 "><p id="p33743900"><a name="p33743900"></a><a name="p33743900"></a>有条件必选</p>
</td>
</tr>
<tr id="row35259646"><td class="cellrowborder" valign="top" width="20.380000000000003%" headers="mcps1.2.4.1.1 "><p id="p37459059"><a name="p37459059"></a><a name="p37459059"></a>Content-Type</p>
</td>
<td class="cellrowborder" valign="top" width="58.87%" headers="mcps1.2.4.1.2 "><p id="p14284953"><a name="p14284953"></a><a name="p14284953"></a>资源内容的类型，例如： text/plain。</p>
<p id="p61455718"><a name="p61455718"></a><a name="p61455718"></a>类型：字符串。</p>
<p id="p16230551"><a name="p16230551"></a><a name="p16230551"></a>默认值：无。</p>
</td>
<td class="cellrowborder" valign="top" width="20.75%" headers="mcps1.2.4.1.3 "><p id="p39606294"><a name="p39606294"></a><a name="p39606294"></a>否</p>
</td>
</tr>
<tr id="row20912334"><td class="cellrowborder" valign="top" width="20.380000000000003%" headers="mcps1.2.4.1.1 "><p id="p16177456"><a name="p16177456"></a><a name="p16177456"></a>Date</p>
</td>
<td class="cellrowborder" valign="top" width="58.87%" headers="mcps1.2.4.1.2 "><p id="p35305575"><a name="p35305575"></a><a name="p35305575"></a>请求发起端的日期和时间。</p>
<p id="p49314726"><a name="p49314726"></a><a name="p49314726"></a>类型：字符串。</p>
<p id="p41179355"><a name="p41179355"></a><a name="p41179355"></a>默认值：无。</p>
<p id="p35069879"><a name="p35069879"></a><a name="p35069879"></a>条件：如果是匿名请求或者消息头中带了x-obs-date字段，则可以不带该字段，其他情况下必选。</p>
</td>
<td class="cellrowborder" valign="top" width="20.75%" headers="mcps1.2.4.1.3 "><p id="p22087952"><a name="p22087952"></a><a name="p22087952"></a>有条件必选</p>
</td>
</tr>
<tr id="row64573848"><td class="cellrowborder" valign="top" width="20.380000000000003%" headers="mcps1.2.4.1.1 "><p id="p63099185"><a name="p63099185"></a><a name="p63099185"></a>Host</p>
</td>
<td class="cellrowborder" valign="top" width="58.87%" headers="mcps1.2.4.1.2 "><p id="p10760359"><a name="p10760359"></a><a name="p10760359"></a>表明主机地址。如bucketname.obs.cn-north-1.myhuaweicloud.com。</p>
<p id="p29734368"><a name="p29734368"></a><a name="p29734368"></a>类型：字符串。</p>
<p id="p66282721"><a name="p66282721"></a><a name="p66282721"></a>默认值：无。</p>
</td>
<td class="cellrowborder" valign="top" width="20.75%" headers="mcps1.2.4.1.3 "><p id="p191303"><a name="p191303"></a><a name="p191303"></a>是</p>
</td>
</tr>
</tbody>
</table>

## 请求消息体（可选）<a name="section14612192315587"></a>

请求消息体通常以结构化格式（如JSON或XML）发出，与请求消息头中Content-type对应，传递除请求消息头之外的内容。

## 响应消息头<a name="section7804143005810"></a>

响应消息头包含如下两部分。

-   一个HTTP状态代码，从2xx成功代码到4xx或5xx错误代码。 或者，可以返回服务定义的状态码，如API文档中所示。
-   附加响应头字段，如支持请求的响应所需，如Content-type响应消息头。详细的公共响应消息头字段请参见[表4](#d0e686)。

    **表 4**  公共响应消息头

    <a name="d0e686"></a>
    <table><thead align="left"><tr id="row58885148"><th class="cellrowborder" valign="top" width="23%" id="mcps1.2.3.1.1"><p id="p4967702"><a name="p4967702"></a><a name="p4967702"></a>消息头名称</p>
    </th>
    <th class="cellrowborder" valign="top" width="77%" id="mcps1.2.3.1.2"><p id="p66839572"><a name="p66839572"></a><a name="p66839572"></a>描述</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row45296255"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p45118014"><a name="p45118014"></a><a name="p45118014"></a>Content-Length</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p30680506"><a name="p30680506"></a><a name="p30680506"></a>响应消息体的字节长度。</p>
    <p id="p7689098"><a name="p7689098"></a><a name="p7689098"></a>类型：字符串。</p>
    <p id="p2093018"><a name="p2093018"></a><a name="p2093018"></a>默认值：无。</p>
    </td>
    </tr>
    <tr id="row18837163"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p49415229"><a name="p49415229"></a><a name="p49415229"></a>Connection</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p43210599"><a name="p43210599"></a><a name="p43210599"></a>指明与服务器的连接是长连接还是短连接。</p>
    <p id="p53351077"><a name="p53351077"></a><a name="p53351077"></a>类型：字符串。</p>
    <p id="p10397650"><a name="p10397650"></a><a name="p10397650"></a>有效值：keep-alive | close。</p>
    <p id="p26469991"><a name="p26469991"></a><a name="p26469991"></a>默认值：无。</p>
    </td>
    </tr>
    <tr id="row36903334"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p36380041"><a name="p36380041"></a><a name="p36380041"></a>Date</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p61102246"><a name="p61102246"></a><a name="p61102246"></a>OBS系统响应的时间。</p>
    <p id="p13049305"><a name="p13049305"></a><a name="p13049305"></a>类型：字符串。</p>
    <p id="p50334883"><a name="p50334883"></a><a name="p50334883"></a>默认值：无。</p>
    </td>
    </tr>
    <tr id="row50360765"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p52690158"><a name="p52690158"></a><a name="p52690158"></a>ETag</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p40044371"><a name="p40044371"></a><a name="p40044371"></a>对象的base64编码的128位MD5摘要。ETag是对象内容的唯一标识，可以通过该值识别对象内容是否有变化。比如上传对象时ETag为A，下载对象时ETag为B，则说明对象内容发生了变化。</p>
    <p id="p24855020"><a name="p24855020"></a><a name="p24855020"></a>类型：字符串。</p>
    </td>
    </tr>
    <tr id="row22368596"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p67025883"><a name="p67025883"></a><a name="p67025883"></a>x-obs-id-2</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p60387405"><a name="p60387405"></a><a name="p60387405"></a>帮助定位问题的特殊符号。</p>
    <p id="p6615739"><a name="p6615739"></a><a name="p6615739"></a>类型：字符串。</p>
    <p id="p59541652"><a name="p59541652"></a><a name="p59541652"></a>默认值：无。</p>
    </td>
    </tr>
    <tr id="row66112827"><td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.3.1.1 "><p id="p53538780"><a name="p53538780"></a><a name="p53538780"></a>x-obs-request-id</p>
    </td>
    <td class="cellrowborder" valign="top" width="77%" headers="mcps1.2.3.1.2 "><p id="p41673925"><a name="p41673925"></a><a name="p41673925"></a>由OBS创建来唯一确定本次请求的值，可以通过该值来定位问题。</p>
    <p id="p39521013"><a name="p39521013"></a><a name="p39521013"></a>类型：字符串。</p>
    <p id="p20144799"><a name="p20144799"></a><a name="p20144799"></a>默认值：无。</p>
    </td>
    </tr>
    </tbody>
    </table>


## 响应消息体（可选）<a name="section034615592583"></a>

响应消息体通常以结构化格式（如JSON或XML）返回，与响应消息头中Content-type对应，传递除响应消息头之外的内容。

## 发起请求<a name="section140743661613"></a>

共有两种方式可以基于已构建好的请求消息发起请求，分别为：

-   cURL

    cURL是一个命令行工具，用来执行各种URL操作和信息传输。cURL充当的是HTTP客户端，可以发送HTTP请求给服务端，并接收响应消息。cURL适用于接口调试。关于cURL详细信息请参见[https://curl.haxx.se/](https://curl.haxx.se/)。由于cURL无法计算签名，使用cURL时仅支持访问匿名的公共OBS资源。

-   编码

    通过编码调用接口，组装请求消息，并发送处理请求消息。可以使用SDK或自行编码实现。


