# API异步启动工作流<a name="obs_04_0127"></a>

## 功能介绍<a name="section583694617498"></a>

本接口用于API方式异步启动已有工作流，产生工作流实例。

## 请求消息样式<a name="section88881434644"></a>

```
POST /v2/workflows/{graph_name} HTTP/1.1
Host: obs.cn-north-1.myhuaweicloud.com 
Authorization: authorization
Content-Type: application/json
Content-Length: length
Date: date

json body
```

## 请求消息参数<a name="section05361254193011"></a>

**表 1**  请求消息参数

<a name="table52631931376"></a>
<table><thead align="left"><tr id="row1726313312719"><th class="cellrowborder" valign="top" width="17.79%" id="mcps1.2.6.1.1"><p id="p162633318720"><a name="p162633318720"></a><a name="p162633318720"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="12.030000000000001%" id="mcps1.2.6.1.2"><p id="p226343111718"><a name="p226343111718"></a><a name="p226343111718"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="9.48%" id="mcps1.2.6.1.3"><p id="p32639311775"><a name="p32639311775"></a><a name="p32639311775"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="16.08%" id="mcps1.2.6.1.4"><p id="p202637311672"><a name="p202637311672"></a><a name="p202637311672"></a>说明</p>
</th>
<th class="cellrowborder" valign="top" width="44.62%" id="mcps1.2.6.1.5"><p id="p1626312311376"><a name="p1626312311376"></a><a name="p1626312311376"></a>约束</p>
</th>
</tr>
</thead>
<tbody><tr id="row142634311673"><td class="cellrowborder" valign="top" width="17.79%" headers="mcps1.2.6.1.1 "><p id="p7481165814816"><a name="p7481165814816"></a><a name="p7481165814816"></a>graph_name</p>
</td>
<td class="cellrowborder" valign="top" width="12.030000000000001%" headers="mcps1.2.6.1.2 "><p id="p9482195819815"><a name="p9482195819815"></a><a name="p9482195819815"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="9.48%" headers="mcps1.2.6.1.3 "><p id="p1948295818810"><a name="p1948295818810"></a><a name="p1948295818810"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="16.08%" headers="mcps1.2.6.1.4 "><p id="p848212584817"><a name="p848212584817"></a><a name="p848212584817"></a>工作流名称。</p>
</td>
<td class="cellrowborder" valign="top" width="44.62%" headers="mcps1.2.6.1.5 "><p id="p154821858285"><a name="p154821858285"></a><a name="p154821858285"></a>名称必须以字母或数字开头，只能由字母、数字、下划线和中划线组成，长度小于等于64个字符。</p>
</td>
</tr>
</tbody>
</table>

## 请求消息头<a name="section16227023104816"></a>

