# HTTP状态码<a name="obs_21_2001"></a>

OBS服务端遵照HTTP规范，在接口调用完成均会返回标准的HTTP状态码，HTTP状态码分类以及OBS中常见的HTTP状态码如下：

-   HTTP状态码分类：

    <a name="table8158144411134"></a>
    <table><thead align="left"><tr id="row11159144414131"><th class="cellrowborder" valign="top" width="29.2%" id="mcps1.1.3.1.1"><p id="p131599441133"><a name="p131599441133"></a><a name="p131599441133"></a>分类</p>
    </th>
    <th class="cellrowborder" valign="top" width="70.8%" id="mcps1.1.3.1.2"><p id="p1615944461318"><a name="p1615944461318"></a><a name="p1615944461318"></a>分类描述</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row141591744171314"><td class="cellrowborder" valign="top" width="29.2%" headers="mcps1.1.3.1.1 "><p id="p41591844151315"><a name="p41591844151315"></a><a name="p41591844151315"></a>1XX</p>
    </td>
    <td class="cellrowborder" valign="top" width="70.8%" headers="mcps1.1.3.1.2 "><p id="p1715974411317"><a name="p1715974411317"></a><a name="p1715974411317"></a>信息，服务器收到请求，需要请求者继续执行操作，一般对客户调用函数不可见。</p>
    </td>
    </tr>
    <tr id="row151591544141319"><td class="cellrowborder" valign="top" width="29.2%" headers="mcps1.1.3.1.1 "><p id="p13159154410135"><a name="p13159154410135"></a><a name="p13159154410135"></a>2XX</p>
    </td>
    <td class="cellrowborder" valign="top" width="70.8%" headers="mcps1.1.3.1.2 "><p id="p181601244121314"><a name="p181601244121314"></a><a name="p181601244121314"></a>成功，操作被成功接收并处理。</p>
    </td>
    </tr>
    <tr id="row12160644171318"><td class="cellrowborder" valign="top" width="29.2%" headers="mcps1.1.3.1.1 "><p id="p616019446138"><a name="p616019446138"></a><a name="p616019446138"></a>3XX</p>
    </td>
    <td class="cellrowborder" valign="top" width="70.8%" headers="mcps1.1.3.1.2 "><p id="p1716094410132"><a name="p1716094410132"></a><a name="p1716094410132"></a>重定向，需要进一步的操作以完成请求，一般对客户调用函数不可见。</p>
    </td>
    </tr>
    <tr id="row145173214149"><td class="cellrowborder" valign="top" width="29.2%" headers="mcps1.1.3.1.1 "><p id="p851715215141"><a name="p851715215141"></a><a name="p851715215141"></a>4XX</p>
    </td>
    <td class="cellrowborder" valign="top" width="70.8%" headers="mcps1.1.3.1.2 "><p id="p45171021181413"><a name="p45171021181413"></a><a name="p45171021181413"></a>客户端错误，请求包含语法错误或无法完成请求。</p>
    </td>
    </tr>
    <tr id="row144972219148"><td class="cellrowborder" valign="top" width="29.2%" headers="mcps1.1.3.1.1 "><p id="p1844952216142"><a name="p1844952216142"></a><a name="p1844952216142"></a>5XX</p>
    </td>
    <td class="cellrowborder" valign="top" width="70.8%" headers="mcps1.1.3.1.2 "><p id="p8449172211146"><a name="p8449172211146"></a><a name="p8449172211146"></a>服务器错误，服务器在处理请求的过程中发生了错误</p>
    </td>
    </tr>
    </tbody>
    </table>

