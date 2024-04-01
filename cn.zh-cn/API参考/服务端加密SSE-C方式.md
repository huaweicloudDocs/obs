# 服务端加密SSE-C方式<a name="obs_04_0107"></a>

## 功能介绍<a name="section104215161210"></a>

SSE-C方式，OBS使用用户提供的密钥和密钥的MD5值进行服务端加密。

## 新增头域<a name="section794711344129"></a>

OBS不存储您提供的加密密钥，如果您丢失加密密钥，则会无法获取该对象。SSE-C方式新增加六个头域来支持SSE-C加密。

使用SSE-C方式加密对象，您必须使用下面的三个头域。

**表 1**  SSE-C方式加密对象使用的头域

|名称|描述|
|--|--|
|x-obs-server-side-encryption-customer-algorithm|SSE-C方式下使用该头域，该头域表示加密对象使用的算法。示例：x-obs-server-side-encryption-customer-algorithm: AES256|
|x-obs-server-side-encryption-customer-key|SSE-C方式下使用该头域，该头域表示加密对象使用的密钥，头域值是256位密钥的base64编码。示例：x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=|
|x-obs-server-side-encryption-customer-key-MD5|SSE-C方式下使用该头域，该头域表示加密对象使用的密钥的MD5值，头域值是加密密钥MD5值的base64编码。MD5值用于验证密钥传输过程中没有出错。示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==|


该新增的三个头域可以应用于如下接口：

-   [PUT上传对象](PUT上传.md)
-   [POST上传对象](POST上传.md)
-   [复制对象](复制对象.md)（新增的头域针对目标对象）
-   [获取对象元数据](获取对象元数据.md)
-   [获取对象内容](下载对象.md)
-   [初始化上传段任务](初始化上传段任务.md)
-   [上传段](上传段.md)
-   [拷贝段](拷贝段.md)（新增的头域针对目标段）

针对复制对象和拷贝段，另外增加三个头域支持源对象是SSE-C加密的场景。

**表 2**  源对象是SSE-C加密的头域

|名称|描述|
|--|--|
|x-obs-copy-source-server-side-encryption-customer-algorithm|SSE-C方式下使用该头域，该头域表示解密源对象使用的算法。示例：x-obs-server-side-encryption-customer-algorithm: AES256|
|x-obs-copy-source-server-side-encryption-customer-key|SSE-C方式下使用该头域，该头域表示解密源对象使用的密钥。示例：x-obs-copy-source-server-side-encryption-customer-algorithm: K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=|
|x-obs-copy-source-server-side-encryption-customer-key-MD5|SSE-C方式下使用该头域，该头域表示解密源对象使用的密钥的MD5值。MD5值用于验证密钥传输过程中没有出错。示例：x-obs-copy-source-server-side-encryption-customer-key:4XvB3tbNTN+tIEVa0/fGaQ==|


## 请求示例：上传SSE-C加密对象<a name="section151461344181918"></a>

```
PUT /encryp2 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:12:00 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:mZSfafoM+llApk0HGOThlqeccu0=
x-obs-server-side-encryption-customer-algorithm:AES256
x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=
x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==
Content-Length: 5242

[5242 Byte object contents]
```

## 响应示例：上传SSE-C加密对象<a name="section039121783514"></a>

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

## 请求示例：将SSE-C加密对象拷贝为KMS加密对象<a name="section3959940113518"></a>

```
PUT /kmsobject HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:20:10 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:mZSfafoM+llApk0HGOThlqeccu0=
x-obs-copy-source-server-side-encryption-customer-algorithm:AES256
x-obs-copy-source-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=
x-obs-copy-source-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==
x-obs-server-side-encryption: kms
x-obs-copy-source: /examplebucket/encryp2
Content-Length: 5242

[5242 Byte object contents]
```

## 响应示例：将SSE-C加密对象拷贝为KMS加密对象<a name="section1589193223912"></a>

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

## 请求示例：在URL中携带签名并上传SSE-C加密对象<a name="section13241145493917"></a>

```
PUT /encrypobject?AccessKeyId=H4IPJX0TQTHTHEBQQCEC&Expires=1532688887&Signature=EQmDuOhaLUrzrzRNZxwS72CXeXM%3D HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
x-obs-server-side-encryption-customer-algorithm: AES256
x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=
x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==
Content-Length: 5242
Expect: 100-continue

[5242 Byte object contents]
```

## 响应示例：在URL中携带签名并上传SSE-C加密对象<a name="section1990581416405"></a>

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