该请求使用公共消息头，具体参见[表3](构造请求.md#table25197309)。

## 请求消息元素<a name="section8568135410306"></a>

**表 2**  参数说明

<a name="table2701243910"></a>
<table><thead align="left"><tr id="row14704249915"><th class="cellrowborder" valign="top" width="12.55%" id="mcps1.2.6.1.1"><p id="p1652321831018"><a name="p1652321831018"></a><a name="p1652321831018"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="11.33%" id="mcps1.2.6.1.2"><p id="p1752301831015"><a name="p1752301831015"></a><a name="p1752301831015"></a>是否必选</p>
</th>
<th class="cellrowborder" valign="top" width="15.42%" id="mcps1.2.6.1.3"><p id="p752317185102"><a name="p752317185102"></a><a name="p752317185102"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="21.43%" id="mcps1.2.6.1.4"><p id="p18523101861019"><a name="p18523101861019"></a><a name="p18523101861019"></a>说明</p>
</th>
<th class="cellrowborder" valign="top" width="39.269999999999996%" id="mcps1.2.6.1.5"><p id="p125231418191017"><a name="p125231418191017"></a><a name="p125231418191017"></a>约束</p>
</th>
</tr>
</thead>
<tbody><tr id="row74541451944"><td class="cellrowborder" valign="top" width="12.55%" headers="mcps1.2.6.1.1 "><p id="p14454554414"><a name="p14454554414"></a><a name="p14454554414"></a>bucket</p>
</td>
<td class="cellrowborder" valign="top" width="11.33%" headers="mcps1.2.6.1.2 "><p id="p194543519410"><a name="p194543519410"></a><a name="p194543519410"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="15.42%" headers="mcps1.2.6.1.3 "><p id="p19454195247"><a name="p19454195247"></a><a name="p19454195247"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.6.1.4 "><p id="p1645465545"><a name="p1645465545"></a><a name="p1645465545"></a>桶名。</p>
</td>
<td class="cellrowborder" valign="top" width="39.269999999999996%" headers="mcps1.2.6.1.5 "><p id="p11454651743"><a name="p11454651743"></a><a name="p11454651743"></a>-</p>
</td>
</tr>
<tr id="row1250013814415"><td class="cellrowborder" valign="top" width="12.55%" headers="mcps1.2.6.1.1 "><p id="p450015818415"><a name="p450015818415"></a><a name="p450015818415"></a>object</p>
</td>
<td class="cellrowborder" valign="top" width="11.33%" headers="mcps1.2.6.1.2 "><p id="p19500208249"><a name="p19500208249"></a><a name="p19500208249"></a>是</p>
</td>
<td class="cellrowborder" valign="top" width="15.42%" headers="mcps1.2.6.1.3 "><p id="p85001813419"><a name="p85001813419"></a><a name="p85001813419"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.6.1.4 "><p id="p19500681848"><a name="p19500681848"></a><a name="p19500681848"></a>对象名。</p>
</td>
<td class="cellrowborder" valign="top" width="39.269999999999996%" headers="mcps1.2.6.1.5 "><p id="p1250048943"><a name="p1250048943"></a><a name="p1250048943"></a>-</p>
</td>
</tr>
<tr id="row5230844194917"><td class="cellrowborder" valign="top" width="12.55%" headers="mcps1.2.6.1.1 "><p id="p14230144414912"><a name="p14230144414912"></a><a name="p14230144414912"></a>inputs</p>
</td>
<td class="cellrowborder" valign="top" width="11.33%" headers="mcps1.2.6.1.2 "><p id="p923074410497"><a name="p923074410497"></a><a name="p923074410497"></a>否</p>
</td>
<td class="cellrowborder" valign="top" width="15.42%" headers="mcps1.2.6.1.3 "><p id="p52301244124910"><a name="p52301244124910"></a><a name="p52301244124910"></a>Json</p>
</td>
<td class="cellrowborder" valign="top" width="21.43%" headers="mcps1.2.6.1.4 "><p id="p2230644134918"><a name="p2230644134918"></a><a name="p2230644134918"></a>工作流中可修改参数列表。</p>
</td>
<td class="cellrowborder" valign="top" width="39.269999999999996%" headers="mcps1.2.6.1.5 "><p id="p192301244194920"><a name="p192301244194920"></a><a name="p192301244194920"></a>Map中的key必须是工作流中的parameter中的名字。</p>
</td>
</tr>
</tbody>
</table>

## 响应消息样式<a name="section122865113138"></a>

```
HTTP/1.1 status_code 
Date: date 
Content-Length: length 
X-Request-ID: obs request id

json body
```

## 响应消息头<a name="section19656537138"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

## 响应消息元素<a name="section28651738111419"></a>

**表 3**  响应元素

<a name="table18966545191311"></a>
<table><thead align="left"><tr id="row129661945131318"><th class="cellrowborder" valign="top" width="23.17231723172317%" id="mcps1.2.4.1.1"><p id="p4966174512133"><a name="p4966174512133"></a><a name="p4966174512133"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="26.542654265426545%" id="mcps1.2.4.1.2"><p id="p99679454137"><a name="p99679454137"></a><a name="p99679454137"></a>参数类型</p>
</th>
<th class="cellrowborder" valign="top" width="50.28502850285028%" id="mcps1.2.4.1.3"><p id="p199673450137"><a name="p199673450137"></a><a name="p199673450137"></a>说明</p>
</th>
</tr>
</thead>
<tbody><tr id="row92050370515"><td class="cellrowborder" valign="top" width="23.17231723172317%" headers="mcps1.2.4.1.1 "><p id="p19336154517147"><a name="p19336154517147"></a><a name="p19336154517147"></a>execution_urn</p>
</td>
<td class="cellrowborder" valign="top" width="26.542654265426545%" headers="mcps1.2.4.1.2 "><p id="p16336045121414"><a name="p16336045121414"></a><a name="p16336045121414"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="50.28502850285028%" headers="mcps1.2.4.1.3 "><p id="p4336144581414"><a name="p4336144581414"></a><a name="p4336144581414"></a>运行实例的URN。</p>
</td>
</tr>
<tr id="row39671445121316"><td class="cellrowborder" valign="top" width="23.17231723172317%" headers="mcps1.2.4.1.1 "><p id="p14336545111412"><a name="p14336545111412"></a><a name="p14336545111412"></a>started_at</p>
</td>
<td class="cellrowborder" valign="top" width="26.542654265426545%" headers="mcps1.2.4.1.2 "><p id="p233634551414"><a name="p233634551414"></a><a name="p233634551414"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="50.28502850285028%" headers="mcps1.2.4.1.3 "><p id="p1333634581420"><a name="p1333634581420"></a><a name="p1333634581420"></a>运行实例启动时间。</p>
</td>
</tr>
<tr id="row1896712457134"><td class="cellrowborder" valign="top" width="23.17231723172317%" headers="mcps1.2.4.1.1 "><p id="p5336124519141"><a name="p5336124519141"></a><a name="p5336124519141"></a>execution_name</p>
</td>
<td class="cellrowborder" valign="top" width="26.542654265426545%" headers="mcps1.2.4.1.2 "><p id="p133614511145"><a name="p133614511145"></a><a name="p133614511145"></a>String</p>
</td>
<td class="cellrowborder" valign="top" width="50.28502850285028%" headers="mcps1.2.4.1.3 "><p id="p193369451145"><a name="p193369451145"></a><a name="p193369451145"></a>运行实例的名字。</p>
</td>
</tr>
</tbody>
</table>

## 错误响应消息<a name="section53511050131419"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例<a name="section20731125951417"></a>

```
POST /v2/workflows/{graph_name} HTTP/1.1
Host: obs.cn-north-1.myhuaweicloud.com 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:sc2PM13Wlfcoc/YZLK0MwsI2Zpo=
Content-Type: application/json
Content-Length: 100
Date: Thu, 27 Aug 2020 12:38:10 GMT

{
    "bucket": "demo-bucket",
    "object": "/mpc/demo.mp4",
    "inputs": {
        "<parameter-name>": <parameter-value>
    }
}
```

## 响应示例<a name="section76081155815"></a>

```
HTTP/1.1 200 OK 
Date: Thu, 27 Aug 2020 12:38:10 GMT 
Content-Length: 100 
X-Request-ID: 000001742FE8FB3CCA20173B00807C43

{
    "execution_urn": "urn:fgs:<region_id>:<project_id>:execution:<graph_name>:<execution_name>:<domain_id>",
    "execution_name": "<execution_name>",
    "started_at": "2020-04-23T13:37:43.847Z"
}
```

