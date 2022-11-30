# OBS服务端错误码<a name="obs_21_2002"></a>

在向OBS服务端发出请求后，如果遇到错误，会在响应中包含响应的错误码描述错误信息。详细的错误码及其对应的描述和HTTP状态码见下表：

<a name="table85188111399"></a>
<table><thead align="left"><tr id="row12519816390"><th class="cellrowborder" valign="top" width="25%" id="mcps1.1.5.1.1"><p id="p16519141133917"><a name="p16519141133917"></a><a name="p16519141133917"></a>HTTP状态码</p>
</th>
<th class="cellrowborder" valign="top" width="25%" id="mcps1.1.5.1.2"><p id="p45195193914"><a name="p45195193914"></a><a name="p45195193914"></a>错误码</p>
</th>
<th class="cellrowborder" valign="top" width="25%" id="mcps1.1.5.1.3"><p id="p175191183915"><a name="p175191183915"></a><a name="p175191183915"></a>错误信息</p>
</th>
<th class="cellrowborder" valign="top" width="25%" id="mcps1.1.5.1.4"><p id="p16519815398"><a name="p16519815398"></a><a name="p16519815398"></a>处理措施</p>
</th>
</tr>
</thead>
<tbody><tr id="row145191017396"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p914111142436"><a name="p914111142436"></a><a name="p914111142436"></a>301 Moved Permanently</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p4141114174314"><a name="p4141114174314"></a><a name="p4141114174314"></a>PermanentRedirect</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p514113144439"><a name="p514113144439"></a><a name="p514113144439"></a>尝试访问的桶必须使用指定的地址，请将以后的请求发送到这个地址。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p16141191424313"><a name="p16141191424313"></a><a name="p16141191424313"></a>按照返回的重定向地址发送请求。</p>
</td>
</tr>
<tr id="row1653951624310"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p543573119435"><a name="p543573119435"></a><a name="p543573119435"></a>301 Moved Permanently</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p943513317437"><a name="p943513317437"></a><a name="p943513317437"></a>WebsiteRedirect</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p154351131104315"><a name="p154351131104315"></a><a name="p154351131104315"></a>Website请求缺少bucketName。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p8435153118434"><a name="p8435153118434"></a><a name="p8435153118434"></a>携带桶名后重试。</p>
</td>
</tr>
<tr id="row18643151844319"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p184355317437"><a name="p184355317437"></a><a name="p184355317437"></a>307 Moved Temporarily</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p9436103119437"><a name="p9436103119437"></a><a name="p9436103119437"></a>TemporaryRedirect</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1043653134319"><a name="p1043653134319"></a><a name="p1043653134319"></a>临时重定向，当DNS更新时，请求将被重定向到桶。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p0436163119437"><a name="p0436163119437"></a><a name="p0436163119437"></a>会自动重定向，也可以将请求发送到重定向地址。</p>
</td>
</tr>
<tr id="row186271119164313"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p103616430438"><a name="p103616430438"></a><a name="p103616430438"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p103610431431"><a name="p103610431431"></a><a name="p103610431431"></a>BadDigest</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p536154344319"><a name="p536154344319"></a><a name="p536154344319"></a>客户端指定的对象内容的MD5值与系统接收到的内容MD5值不一致。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1436843154314"><a name="p1436843154314"></a><a name="p1436843154314"></a>检查头域中携带的MD5与消息体计算出来的MD5是否一致。</p>
</td>
</tr>
<tr id="row167313208431"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1336184312438"><a name="p1336184312438"></a><a name="p1336184312438"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p236643114318"><a name="p236643114318"></a><a name="p236643114318"></a>BadDomainName</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p43624312432"><a name="p43624312432"></a><a name="p43624312432"></a>域名不合法。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p17361843164313"><a name="p17361843164313"></a><a name="p17361843164313"></a>使用合法的域名。</p>
</td>
</tr>
<tr id="row1653719212432"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p8360435430"><a name="p8360435430"></a><a name="p8360435430"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p9361843194318"><a name="p9361843194318"></a><a name="p9361843194318"></a>BadRequest</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p203644320438"><a name="p203644320438"></a><a name="p203644320438"></a>请求参数不合法。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p03684317439"><a name="p03684317439"></a><a name="p03684317439"></a>根据返回的错误消息体提示进行修改。</p>
</td>
</tr>
<tr id="row5307132284317"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p123684320430"><a name="p123684320430"></a><a name="p123684320430"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p6361243184318"><a name="p6361243184318"></a><a name="p6361243184318"></a>CustomDomainAreadyExist</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p11361743104314"><a name="p11361743104314"></a><a name="p11361743104314"></a>配置了已存在的域。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1436154314320"><a name="p1436154314320"></a><a name="p1436154314320"></a>已经配置过了，不需要再配置。</p>
</td>
</tr>
<tr id="row14917236433"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p336184319438"><a name="p336184319438"></a><a name="p336184319438"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p163694311437"><a name="p163694311437"></a><a name="p163694311437"></a>CustomDomainNotExist</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1836143204318"><a name="p1836143204318"></a><a name="p1836143204318"></a>删除不存在的域。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p153714432434"><a name="p153714432434"></a><a name="p153714432434"></a>未配置或已经删除，无需删除。</p>
</td>
</tr>
<tr id="row1249114404311"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p14167161384413"><a name="p14167161384413"></a><a name="p14167161384413"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p4167413154418"><a name="p4167413154418"></a><a name="p4167413154418"></a>EntityTooLarge</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p101671013124411"><a name="p101671013124411"></a><a name="p101671013124411"></a>用户POST上传的对象大小超过了条件允许的最大大小。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1316731324411"><a name="p1316731324411"></a><a name="p1316731324411"></a>修改POST上传的policy中的条件或者减少对象大小。</p>
</td>
</tr>
<tr id="row17943572444"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p191681113194419"><a name="p191681113194419"></a><a name="p191681113194419"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1716851315446"><a name="p1716851315446"></a><a name="p1716851315446"></a>EntityTooSmall</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p916815137441"><a name="p916815137441"></a><a name="p916815137441"></a>用户POST上传的对象大小小于条件允许的最小大小。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p116871324416"><a name="p116871324416"></a><a name="p116871324416"></a>修改POST上传的policy中的条件或者增加对象大小。</p>
</td>
</tr>
<tr id="row6116119114410"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p15168151354412"><a name="p15168151354412"></a><a name="p15168151354412"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p121681713114419"><a name="p121681713114419"></a><a name="p121681713114419"></a>IllegalLocationConstraintException</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p101681113124415"><a name="p101681113124415"></a><a name="p101681113124415"></a>用户未带Location在非默认Region创桶。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p016821314419"><a name="p016821314419"></a><a name="p016821314419"></a>请求发往默认Region创桶或带非默认Region的Location创桶。</p>
</td>
</tr>
<tr id="row119421995443"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p316817135447"><a name="p316817135447"></a><a name="p316817135447"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1916821324412"><a name="p1916821324412"></a><a name="p1916821324412"></a>IncompleteBody</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p11168191314448"><a name="p11168191314448"></a><a name="p11168191314448"></a>由于网络原因或其他问题导致请求体未接受完整。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p41687134446"><a name="p41687134446"></a><a name="p41687134446"></a>重新上传对象。</p>
</td>
</tr>
<tr id="row10631171013442"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p141681813144410"><a name="p141681813144410"></a><a name="p141681813144410"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p416861316448"><a name="p416861316448"></a><a name="p416861316448"></a>IncorrectNumberOfFilesInPost Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p15168213114415"><a name="p15168213114415"></a><a name="p15168213114415"></a>每个POST请求都需要带一个上传的文件。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p01681713144415"><a name="p01681713144415"></a><a name="p01681713144415"></a>带上一个上传文件。</p>
</td>
</tr>
<tr id="row263171524419"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1466732904416"><a name="p1466732904416"></a><a name="p1466732904416"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p106671029134420"><a name="p106671029134420"></a><a name="p106671029134420"></a>InvalidArgument</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p26671293449"><a name="p26671293449"></a><a name="p26671293449"></a>无效的参数。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1266752916442"><a name="p1266752916442"></a><a name="p1266752916442"></a>根据返回的错误消息体提示进行修改。</p>
</td>
</tr>
<tr id="row209318248440"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1466752964417"><a name="p1466752964417"></a><a name="p1466752964417"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p166672295449"><a name="p166672295449"></a><a name="p166672295449"></a>InvalidBucket</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p206671529114413"><a name="p206671529114413"></a><a name="p206671529114413"></a>请求访问的桶已不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p76679298440"><a name="p76679298440"></a><a name="p76679298440"></a>更换桶名。</p>
</td>
</tr>
<tr id="row1367362564415"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p66681629174412"><a name="p66681629174412"></a><a name="p66681629174412"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p17668729184414"><a name="p17668729184414"></a><a name="p17668729184414"></a>InvalidBucketName</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p10668829104411"><a name="p10668829104411"></a><a name="p10668829104411"></a>请求中指定的桶名无效，超长或带不允许的特殊字符。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p566822984415"><a name="p566822984415"></a><a name="p566822984415"></a>更换桶名。</p>
</td>
</tr>
<tr id="row18363162620443"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p2668182954417"><a name="p2668182954417"></a><a name="p2668182954417"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1668162914448"><a name="p1668162914448"></a><a name="p1668162914448"></a>InvalidEncryptionAlgorithmError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p66682294440"><a name="p66682294440"></a><a name="p66682294440"></a>错误的加密算法。下载SSE-C加密的对象，携带的加密头域错误，导致不能解密。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p26685297449"><a name="p26685297449"></a><a name="p26685297449"></a>携带正确的加密头域下载对象。</p>
</td>
</tr>
<tr id="row1871172774410"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p26681429144418"><a name="p26681429144418"></a><a name="p26681429144418"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p966816296448"><a name="p966816296448"></a><a name="p966816296448"></a>InvalidLocationConstraint</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p9668829194412"><a name="p9668829194412"></a><a name="p9668829194412"></a>创建桶时，指定的Location不合法或不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p12668112915449"><a name="p12668112915449"></a><a name="p12668112915449"></a>指定正确的Location创桶。</p>
</td>
</tr>
<tr id="row7331173314441"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1643544513440"><a name="p1643544513440"></a><a name="p1643544513440"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1943514516443"><a name="p1943514516443"></a><a name="p1943514516443"></a>InvalidPart</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1043511458444"><a name="p1043511458444"></a><a name="p1043511458444"></a>一个或多个指定的段无法找到。这些段可能没有上传，或者指定的entity tag与段的entity tag不一致。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p134351645114413"><a name="p134351645114413"></a><a name="p134351645114413"></a>按照正确的段和entity tag合并段。</p>
</td>
</tr>
<tr id="row532019357443"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p243564524410"><a name="p243564524410"></a><a name="p243564524410"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p74351945124419"><a name="p74351945124419"></a><a name="p74351945124419"></a>InvalidPartOrder</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p643517457446"><a name="p643517457446"></a><a name="p643517457446"></a>段列表的顺序不是升序，段列表必须按段号升序排列。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p643520459441"><a name="p643520459441"></a><a name="p643520459441"></a>按段号升序排列后重新合并。</p>
</td>
</tr>
<tr id="row18115193644413"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1843514514445"><a name="p1843514514445"></a><a name="p1843514514445"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p543519457446"><a name="p543519457446"></a><a name="p543519457446"></a>InvalidPolicyDocument</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1443510457443"><a name="p1443510457443"></a><a name="p1443510457443"></a>表单中的内容与策略文档中指定的条件不一致。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p7435104520446"><a name="p7435104520446"></a><a name="p7435104520446"></a>根据返回的错误消息体提示修改构造表单的policy重试。</p>
</td>
</tr>
<tr id="row7765136194411"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p11435845184411"><a name="p11435845184411"></a><a name="p11435845184411"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1943544516447"><a name="p1943544516447"></a><a name="p1943544516447"></a>InvalidRedirectLocation</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p16435445194417"><a name="p16435445194417"></a><a name="p16435445194417"></a>无效的重定向地址。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p114351345144410"><a name="p114351345144410"></a><a name="p114351345144410"></a>指定正确的地址。</p>
</td>
</tr>
<tr id="row194261372448"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p12435145124412"><a name="p12435145124412"></a><a name="p12435145124412"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1843554513442"><a name="p1843554513442"></a><a name="p1843554513442"></a>InvalidRequest</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p543504534410"><a name="p543504534410"></a><a name="p543504534410"></a>无效请求。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p20435134519444"><a name="p20435134519444"></a><a name="p20435134519444"></a>根据返回的错误消息体提示进行修改。</p>
</td>
</tr>
<tr id="row162121647104418"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p12801234459"><a name="p12801234459"></a><a name="p12801234459"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1928083204513"><a name="p1928083204513"></a><a name="p1928083204513"></a>InvalidRequestBody</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p828073204519"><a name="p828073204519"></a><a name="p828073204519"></a>请求体无效，需要消息体的请求没有上传消息体。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p62804313458"><a name="p62804313458"></a><a name="p62804313458"></a>按照正确的格式上传消息体。</p>
</td>
</tr>
<tr id="row299611478443"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p628023114510"><a name="p628023114510"></a><a name="p628023114510"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p172802374513"><a name="p172802374513"></a><a name="p172802374513"></a>InvalidTargetBucketForLogging</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1828018315458"><a name="p1828018315458"></a><a name="p1828018315458"></a>delivery group对目标桶无ACL权限。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p92800314516"><a name="p92800314516"></a><a name="p92800314516"></a>对目标桶配置ACL权限后重试。</p>
</td>
</tr>
<tr id="row149352048184410"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p172808315457"><a name="p172808315457"></a><a name="p172808315457"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p17280193144519"><a name="p17280193144519"></a><a name="p17280193144519"></a>KeyTooLongError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p162806334518"><a name="p162806334518"></a><a name="p162806334518"></a>提供的Key过长。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p828023164510"><a name="p828023164510"></a><a name="p828023164510"></a>使用较短的Key。</p>
</td>
</tr>
<tr id="row145752495441"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1228073164510"><a name="p1228073164510"></a><a name="p1228073164510"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p182819354511"><a name="p182819354511"></a><a name="p182819354511"></a>KMS.DisabledException</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p14281183164514"><a name="p14281183164514"></a><a name="p14281183164514"></a>SSE-KMS加密方式下，主密钥被禁用。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p82811932452"><a name="p82811932452"></a><a name="p82811932452"></a>更换密钥后重试，或联系技术支持。</p>
</td>
</tr>
<tr id="row43131250124411"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p42817318450"><a name="p42817318450"></a><a name="p42817318450"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p142810344518"><a name="p142810344518"></a><a name="p142810344518"></a>KMS.NotFoundException</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p42818311452"><a name="p42818311452"></a><a name="p42818311452"></a>SSE-KMS加密方式下，主密钥不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p32813354511"><a name="p32813354511"></a><a name="p32813354511"></a>携带正确的主密钥重试。</p>
</td>
</tr>
<tr id="row1488611152450"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p580721114511"><a name="p580721114511"></a><a name="p580721114511"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p128062113454"><a name="p128062113454"></a><a name="p128062113454"></a>MalformedACLError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p9806213451"><a name="p9806213451"></a><a name="p9806213451"></a>提供的XML格式错误，或者不符合我们要求的格式。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p28002115450"><a name="p28002115450"></a><a name="p28002115450"></a>使用正确的XML格式重试。</p>
</td>
</tr>
<tr id="row2720816164512"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p780122124510"><a name="p780122124510"></a><a name="p780122124510"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p18809211450"><a name="p18809211450"></a><a name="p18809211450"></a>MalformedError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1380121164518"><a name="p1380121164518"></a><a name="p1380121164518"></a>请求中携带的XML格式不正确。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p88015218451"><a name="p88015218451"></a><a name="p88015218451"></a>使用正确的XML格式重试。</p>
</td>
</tr>
<tr id="row1937111764515"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1280521184518"><a name="p1280521184518"></a><a name="p1280521184518"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1980112164511"><a name="p1980112164511"></a><a name="p1980112164511"></a>MalformedLoggingStatus</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p380421164519"><a name="p380421164519"></a><a name="p380421164519"></a>Logging的XML格式不正确。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p18018216450"><a name="p18018216450"></a><a name="p18018216450"></a>使用正确的XML格式重试。</p>
</td>
</tr>
<tr id="row1228641812458"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p14801721144513"><a name="p14801721144513"></a><a name="p14801721144513"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p880152174517"><a name="p880152174517"></a><a name="p880152174517"></a>MalformedPolicy</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1780122174519"><a name="p1780122174519"></a><a name="p1780122174519"></a>Bucket policy检查不通过。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p781162184517"><a name="p781162184517"></a><a name="p781162184517"></a>根据返回的错误消息体提示结合桶policy的要求进行修改。</p>
</td>
</tr>
<tr id="row149868187454"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p178110216453"><a name="p178110216453"></a><a name="p178110216453"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p68192164517"><a name="p68192164517"></a><a name="p68192164517"></a>MalformedQuotaError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p08142117451"><a name="p08142117451"></a><a name="p08142117451"></a>Quota的XML格式不正确。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p148122120453"><a name="p148122120453"></a><a name="p148122120453"></a>使用正确的XML格式重试。</p>
</td>
</tr>
<tr id="row122872256455"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p6489183864519"><a name="p6489183864519"></a><a name="p6489183864519"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1490238164517"><a name="p1490238164517"></a><a name="p1490238164517"></a>MalformedXML</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1349003810452"><a name="p1349003810452"></a><a name="p1349003810452"></a>当用户发送了一个配置项的错误格式的XML会出现这样的错误。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p14490138144518"><a name="p14490138144518"></a><a name="p14490138144518"></a>使用正确的XML格式重试。</p>
</td>
</tr>
<tr id="row2377123411451"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p4490153817450"><a name="p4490153817450"></a><a name="p4490153817450"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1749053815459"><a name="p1749053815459"></a><a name="p1749053815459"></a>MaxMessageLengthExceeded</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p5490203884514"><a name="p5490203884514"></a><a name="p5490203884514"></a>拷贝对象，带请求消息体。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p15490173811453"><a name="p15490173811453"></a><a name="p15490173811453"></a>拷贝对象不带消息体重试。</p>
</td>
</tr>
<tr id="row331133584519"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p5490738194510"><a name="p5490738194510"></a><a name="p5490738194510"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p19490153874520"><a name="p19490153874520"></a><a name="p19490153874520"></a>MetadataTooLarge</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1349012385456"><a name="p1349012385456"></a><a name="p1349012385456"></a>元数据消息头超过了允许的最大元数据大小。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p5490153813456"><a name="p5490153813456"></a><a name="p5490153813456"></a>减少元数据消息头。</p>
</td>
</tr>
<tr id="row374120357458"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p14490113810458"><a name="p14490113810458"></a><a name="p14490113810458"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1149011389450"><a name="p1149011389450"></a><a name="p1149011389450"></a>MissingRegion</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p134901738124515"><a name="p134901738124515"></a><a name="p134901738124515"></a>请求中缺少Region信息，且系统无默认Region。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p6490173819457"><a name="p6490173819457"></a><a name="p6490173819457"></a>请求中携带Region信息。</p>
</td>
</tr>
<tr id="row7413183674516"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p5491838144519"><a name="p5491838144519"></a><a name="p5491838144519"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p5491738154517"><a name="p5491738154517"></a><a name="p5491738154517"></a>MissingRequestBodyError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p134911386450"><a name="p134911386450"></a><a name="p134911386450"></a>当用户发送一个空的XML文档作为请求时会发生。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1491183894511"><a name="p1491183894511"></a><a name="p1491183894511"></a>提供正确的XML文档。</p>
</td>
</tr>
<tr id="row8329164018455"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p09481652104512"><a name="p09481652104512"></a><a name="p09481652104512"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p194845244513"><a name="p194845244513"></a><a name="p194845244513"></a>MissingRequiredHeader</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p99481452184516"><a name="p99481452184516"></a><a name="p99481452184516"></a>请求中缺少必要的头域。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p494815210456"><a name="p494815210456"></a><a name="p494815210456"></a>提供必要的头域。</p>
</td>
</tr>
<tr id="row85531741194512"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p894825212455"><a name="p894825212455"></a><a name="p894825212455"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p12948145274517"><a name="p12948145274517"></a><a name="p12948145274517"></a>MissingSecurityHeader</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p109497524450"><a name="p109497524450"></a><a name="p109497524450"></a>请求缺少一个必须的头。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1094919528458"><a name="p1094919528458"></a><a name="p1094919528458"></a>提供必要的头域。</p>
</td>
</tr>
<tr id="row92892423455"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p7949752154510"><a name="p7949752154510"></a><a name="p7949752154510"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p119491252204517"><a name="p119491252204517"></a><a name="p119491252204517"></a>TooManyBuckets</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1494965294511"><a name="p1494965294511"></a><a name="p1494965294511"></a>用户拥有的桶的数量达到了系统的上限，并且请求试图创建一个新桶。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p994965220457"><a name="p994965220457"></a><a name="p994965220457"></a>删除部分桶后重试。</p>
</td>
</tr>
<tr id="row595314210458"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p094955217456"><a name="p094955217456"></a><a name="p094955217456"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1894905244513"><a name="p1894905244513"></a><a name="p1894905244513"></a>TooManyCustomDomains</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p39491152154518"><a name="p39491152154518"></a><a name="p39491152154518"></a>配置了过多的用户域</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1594975211452"><a name="p1594975211452"></a><a name="p1594975211452"></a>删除部分用户域后重试。</p>
</td>
</tr>
<tr id="row786313434454"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p79491526458"><a name="p79491526458"></a><a name="p79491526458"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p139491852134514"><a name="p139491852134514"></a><a name="p139491852134514"></a>TooManyWrongSignature</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p119491052204510"><a name="p119491052204510"></a><a name="p119491052204510"></a>因高频错误请求被拒绝服务。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p69495523454"><a name="p69495523454"></a><a name="p69495523454"></a>更换正确的Access Key后重试。</p>
</td>
</tr>
<tr id="row3756554164518"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p186561277465"><a name="p186561277465"></a><a name="p186561277465"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p56561775468"><a name="p56561775468"></a><a name="p56561775468"></a>UnexpectedContent</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1165617134615"><a name="p1165617134615"></a><a name="p1165617134615"></a>该请求需要消息体而客户端没带，或该请求不需要消息体而客户端带了。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1065637114610"><a name="p1065637114610"></a><a name="p1065637114610"></a>根据说明重试。</p>
</td>
</tr>
<tr id="row195831271474"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p66287146479"><a name="p66287146479"></a><a name="p66287146479"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1558477154712"><a name="p1558477154712"></a><a name="p1558477154712"></a>AZRedundancyTypeNotSupported</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p6934105513478"><a name="p6934105513478"></a><a name="p6934105513478"></a>当前region不支持此AZRedundancy的桶</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p2934165594714"><a name="p2934165594714"></a><a name="p2934165594714"></a>选择合适的AZ Redundancy创桶</p>
</td>
</tr>
<tr id="row3544855134517"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p186561376469"><a name="p186561376469"></a><a name="p186561376469"></a>400 Bad Request</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p6656107134620"><a name="p6656107134620"></a><a name="p6656107134620"></a>UserKeyMustBeSpecified</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p36562719463"><a name="p36562719463"></a><a name="p36562719463"></a>该操作只有特殊用户可使用。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1365618717463"><a name="p1365618717463"></a><a name="p1365618717463"></a>请联系技术支持。</p>
</td>
</tr>
<tr id="row3367556124517"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p9894228184611"><a name="p9894228184611"></a><a name="p9894228184611"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p6894152864613"><a name="p6894152864613"></a><a name="p6894152864613"></a>AccessDenied</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p58951028194620"><a name="p58951028194620"></a><a name="p58951028194620"></a>拒绝访问，请求没有携带日期头域或者头域格式错误。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1589516287465"><a name="p1589516287465"></a><a name="p1589516287465"></a>请求携带正确的日期头域。</p>
</td>
</tr>
<tr id="row1625485744512"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1895628184611"><a name="p1895628184611"></a><a name="p1895628184611"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p989582874611"><a name="p989582874611"></a><a name="p989582874611"></a>AccessForbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p2895102804613"><a name="p2895102804613"></a><a name="p2895102804613"></a>权限不足，桶未配置CORS或者CORS规则不匹配。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p889515288462"><a name="p889515288462"></a><a name="p889515288462"></a>修改桶的CORS配置，或者根据桶的CORS配置发送匹配的OPTIONS请求。</p>
</td>
</tr>
<tr id="row4146205811456"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p88951228124611"><a name="p88951228124611"></a><a name="p88951228124611"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1889552818466"><a name="p1889552818466"></a><a name="p1889552818466"></a>AllAccessDisabled</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p5895122874616"><a name="p5895122874616"></a><a name="p5895122874616"></a>用户无权限执行某操作。桶名为禁用关键字。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p189542894620"><a name="p189542894620"></a><a name="p189542894620"></a>更换桶名。</p>
</td>
</tr>
<tr id="row9349823144613"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p5895182894616"><a name="p5895182894616"></a><a name="p5895182894616"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1289511288460"><a name="p1289511288460"></a><a name="p1289511288460"></a>DeregisterUserId</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1989618283467"><a name="p1989618283467"></a><a name="p1989618283467"></a>用户已经注销。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p589612834616"><a name="p589612834616"></a><a name="p589612834616"></a>充值或重新开户。</p>
</td>
</tr>
<tr id="row5311724124610"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p19896172824617"><a name="p19896172824617"></a><a name="p19896172824617"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p12896028124614"><a name="p12896028124614"></a><a name="p12896028124614"></a>InArrearOrInsufficientBalance</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1589622884619"><a name="p1589622884619"></a><a name="p1589622884619"></a>用户欠费或余额不足而没有权限进行某种操作。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p9896152812463"><a name="p9896152812463"></a><a name="p9896152812463"></a>充值。</p>
</td>
</tr>
<tr id="row6122514618"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p208969283467"><a name="p208969283467"></a><a name="p208969283467"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1789632818465"><a name="p1789632818465"></a><a name="p1789632818465"></a>InsufficientStorageSpace</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p589602812462"><a name="p589602812462"></a><a name="p589602812462"></a>存储空间不足。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p11896142820467"><a name="p11896142820467"></a><a name="p11896142820467"></a>超过配额限制，增加配额或删除部分对象。</p>
</td>
</tr>
<tr id="row186507259467"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p3896172811462"><a name="p3896172811462"></a><a name="p3896172811462"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p68974285469"><a name="p68974285469"></a><a name="p68974285469"></a>InvalidAccessKeyId</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p17897182816463"><a name="p17897182816463"></a><a name="p17897182816463"></a>系统记录中不存在客户提供的Access Key Id。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p9897192804614"><a name="p9897192804614"></a><a name="p9897192804614"></a>携带正确的Access Key Id。</p>
</td>
</tr>
<tr id="row746615268464"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p889711285462"><a name="p889711285462"></a><a name="p889711285462"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p38971928184617"><a name="p38971928184617"></a><a name="p38971928184617"></a>NotSignedUp</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p6897142834620"><a name="p6897142834620"></a><a name="p6897142834620"></a>你的帐户还没有在系统中注册，必须先在系统中注册了才能使用该帐户。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1889722817467"><a name="p1889722817467"></a><a name="p1889722817467"></a>先注册OBS服务。</p>
</td>
</tr>
<tr id="row19517153013468"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p413519402463"><a name="p413519402463"></a><a name="p413519402463"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1413514074618"><a name="p1413514074618"></a><a name="p1413514074618"></a>RequestTimeTooSkewed</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p813524018468"><a name="p813524018468"></a><a name="p813524018468"></a>请求的时间与服务器的时间相差太大。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p21351540194615"><a name="p21351540194615"></a><a name="p21351540194615"></a>检查客户端时间是否与当前时间相差太大。</p>
</td>
</tr>
<tr id="row198893717465"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p813574020467"><a name="p813574020467"></a><a name="p813574020467"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p6135240154615"><a name="p6135240154615"></a><a name="p6135240154615"></a>SignatureDoesNotMatch</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1513517400466"><a name="p1513517400466"></a><a name="p1513517400466"></a>请求中带的签名与系统计算得到的签名不一致。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p113544044618"><a name="p113544044618"></a><a name="p113544044618"></a>检查你的Secret Access Key和签名计算方法。</p>
</td>
</tr>
<tr id="row76585388468"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p16135940124612"><a name="p16135940124612"></a><a name="p16135940124612"></a>403 Forbidden</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p713513407465"><a name="p713513407465"></a><a name="p713513407465"></a>Unauthorized</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p4135840144614"><a name="p4135840144614"></a><a name="p4135840144614"></a>用户未实名认证。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p19135174016464"><a name="p19135174016464"></a><a name="p19135174016464"></a>请实名认证后重试。</p>
</td>
</tr>
<tr id="row19225641104610"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p88761057154612"><a name="p88761057154612"></a><a name="p88761057154612"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1887675714467"><a name="p1887675714467"></a><a name="p1887675714467"></a>NoSuchBucket</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p14876185754614"><a name="p14876185754614"></a><a name="p14876185754614"></a>指定的桶不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1876185734613"><a name="p1876185734613"></a><a name="p1876185734613"></a>先创桶再操作。</p>
</td>
</tr>
<tr id="row1889055004613"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p787795710466"><a name="p787795710466"></a><a name="p787795710466"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1887735711468"><a name="p1887735711468"></a><a name="p1887735711468"></a>NoSuchBucketPolicy</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p08779571464"><a name="p08779571464"></a><a name="p08779571464"></a>桶policy不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p7877165710465"><a name="p7877165710465"></a><a name="p7877165710465"></a>先配置桶policy。</p>
</td>
</tr>
<tr id="row474175194611"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p158771357184614"><a name="p158771357184614"></a><a name="p158771357184614"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1187745712466"><a name="p1187745712466"></a><a name="p1187745712466"></a>NoSuchCORSConfiguration</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p387713573460"><a name="p387713573460"></a><a name="p387713573460"></a>CORS配置不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p887735784615"><a name="p887735784615"></a><a name="p887735784615"></a>先配置CORS。</p>
</td>
</tr>
<tr id="row4391195234612"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p188771957124610"><a name="p188771957124610"></a><a name="p188771957124610"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p6877115714464"><a name="p6877115714464"></a><a name="p6877115714464"></a>NoSuchCustomDomain</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p48771657114610"><a name="p48771657114610"></a><a name="p48771657114610"></a>请求的用户域不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p587720575464"><a name="p587720575464"></a><a name="p587720575464"></a>先设置用户域。</p>
</td>
</tr>
<tr id="row1269253194612"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p28775579464"><a name="p28775579464"></a><a name="p28775579464"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1987716576462"><a name="p1987716576462"></a><a name="p1987716576462"></a>NoSuchKey</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1087735720467"><a name="p1087735720467"></a><a name="p1087735720467"></a>指定的Key不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p14877357174618"><a name="p14877357174618"></a><a name="p14877357174618"></a>先上传对象。</p>
</td>
</tr>
<tr id="row13790195364617"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1087735710463"><a name="p1087735710463"></a><a name="p1087735710463"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p08773573462"><a name="p08773573462"></a><a name="p08773573462"></a>NoSuchLifecycleConfiguration</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p787755714617"><a name="p787755714617"></a><a name="p787755714617"></a>请求的LifeCycle不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p787775717461"><a name="p787775717461"></a><a name="p787775717461"></a>先配置LifeCycle。</p>
</td>
</tr>
<tr id="row8536125484615"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p118771057204618"><a name="p118771057204618"></a><a name="p118771057204618"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p887785794610"><a name="p887785794610"></a><a name="p887785794610"></a>NoSuchUpload</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p7878657204618"><a name="p7878657204618"></a><a name="p7878657204618"></a>指定的多段上传不存在。Upload ID不存在，或者多段上传已经终止或完成。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p208780573465"><a name="p208780573465"></a><a name="p208780573465"></a>使用存在的段或重新初始化段。</p>
</td>
</tr>
<tr id="row61911855124610"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p118788572461"><a name="p118788572461"></a><a name="p118788572461"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p1587835754610"><a name="p1587835754610"></a><a name="p1587835754610"></a>NoSuchVersion</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1587855704616"><a name="p1587855704616"></a><a name="p1587855704616"></a>请求中指定的version ID与现存的所有版本都不匹配。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1387895710468"><a name="p1387895710468"></a><a name="p1387895710468"></a>使用正确的version ID。</p>
</td>
</tr>
<tr id="row455785674612"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p6878125754616"><a name="p6878125754616"></a><a name="p6878125754616"></a>404 Not Found</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p3878157114617"><a name="p3878157114617"></a><a name="p3878157114617"></a>NoSuchWebsiteConfiguration</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p08783571468"><a name="p08783571468"></a><a name="p08783571468"></a>请求的Website不存在。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p58781457114615"><a name="p58781457114615"></a><a name="p58781457114615"></a>先配置Website。</p>
</td>
</tr>
<tr id="row6544115919465"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p945320713476"><a name="p945320713476"></a><a name="p945320713476"></a>405 Method Not Allowed</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p44535794712"><a name="p44535794712"></a><a name="p44535794712"></a>MethodNotAllowed</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p74536774716"><a name="p74536774716"></a><a name="p74536774716"></a>指定的方法不允许操作在请求的资源上。</p>
<p id="p1525513515437"><a name="p1525513515437"></a><a name="p1525513515437"></a>对应返回的Message为：Specified method is not supported.</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p164534734716"><a name="p164534734716"></a><a name="p164534734716"></a>方法不允许。</p>
</td>
</tr>
<tr id="row153109817473"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p74178199476"><a name="p74178199476"></a><a name="p74178199476"></a>408 Request Timeout</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p541781954713"><a name="p541781954713"></a><a name="p541781954713"></a>RequestTimeout</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p174171719194712"><a name="p174171719194712"></a><a name="p174171719194712"></a>用户与Server之间的socket连接在超时时间内没有进行读写操作。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p241741910478"><a name="p241741910478"></a><a name="p241741910478"></a>检查网络后重试，或联系技术支持。</p>
</td>
</tr>
<tr id="row6258111017472"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p187433494711"><a name="p187433494711"></a><a name="p187433494711"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p387416344477"><a name="p387416344477"></a><a name="p387416344477"></a>BucketAlreadyExists</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p4874133416470"><a name="p4874133416470"></a><a name="p4874133416470"></a>请求的桶名已经存在。桶的命名空间是系统中所有用户共用的，选择一个不同的桶名再重试一次。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p11874934154719"><a name="p11874934154719"></a><a name="p11874934154719"></a>更换桶名。</p>
</td>
</tr>
<tr id="row710412115470"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p3874173414710"><a name="p3874173414710"></a><a name="p3874173414710"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p587414347472"><a name="p587414347472"></a><a name="p587414347472"></a>BucketAlreadyOwnedByYou</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p78741634104713"><a name="p78741634104713"></a><a name="p78741634104713"></a>发起该请求的用户已经创建过了这个名字的桶，并拥有这个桶。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p198741834184717"><a name="p198741834184717"></a><a name="p198741834184717"></a>不需要再创桶了。</p>
</td>
</tr>
<tr id="row426742810476"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p787483411473"><a name="p787483411473"></a><a name="p787483411473"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p287493414713"><a name="p287493414713"></a><a name="p287493414713"></a>BucketNotEmpty</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p108742034104716"><a name="p108742034104716"></a><a name="p108742034104716"></a>用户尝试删除的桶不为空。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1787410342474"><a name="p1787410342474"></a><a name="p1787410342474"></a>先删除桶中对象，然后再删桶。</p>
</td>
</tr>
<tr id="row86939182173"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1469351815171"><a name="p1469351815171"></a><a name="p1469351815171"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p36931518181715"><a name="p36931518181715"></a><a name="p36931518181715"></a>FsObjectConflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p116938185174"><a name="p116938185174"></a><a name="p116938185174"></a>用户上传或创建文件失败</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p938082882614"><a name="p938082882614"></a><a name="p938082882614"></a>检查创建文件规则。例如是否在不允许覆盖的场景下覆盖文件、是否在POSIX语义下在文件下上传文件（将文件当作目录）</p>
</td>
</tr>
<tr id="row191241329154711"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p8874934194717"><a name="p8874934194717"></a><a name="p8874934194717"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p118745345472"><a name="p118745345472"></a><a name="p118745345472"></a>InvalidBucketState</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p12874934204710"><a name="p12874934204710"></a><a name="p12874934204710"></a>无效的桶状态，配置跨Region复制后不允许关闭桶多版本。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p587443415478"><a name="p587443415478"></a><a name="p587443415478"></a>不关闭桶的多版本或取消跨Region复制。</p>
</td>
</tr>
<tr id="row1783617295472"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p987423464711"><a name="p987423464711"></a><a name="p987423464711"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p287473404716"><a name="p287473404716"></a><a name="p287473404716"></a>OperationAborted</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p2874834124714"><a name="p2874834124714"></a><a name="p2874834124714"></a>另外一个冲突的操作当前正作用在这个资源上，请重试。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p3874123415474"><a name="p3874123415474"></a><a name="p3874123415474"></a>等待一段时间后重试。</p>
</td>
</tr>
<tr id="row856233014712"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p7874203414711"><a name="p7874203414711"></a><a name="p7874203414711"></a>409 Conflict</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p587412347474"><a name="p587412347474"></a><a name="p587412347474"></a>ServiceNotSupported</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p287417349471"><a name="p287417349471"></a><a name="p287417349471"></a>请求的方法服务端不支持。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p58744346479"><a name="p58744346479"></a><a name="p58744346479"></a>服务端不支持，请联系技术支持。</p>
</td>
</tr>
<tr id="row21431336174713"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p334494215474"><a name="p334494215474"></a><a name="p334494215474"></a>411 Length Required</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p5344194254718"><a name="p5344194254718"></a><a name="p5344194254718"></a>MissingContentLength</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1344194244710"><a name="p1344194244710"></a><a name="p1344194244710"></a>必须要提供HTTP消息头中的Content-Length字段。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p14344174264717"><a name="p14344174264717"></a><a name="p14344174264717"></a>提供Content-Length消息头。</p>
</td>
</tr>
<tr id="row54471543134713"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p175356516478"><a name="p175356516478"></a><a name="p175356516478"></a>412 Precondition Failed</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p105353513476"><a name="p105353513476"></a><a name="p105353513476"></a>PreconditionFailed</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p16535165119478"><a name="p16535165119478"></a><a name="p16535165119478"></a>用户指定的先决条件中至少有一项没有包含。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1553565113478"><a name="p1553565113478"></a><a name="p1553565113478"></a>根据返回消息体中的Condition提示进行修改。</p>
</td>
</tr>
<tr id="row15453952144716"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p10428101488"><a name="p10428101488"></a><a name="p10428101488"></a>416 Client Requested Range Not Satisfiable</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p114281206482"><a name="p114281206482"></a><a name="p114281206482"></a>InvalidRange</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1142812016481"><a name="p1142812016481"></a><a name="p1142812016481"></a>请求的range不可获得。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p1142814094811"><a name="p1142814094811"></a><a name="p1142814094811"></a>携带正确的range重试。</p>
</td>
</tr>
<tr id="row1453105544720"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p8388141024817"><a name="p8388141024817"></a><a name="p8388141024817"></a>500 Internal Server Error</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p173880103481"><a name="p173880103481"></a><a name="p173880103481"></a>InternalError</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1438861074815"><a name="p1438861074815"></a><a name="p1438861074815"></a>系统遇到内部错误，请重试。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p2038821074810"><a name="p2038821074810"></a><a name="p2038821074810"></a>请联系技术支持。</p>
</td>
</tr>
<tr id="row1030414564479"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1438871024818"><a name="p1438871024818"></a><a name="p1438871024818"></a>501 Not Implemented</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p938891019487"><a name="p938891019487"></a><a name="p938891019487"></a>ServiceNotImplemented</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p1838811013482"><a name="p1838811013482"></a><a name="p1838811013482"></a>请求的方法服务端没有实现。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p0388910194810"><a name="p0388910194810"></a><a name="p0388910194810"></a>当前不支持，请联系技术支持。</p>
</td>
</tr>
<tr id="row9118125614720"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p3388141024810"><a name="p3388141024810"></a><a name="p3388141024810"></a>503 Service Unavailable</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p3388191024812"><a name="p3388191024812"></a><a name="p3388191024812"></a>ServiceUnavailable</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p33881710184816"><a name="p33881710184816"></a><a name="p33881710184816"></a>服务器过载或者内部错误异常。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p173888109481"><a name="p173888109481"></a><a name="p173888109481"></a>等待一段时间后重试，或联系技术支持。</p>
</td>
</tr>
<tr id="row1242578124811"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.1 "><p id="p1638871024818"><a name="p1638871024818"></a><a name="p1638871024818"></a>503 Service Unavailable</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.2 "><p id="p4388210134816"><a name="p4388210134816"></a><a name="p4388210134816"></a>SlowDown</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.3 "><p id="p9388111084814"><a name="p9388111084814"></a><a name="p9388111084814"></a>请降低请求频率。</p>
</td>
<td class="cellrowborder" valign="top" width="25%" headers="mcps1.1.5.1.4 "><p id="p16389171054820"><a name="p16389171054820"></a><a name="p16389171054820"></a>请降低请求频率。</p>
</td>
</tr>
</tbody>
</table>

