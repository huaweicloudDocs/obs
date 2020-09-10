# 查询Action模板详情<a name="obs_04_0133"></a>

## 功能介绍<a name="section75005621314"></a>

本接口用于按名称查询Action模板。

## 请求消息样式<a name="section6107610185512"></a>

```
GET /v2/actiontemplates/{template_name} HTTP/1.1
Host: obs.cn-north-1.myhuaweicloud.com 
Authorization: authorization
Content-Type: application/json
Content-Length: length
Date: date
```

## 请求消息参数<a name="section95731039205518"></a>

**表 1**  请求参数

<a name="table52631931376"></a>
<table><thead align="left"><tr id="row1726313312719"><th class="cellrowborder" valign="top" width="17.79%" id="mcps1.2.6.1.1"><p id="p162633318720"><a name="p162633318720"></a><a name="p162633318720"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="12.030000000000001%" id="mcps1.2.6.1.2"><p id="p226343111718"><a name="p226343111718"></a><a name="p226343111718"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="9.48%" id="mcps1.2.6.1.3"><p id="p32639311775"><a name="p32639311775"></a><a name="p32639311775"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="22.31%" id="mcps1.2.6.1.4"><p id="p202637311672"><a name="p202637311672"></a><a name="p202637311672"></a>说明</p>
</th>
<th class="cellrowborder" valign="top" width="38.39%" id="mcps1.2.6.1.5"><p id="p1626312311376"><a name="p1626312311376"></a><a name="p1626312311376"></a>约束</p>
</th>
</tr>
</thead>
<tbody><tr id="row142634311673"><td class="cellrowborder" valign="top" width="17.79%" headers="mcps1.2.6.1.1 "><p id="p7481165814816"><a name="p7481165814816"></a><a name="p7481165814816"></a>template_name</p>
</td>
<td class="cellrowborder" valign="top" width="12.030000000000001%" headers="mcps1.2.6.1.2 "><p id="p9482195819815"><a name="p9482195819815"></a><a name="p9482195819815"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="9.48%" headers="mcps1.2.6.1.3 "><p id="p1948295818810"><a name="p1948295818810"></a><a name="p1948295818810"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="22.31%" headers="mcps1.2.6.1.4 "><p id="p848212584817"><a name="p848212584817"></a><a name="p848212584817"></a>Action模板名称，默认内置的枚举值有：<a href="创建工作流.md#table11855202184517">内置Action模板名</a>。</p>
</td>
<td class="cellrowborder" valign="top" width="38.39%" headers="mcps1.2.6.1.5 "><p id="p154821858285"><a name="p154821858285"></a><a name="p154821858285"></a>名称必须以字母或数字开头，只能由字母、数字、下划线和中划线组成，长度小于等于64个字符。</p>
</td>
</tr>
</tbody>
</table>

## 请求消息头<a name="section742141334119"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section328020178411"></a>

该请求消息中不使用消息元素。

## 响应消息样式<a name="section1621418229411"></a>

```
HTTP/1.1 status_code 
Date: date 
Content-Length: length 
X-Request-ID: obs request id

json body
```

## 响应消息头<a name="section749314404574"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section1816644411576"></a>

**表 2**  响应消息元素

<a name="table7265171945817"></a>
<table><thead align="left"><tr id="row132651819155812"><th class="cellrowborder" valign="top" width="18.421842184218423%" id="mcps1.2.4.1.1"><p id="p192652019145812"><a name="p192652019145812"></a><a name="p192652019145812"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="20.49204920492049%" id="mcps1.2.4.1.2"><p id="p15265141955817"><a name="p15265141955817"></a><a name="p15265141955817"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="61.08610861086109%" id="mcps1.2.4.1.3"><p id="p9265111910585"><a name="p9265111910585"></a><a name="p9265111910585"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row12265131919582"><td class="cellrowborder" valign="top" width="18.421842184218423%" headers="mcps1.2.4.1.1 "><p id="p14265919105813"><a name="p14265919105813"></a><a name="p14265919105813"></a>provided_actions</p>
</td>
<td class="cellrowborder" valign="top" width="20.49204920492049%" headers="mcps1.2.4.1.2 "><p id="p162651619115817"><a name="p162651619115817"></a><a name="p162651619115817"></a>Array of <a href="#table6565174183715">ProvidedAction</a></p>
</td>
<td class="cellrowborder" valign="top" width="61.08610861086109%" headers="mcps1.2.4.1.3 "><p id="p7265111913588"><a name="p7265111913588"></a><a name="p7265111913588"></a>可选的Action列表。</p>
</td>
</tr>
</tbody>
</table>

