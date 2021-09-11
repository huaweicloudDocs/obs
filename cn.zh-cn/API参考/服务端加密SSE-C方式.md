# 服务端加密SSE-C方式<a name="obs_04_0107"></a>

SSE-C方式，OBS使用用户提供的密钥和密钥的MD5值进行服务端加密。

OBS不存储您提供的加密密钥，如果您丢失加密密钥，则会无法获取该对象。SSE-C方式新增加六个头域来支持SSE-C加密。

使用SSE-C方式加密对象，您必须使用下面的三个头域。

**表 1**  SSE-C方式加密对象使用的头域

<a name="table101231237144214"></a>
<table><thead align="left"><tr id="row0125153764211"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p171250379427"><a name="p171250379427"></a><a name="p171250379427"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p5125193718420"><a name="p5125193718420"></a><a name="p5125193718420"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1412573764215"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p18431172634319"><a name="p18431172634319"></a><a name="p18431172634319"></a>x-obs-server-side-encryption-customer-algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1843282614431"><a name="p1843282614431"></a><a name="p1843282614431"></a>SSE-C方式下使用该头域，该头域表示加密对象使用的算法。</p>
<p id="p1143292694311"><a name="p1143292694311"></a><a name="p1143292694311"></a>示例：x-obs-server-side-encryption-customer-algorithm：AES256</p>
</td>
</tr>
<tr id="row1112515375428"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p143416261434"><a name="p143416261434"></a><a name="p143416261434"></a>x-obs-server-side-encryption-customer-key</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p104351326134318"><a name="p104351326134318"></a><a name="p104351326134318"></a>SSE-C方式下使用该头域，该头域表示加密对象使用的密钥，头域值是256位或者512位密钥的base64编码。</p>
<p id="p16437132617435"><a name="p16437132617435"></a><a name="p16437132617435"></a>示例：x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=</p>
</td>
</tr>
<tr id="row151254372427"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1944018267432"><a name="p1944018267432"></a><a name="p1944018267432"></a>x-obs-server-side-encryption-customer-key-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p144252654312"><a name="p144252654312"></a><a name="p144252654312"></a>SSE-C方式下使用该头域，该头域表示加密对象使用的密钥的MD5值，头域值是加密密钥MD5值的base64编码。MD5值用于验证密钥传输过程中没有出错。</p>
<p id="p10442192613436"><a name="p10442192613436"></a><a name="p10442192613436"></a>示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==</p>
</td>
</tr>
</tbody>
</table>

该新增的三个头域可以应用于如下接口：

-   PUT上传对象
-   POST上传对象
-   复制对象（新增的头域针对目标对象）
-   获取对象元数据
-   获取对象内容
-   初始化上传段任务
-   上传段
-   拷贝段（新增的头域针对目标段）

针对复制对象和拷贝段，另外增加三个头域支持源对象是SSE-C加密的场景。

**表 2**  源对象是SSE-C加密的头域

<a name="table2106157194518"></a>
<table><thead align="left"><tr id="row8106195715458"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p20106155754514"><a name="p20106155754514"></a><a name="p20106155754514"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p8106135734511"><a name="p8106135734511"></a><a name="p8106135734511"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1910720576459"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1569686"><a name="p1569686"></a><a name="p1569686"></a>x-obs-copy-source-server-side-encryption-customer-algorithm</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p60035769"><a name="p60035769"></a><a name="p60035769"></a>SSE-C方式下使用该头域，该头域表示解密源对象使用的算法。</p>
<p id="p3451011"><a name="p3451011"></a><a name="p3451011"></a>示例：x-obs-server-side-encryption-customer-algorithm：AES256</p>
</td>
</tr>
<tr id="row510705704518"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p32759143"><a name="p32759143"></a><a name="p32759143"></a>x-obs-copy-source-server-side-encryption-customer-key</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p36244931"><a name="p36244931"></a><a name="p36244931"></a>SSE-C方式下使用该头域，该头域表示解密源对象使用的密钥。</p>
<p id="p57768927"><a name="p57768927"></a><a name="p57768927"></a>示例：x-obs-copy-source-server-side-encryption-customer-algorithm：K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=</p>
</td>
</tr>
<tr id="row16107185794515"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p36290124"><a name="p36290124"></a><a name="p36290124"></a>x-obs-copy-source-server-side-encryption-customer-key-MD5</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p53818954"><a name="p53818954"></a><a name="p53818954"></a>SSE-C方式下使用该头域，该头域表示解密源对象使用的密钥的MD5值。MD5值用于验证密钥传输过程中没有出错。</p>
<p id="p14608539"><a name="p14608539"></a><a name="p14608539"></a>示例：x-obs-copy-source-server-side-encryption-customer-key:4XvB3tbNTN+tIEVa0/fGaQ==</p>
</td>
</tr>
</tbody>
</table>

## 请求示例1<a name="section151461344181918"></a>

**上传SSE-C加密对象**

```
PUT /encryp2 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:12:00 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:mZSfafoM+llApk0HGOThlqeccu0=
x-obs-server-side-encryption-customer-algorithm:AES256
x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=
x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==
Content-Length: 5242

[5242 Byte object contents]
```

## 响应示例1<a name="section039121783514"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D45E0017055619BD02B8
ETag: "0f91242c7f3d86f98ae572a686d0696e"
x-obs-server-side-encryption-customer-algorithm: AES256
x-obs-server-side-encryption-customer-key-MD5: 4XvB3tbNTN+tIEVa0/fGaQ==
x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCSSAJ8bTNJV0X+Ote1PtuWecqyMh6zBJ
Date: Wed, 06 Jun 2018 09:12:00 GMT
Content-Length: 0
```

## 请求示例2<a name="section3959940113518"></a>

**将SSE-C加密对象拷贝为KMS加密对象**

```
PUT /kmsobject HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:20:10 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:mZSfafoM+llApk0HGOThlqeccu0=
x-obs-copy-source-server-side-encryption-customer-algorithm:AES256
x-obs-copy-source-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=
x-obs-copy-source-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==
x-obs-server-side-encryption: kms
x-obs-copy-source: /examplebucket/encryp2
Content-Length: 5242

[5242 Byte object contents]
```

## 响应示例2<a name="section1589193223912"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164848E0FC70528B9D92C41
ETag: "1072e1b96b47d7ec859710068aa70d57"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-4:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTkkRzQXs9ECzZcavVRncBqqYNkoAEsr
Date: Wed, 06 Jun 2018 09:20:10 GMT
Content-Length: 0
```

## 请求示例3<a name="section13241145493917"></a>

**在URL中携带签名并上传SSE-C加密对象**

```
PUT /encrypobject?AccessKeyId=H4IPJX0TQTHTHEBQQCEC&Expires=1532688887&Signature=EQmDuOhWLUrzrzRNZxwS72CXeXM%3D HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
x-obs-server-side-encryption-customer-algorithm: AES256
x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=
x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==
Content-Length: 5242
Expect: 100-continue

[5242 Byte object contents]
```

## 响应示例3<a name="section1990581416405"></a>

```
HTTP/1.1 100 Continue
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 804F00000164DB5E5B7FB908D3BA8E00
ETag: "1072e1b96b47d7ec859710068aa70d57"
x-obs-server-side-encryption-customer-algorithm: AES256
x-obs-server-side-encryption-customer-key-MD5: 4XvB3tbNTN+tIEVa0/fGaQ==
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTlpxILjhVK/heKOWIP8Wn2IWmQoerfw
Content-Length: 0
```