-   OBS中常见的HTTP状态码及其含义：

    <a name="table13232123612812"></a>
    <table><thead align="left"><tr id="row11233143662813"><th class="cellrowborder" valign="top" width="23.9023902390239%" id="mcps1.1.4.1.1"><p id="p122335364283"><a name="p122335364283"></a><a name="p122335364283"></a>HTTP状态码</p>
    </th>
    <th class="cellrowborder" valign="top" width="33.15331533153316%" id="mcps1.1.4.1.2"><p id="p83757322910"><a name="p83757322910"></a><a name="p83757322910"></a>描述</p>
    </th>
    <th class="cellrowborder" valign="top" width="42.94429442944294%" id="mcps1.1.4.1.3"><p id="p1123313613287"><a name="p1123313613287"></a><a name="p1123313613287"></a>常见原因</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row2233143662818"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p11233236122816"><a name="p11233236122816"></a><a name="p11233236122816"></a>400 Bad Request</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p19233193642818"><a name="p19233193642818"></a><a name="p19233193642818"></a>请求参数错误</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><a name="ul4569911163313"></a><a name="ul4569911163313"></a><ul id="ul4569911163313"><li>请求参数不合法；</li><li>客户端携带MD5请求后一致性校验失败；</li><li>无效的参数（使用SDK时传递了不合法的参数）；</li><li>无效的桶名（使用了不合法的桶名）；</li></ul>
    </td>
    </tr>
    <tr id="row182331436182816"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p19233103616280"><a name="p19233103616280"></a><a name="p19233103616280"></a>403 Forbidden</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p223373614283"><a name="p223373614283"></a><a name="p223373614283"></a>拒绝访问</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><a name="ul3752114484720"></a><a name="ul3752114484720"></a><ul id="ul3752114484720"><li>客户端请求中携带的签名和服务端计算出的签名不匹配（一般是AK/SK错误）；</li><li>权限不足（帐号对请求的资源无权限）；</li><li>帐号欠费；</li><li>桶的空间不足（出现在对桶设置了配额的场景）；</li><li>无效的AK；</li><li>客户端时间和服务端时间相差过大（客户端所在机器的时间与NTP服务不同步）；</li></ul>
    </td>
    </tr>
    <tr id="row112336361284"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p162331736142810"><a name="p162331736142810"></a><a name="p162331736142810"></a>404 Not Found</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p32331636152812"><a name="p32331636152812"></a><a name="p32331636152812"></a>请求的资源不存在</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><a name="ul8174554125217"></a><a name="ul8174554125217"></a><ul id="ul8174554125217"><li>桶不存在；</li><li>对象不存在；</li><li>桶的策略配置不存在（桶CORS配置不存在、桶Policy配置不存在等）；</li><li>分段上传任务不存在；</li></ul>
    </td>
    </tr>
    <tr id="row723353692819"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p172331936182810"><a name="p172331936182810"></a><a name="p172331936182810"></a>405 Method Not Allowed</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p1023343616289"><a name="p1023343616289"></a><a name="p1023343616289"></a>请求的方法不支持</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><p id="p1233153615287"><a name="p1233153615287"></a><a name="p1233153615287"></a>请求的方法/特性未在该桶所在的区域上线</p>
    </td>
    </tr>
    <tr id="row9233636132812"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p923418363284"><a name="p923418363284"></a><a name="p923418363284"></a>408 Request Timeout</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p14234836142820"><a name="p14234836142820"></a><a name="p14234836142820"></a>请求超时</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><p id="p62341136192812"><a name="p62341136192812"></a><a name="p62341136192812"></a>服务端与客户端Socket连接超时</p>
    </td>
    </tr>
    <tr id="row8234133620283"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p102341736152817"><a name="p102341736152817"></a><a name="p102341736152817"></a>409 Conflict</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p8234636172819"><a name="p8234636172819"></a><a name="p8234636172819"></a>请求冲突</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><a name="ul14894131205915"></a><a name="ul14894131205915"></a><ul id="ul14894131205915"><li>在不同区域重复创建同名桶；</li><li>尝试删除非空桶；</li></ul>
    </td>
    </tr>
    <tr id="row8234636192810"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p2023433617283"><a name="p2023433617283"></a><a name="p2023433617283"></a>500 Internal Server Error</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p18234163611286"><a name="p18234163611286"></a><a name="p18234163611286"></a>服务端内部错误</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><p id="p72341369285"><a name="p72341369285"></a><a name="p72341369285"></a>服务端内部错误</p>
    </td>
    </tr>
    <tr id="row1929189154414"><td class="cellrowborder" valign="top" width="23.9023902390239%" headers="mcps1.1.4.1.1 "><p id="p163099154420"><a name="p163099154420"></a><a name="p163099154420"></a>503 Service Unavaliable</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.15331533153316%" headers="mcps1.1.4.1.2 "><p id="p63012984420"><a name="p63012984420"></a><a name="p63012984420"></a>服务不可用</p>
    </td>
    <td class="cellrowborder" valign="top" width="42.94429442944294%" headers="mcps1.1.4.1.3 "><p id="p153199124412"><a name="p153199124412"></a><a name="p153199124412"></a>服务端暂时不可访问</p>
    </td>
    </tr>
    </tbody>
    </table>