**表 3**  ProvidedAction参数说明

<a name="table6565174183715"></a>
<table><thead align="left"><tr id="row8565641203714"><th class="cellrowborder" valign="top" width="23.89%" id="mcps1.2.5.1.1"><p id="p2565134118375"><a name="p2565134118375"></a><a name="p2565134118375"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="11.77%" id="mcps1.2.5.1.2"><p id="p12900175483013"><a name="p12900175483013"></a><a name="p12900175483013"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="18.310000000000002%" id="mcps1.2.5.1.3"><p id="p65661416370"><a name="p65661416370"></a><a name="p65661416370"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="46.03%" id="mcps1.2.5.1.4"><p id="p156616412371"><a name="p156616412371"></a><a name="p156616412371"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row519411587442"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p11182143183519"><a name="p11182143183519"></a><a name="p11182143183519"></a>name</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p921615392574"><a name="p921615392574"></a><a name="p921615392574"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p121821843193519"><a name="p121821843193519"></a><a name="p121821843193519"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p151825439358"><a name="p151825439358"></a><a name="p151825439358"></a>Action模板名称。</p>
</td>
</tr>
<tr id="row783216556447"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p5743185093512"><a name="p5743185093512"></a><a name="p5743185093512"></a>category</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p139001854113016"><a name="p139001854113016"></a><a name="p139001854113016"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p67431250173511"><a name="p67431250173511"></a><a name="p67431250173511"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p87432509353"><a name="p87432509353"></a><a name="p87432509353"></a>分类。</p>
</td>
</tr>
<tr id="row6584105112913"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p15852051182916"><a name="p15852051182916"></a><a name="p15852051182916"></a>create_time</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p0941141823418"><a name="p0941141823418"></a><a name="p0941141823418"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p3585155110294"><a name="p3585155110294"></a><a name="p3585155110294"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p165854513290"><a name="p165854513290"></a><a name="p165854513290"></a>创建时间。</p>
</td>
</tr>
<tr id="row9913121114554"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p16135929155516"><a name="p16135929155516"></a><a name="p16135929155516"></a>last_modify_time</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p2289420133412"><a name="p2289420133412"></a><a name="p2289420133412"></a>否</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p1391310116554"><a name="p1391310116554"></a><a name="p1391310116554"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p691331118556"><a name="p691331118556"></a><a name="p691331118556"></a>最近修改时间。</p>
</td>
</tr>
<tr id="row15757718123018"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p62531830203610"><a name="p62531830203610"></a><a name="p62531830203610"></a>function_template</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p74935415542"><a name="p74935415542"></a><a name="p74935415542"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p5402204541811"><a name="p5402204541811"></a><a name="p5402204541811"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p17253113013612"><a name="p17253113013612"></a><a name="p17253113013612"></a>函数的URN。</p>
</td>
</tr>
<tr id="row67301025151413"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p14230144414912"><a name="p14230144414912"></a><a name="p14230144414912"></a>inputs</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p1552682245617"><a name="p1552682245617"></a><a name="p1552682245617"></a>否</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p1022044741416"><a name="p1022044741416"></a><a name="p1022044741416"></a>Array of <a href="查询Action模板详情.md">Input</a></p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p2230644134918"><a name="p2230644134918"></a><a name="p2230644134918"></a>可修改参数定义列表。</p>
</td>
</tr>
<tr id="row19731857191115"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p77316576117"><a name="p77316576117"></a><a name="p77316576117"></a>dynamic_source_definition</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p19526122205613"><a name="p19526122205613"></a><a name="p19526122205613"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p1279317256459"><a name="p1279317256459"></a><a name="p1279317256459"></a>Map</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p4793182544516"><a name="p4793182544516"></a><a name="p4793182544516"></a>可修改参数引用。</p>
</td>
</tr>
<tr id="row19994259911"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p69910251494"><a name="p69910251494"></a><a name="p69910251494"></a>need_policy</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p116689294917"><a name="p116689294917"></a><a name="p116689294917"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p1766822911911"><a name="p1766822911911"></a><a name="p1766822911911"></a><a href="#table1771143675018">Policy</a></p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p1966892914910"><a name="p1966892914910"></a><a name="p1966892914910"></a>需要的权限。</p>
</td>
</tr>
<tr id="row1657145641613"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p16571756111617"><a name="p16571756111617"></a><a name="p16571756111617"></a>provider</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p11526122235612"><a name="p11526122235612"></a><a name="p11526122235612"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p11571756111613"><a name="p11571756111613"></a><a name="p11571756111613"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p185785614164"><a name="p185785614164"></a><a name="p185785614164"></a>提供方。</p>
</td>
</tr>
<tr id="row1052514196308"><td class="cellrowborder" valign="top" width="23.89%" headers="mcps1.2.5.1.1 "><p id="p1825315309364"><a name="p1825315309364"></a><a name="p1825315309364"></a>description</p>
</td>
<td class="cellrowborder" valign="top" width="11.77%" headers="mcps1.2.5.1.2 "><p id="p352612229566"><a name="p352612229566"></a><a name="p352612229566"></a>否</p>
</td>
<td class="cellrowborder" valign="top" width="18.310000000000002%" headers="mcps1.2.5.1.3 "><p id="p188955416189"><a name="p188955416189"></a><a name="p188955416189"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="46.03%" headers="mcps1.2.5.1.4 "><p id="p1625315307363"><a name="p1625315307363"></a><a name="p1625315307363"></a>描述。</p>
</td>
</tr>
</tbody>
</table>

**表 4**  Policy参数说明

<a name="table1771143675018"></a>
<table><thead align="left"><tr id="row6711236175020"><th class="cellrowborder" valign="top" width="22.662266226622663%" id="mcps1.2.4.1.1"><p id="p1711436145011"><a name="p1711436145011"></a><a name="p1711436145011"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="20.7020702070207%" id="mcps1.2.4.1.2"><p id="p57118361509"><a name="p57118361509"></a><a name="p57118361509"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="56.63566356635664%" id="mcps1.2.4.1.3"><p id="p17114363502"><a name="p17114363502"></a><a name="p17114363502"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row5711836165018"><td class="cellrowborder" valign="top" width="22.662266226622663%" headers="mcps1.2.4.1.1 "><p id="p1145315526500"><a name="p1145315526500"></a><a name="p1145315526500"></a>version</p>
</td>
<td class="cellrowborder" valign="top" width="20.7020702070207%" headers="mcps1.2.4.1.2 "><p id="p6453135220509"><a name="p6453135220509"></a><a name="p6453135220509"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="56.63566356635664%" headers="mcps1.2.4.1.3 "><p id="p1113951125019"><a name="p1113951125019"></a><a name="p1113951125019"></a>权限版本号。</p>
<a name="ul131391111507"></a><a name="ul131391111507"></a><ul id="ul131391111507"><li>1.0：系统预置的角色。以服务为粒度，提供有限的服务相关角色用于授权。</li><li>1.1：策略。IAM最新提供的一种细粒度授权的能力，可以精确到具体服务的操作、资源以及请求条件等。</li></ul>
</td>
</tr>
<tr id="row15711183615502"><td class="cellrowborder" valign="top" width="22.662266226622663%" headers="mcps1.2.4.1.1 "><p id="p1845317527503"><a name="p1845317527503"></a><a name="p1845317527503"></a>statement</p>
</td>
<td class="cellrowborder" valign="top" width="20.7020702070207%" headers="mcps1.2.4.1.2 "><p id="p1453452105013"><a name="p1453452105013"></a><a name="p1453452105013"></a>Array of <a href="#table1057217812488">Statement</a></p>
</td>
<td class="cellrowborder" valign="top" width="56.63566356635664%" headers="mcps1.2.4.1.3 "><p id="p9453552135011"><a name="p9453552135011"></a><a name="p9453552135011"></a><span>授权语句，描述权限的具体内容。</span></p>
</td>
</tr>
</tbody>
</table>

**表 5**  Statement参数说明

<a name="table1057217812488"></a>
<table><thead align="left"><tr id="row17572148104817"><th class="cellrowborder" valign="top" width="22.662266226622663%" id="mcps1.2.4.1.1"><p id="p457217814482"><a name="p457217814482"></a><a name="p457217814482"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="20.7020702070207%" id="mcps1.2.4.1.2"><p id="p9572118154820"><a name="p9572118154820"></a><a name="p9572118154820"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="56.63566356635664%" id="mcps1.2.4.1.3"><p id="p657238164815"><a name="p657238164815"></a><a name="p657238164815"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row105725810484"><td class="cellrowborder" valign="top" width="22.662266226622663%" headers="mcps1.2.4.1.1 "><p id="p115727894819"><a name="p115727894819"></a><a name="p115727894819"></a>action</p>
</td>
<td class="cellrowborder" valign="top" width="20.7020702070207%" headers="mcps1.2.4.1.2 "><p id="p157215874813"><a name="p157215874813"></a><a name="p157215874813"></a>Array String</p>
</td>
<td class="cellrowborder" valign="top" width="56.63566356635664%" headers="mcps1.2.4.1.3 "><p id="p17597162325014"><a name="p17597162325014"></a><a name="p17597162325014"></a>授权项。指对资源的具体操作权限，不超过100个。</p>
<a name="ul1259714239506"></a><a name="ul1259714239506"></a><ul id="ul1259714239506"><li>格式为：服务名:资源类型:操作，例：vpc:ports:create。</li><li>服务名为产品名称，例如ecs、evs和vpc等，服务名仅支持小写。 资源类型和操作没有大小写，要求支持通配符号*，无需罗列全部授权项。</li><li>当自定义策略为委托自定义策略时，该字段值为：<em id="i1259732313505"><a name="i1259732313505"></a><a name="i1259732313505"></a> "Action": ["iam:agencies:assume"]</em>。</li></ul>
</td>
</tr>
<tr id="row557217864813"><td class="cellrowborder" valign="top" width="22.662266226622663%" headers="mcps1.2.4.1.1 "><p id="p25729819486"><a name="p25729819486"></a><a name="p25729819486"></a>resource</p>
</td>
<td class="cellrowborder" valign="top" width="20.7020702070207%" headers="mcps1.2.4.1.2 "><p id="p457210820482"><a name="p457210820482"></a><a name="p457210820482"></a>Array String</p>
</td>
<td class="cellrowborder" valign="top" width="56.63566356635664%" headers="mcps1.2.4.1.3 "><p id="p14403573507"><a name="p14403573507"></a><a name="p14403573507"></a>资源。数组长度不超过10，每个字符串长度不超过128，规则如下：</p>
<a name="ul1540457155013"></a><a name="ul1540457155013"></a><ul id="ul1540457155013"><li>可填 * 的五段式：::::，例："obs:::bucket:*"。</li><li>region字段为*或用户可访问的region。service必须存在且resource属于对应service。</li><li>当该自定义策略为委托自定义策略时，该字段类型为Object，值为：<em id="i1040105710506"><a name="i1040105710506"></a><a name="i1040105710506"></a>"Resource": {"uri": ["/iam/agencies/07805acaba800fdd4fbdc00b8f888c7c"]}</em>。</li></ul>
</td>
</tr>
</tbody>
</table>

## 错误响应消息<a name="section1314918415580"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section25157713588"></a>

```
GET /v2/actiontemplates/{template_name} HTTP/1.1
Host: obs.cn-north-1.myhuaweicloud.com 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:sc2PM13Wlfcoc/YZLK0MwsI2Zpo=
Content-Type: application/json
Content-Length: 0
Date: Thu, 27 Aug 2020 12:38:10 GMT
```

## 响应示例<a name="section145191611316"></a>

```
HTTP/1.1 200 OK 
Date: Thu, 27 Aug 2020 12:38:10 GMT 
Content-Length: 0 
Content-Type: application/json
X-Request-ID: 6a63a18b8bab40ffb71ebd9cb80d0085
{
    "provided_actions": {
        "created_time": "<timestamp>",
        "last_modify_time": "<timestamp>",
        "name": "<template_name>",
        "category": "<category>",
        "provider_domainid": "<domainid>",
        "provider_userid": "<userid>",
        "provider_name": "<name>",
        "function_template": "urn:fss:cn-north-5:3f1e6caf808246c68457e660e4bfeb2f:function:default:test",
        "inputs": [{
            "parameter_name": "param1",
            "default": "TCP",
            "type": "string",
            "label": "action1",
            "constraints": {
                "valid_values": ["TCP", "UDP"]
            },
            "invisible": true,
            "description": "description param1"
        }],
        "dynamic_source_definition": {
            "param1": {
                "get_input": "$.inputs.param1"
            },
            "param2": {
                "get_input": "$.inputs.param2"
            }
        },
        "need_policy": {
            "version": "1.1",
            "statement": [{
                "action": [
                    "FunctionGraph:function:invokeAsync",
                    "FunctionGraph:function:invoke",
                    "FunctionGraph:function:updateCode",
                    "FunctionGraph:function:updateConfig",
                    "FunctionGraph:function:create",
                    "FunctionGraph:function:getConfig",
                    "FunctionGraph:function:getCode"
                ],
                "resource": ["FunctionGraph:*:*:function:*"]
            }, {
                "action": ["MPC:*:*:mpc:*"]
            }]
        },
        "description": ""
    }
}
```

