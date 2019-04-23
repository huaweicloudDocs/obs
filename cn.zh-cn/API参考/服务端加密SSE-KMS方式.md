# 服务端加密SSE-KMS方式<a name="ZH-CN_TOPIC_0100846795"></a>

SSE-KMS方式，OBS使用KMS（Key Management Service）服务提供的密钥进行服务端加密。用户首次向区域中的桶上传SSE-KMS 加密的对象时，OBS将自动为您创建一个默认客户主密钥，客户主密钥用于加密和解密KMS提供的密钥。SSE-KMS方式不支持用户自建密钥。Bucket ACL/Policy不支持SSE-KMS加密对象进行跨租户授权访问。

SSE-KMS方式新增加两个头域来支持SSE-KMS加密。

**表 1**  SSE-KMS方式使用的头域

<a name="table1716921114398"></a>
<table><thead align="left"><tr id="row17170311133917"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p17170131112393"><a name="p17170131112393"></a><a name="p17170131112393"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p5170161123920"><a name="p5170161123920"></a><a name="p5170161123920"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row21701119392"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p10565331133917"><a name="p10565331133917"></a><a name="p10565331133917"></a>x-obs-server-side-encryption</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p11565431143913"><a name="p11565431143913"></a><a name="p11565431143913"></a>使用该头域表示服务端加密是SSE-KMS方式。对象使用SSE-KMS方式加密。</p>
<p id="p8363154416375"><a name="p8363154416375"></a><a name="p8363154416375"></a>类型：字符串</p>
<p id="p12566173111399"><a name="p12566173111399"></a><a name="p12566173111399"></a>示例：x-obs-server-side-encryption：kms</p>
</td>
</tr>
<tr id="row11701119396"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p125672313392"><a name="p125672313392"></a><a name="p125672313392"></a>x-obs-server-side-encryption-kms-key-id</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p456853193912"><a name="p456853193912"></a><a name="p456853193912"></a>SSE-KMS方式下使用该头域，该头域表示加密对象使用的主密钥，如果用户没有提供该头域，那么默认的主密钥将会被使用。</p>
<p id="p12882047173716"><a name="p12882047173716"></a><a name="p12882047173716"></a>类型：字符串</p>
<p id="p6679135313114"><a name="p6679135313114"></a><a name="p6679135313114"></a>支持两种格式的描述方式：</p>
<p id="p17964154220128"><a name="p17964154220128"></a><a name="p17964154220128"></a>1. regionID:domainID(租户ID):key/key_id 或者</p>
<p id="p090816596123"><a name="p090816596123"></a><a name="p090816596123"></a>2.key_id</p>
<p id="p558627121315"><a name="p558627121315"></a><a name="p558627121315"></a>其中regionID是使用秘钥所属region的ID；domainID是使用秘钥所属租户的租户ID；key_id是从<span>数据加密服务</span>创建的秘钥ID。</p>
<p id="p17830152818144"><a name="p17830152818144"></a><a name="p17830152818144"></a>示例：</p>
<p id="p4765922"><a name="p4765922"></a><a name="p4765922"></a>1. x-obs-server-side-encryption-kms-key-id：cn-north-1:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0  或者</p>
<p id="p9607740151414"><a name="p9607740151414"></a><a name="p9607740151414"></a>2. x-obs-server-side-encryption-kms-key-id：4f1cd4de-ab64-4807-920a-47fc42e7f0d0</p>
</td>
</tr>
</tbody>
</table>

该新增的两个头域可以应用于如下接口：

-   PUT 上传对象
-   POST 上传对象（需要将x-obs-server-side-encryption和x-obs-server-side-encryption-kms-key-id放到表单中，而不是头域中）
-   复制对象 （新增的头域针对目标对象）
-   初始化上传段任务

OBS支持Bucket Policy，如果您要对所有存储在桶中的对象执行服务端加密限制，则可以使用这些策略。例如，如果本租户的上传对象请求不包含用于请求服务端加密 \(SSE-KMS\) 的头域x-obs-server-side-encryption:"kms"，则下面的Bucket Policy将拒绝该上传对象请求。

```
{
"Statement":[{
"Sid":"DenyUnEncryptedObjectUploads",
"Effect":"Deny",
"Principal":"*",
"Action":"PutObject",
"Resource":"YourBucket/*",
"Condition":{
"StringNotEquals":{
"x-obs-server-side-encryption":"kms"
}
}
}
}
```

## 请求示例1<a name="section9676048111413"></a>

****使用默认秘钥对上传的对象进行加密****

```
PUT /encryp1 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:08:21 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:f3/7eS6MFbW3JO4+7I5AtyAQENU=
x-obs-server-side-encryption:kms
Content-Length: 5242
Expect: 100-continue

[5242 Byte object contents]
```

## 响应示例1<a name="section5769165793118"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D45AA81D038B6AE4C482
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-1:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTv7cHmAnGfBAGXUHeibUsiETTNqlCqC
Date: Wed, 06 Jun 2018 09:08:21 GMT
Content-Length: 0
```

## 请求示例2<a name="section1066121573210"></a>

**使用指定秘钥对上传的对象进行加密**

```
PUT /encryp1 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:08:50 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:f3/PWjkXYTYGs5lPOctTNEI2QENU=
x-obs-server-side-encryption:kms
x-obs-server-side-encryption-kms-key-id: 522d6070-5ad3-4765-43a7-a7d1-ab21f498482d
Content-Length: 5242
Expect: 100-continue

[5242 Byte object contents]
```

## 响应示例2<a name="section3936203519339"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D45AA81D038B6AE4C482
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-1:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-43a7-a7d1-ab21f498482d
x-obs-id-2: 32AAAUJAIAABAdiAEAABA09AEAABCTv7cHmAn12BAG83ibUsiET5eqlCqg
Date: Wed, 06 Jun 2018 09:08:50 GMT
Content-Length: 0
```

## 请求示例3<a name="section1354925617332"></a>

**将普通对象拷贝为加密对象，且指定加密秘钥**

```
PUT /destobject HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
x-obs-server-side-encryption:kms
x-obs-server-side-encryption-kms-key-id: cn-north-1:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
Accept: */*
Date: Wed, 06 Jun 2018 09:10:29 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:SH3uTrElaGWarVI1uTq325kTVCI=
x-obs-copy-source: /bucket/srcobject1
```

## 响应示例3<a name="section1665573753412"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB78000001648480AF3900CED7F15155
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-1:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: oRAXhgwdTLc9wKVHqTLSmQB7I35D+32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS
Date: Wed, 06 Jun 2018 09:10:29 GMT
Content-Length: 0
```

## 请求示例4<a name="section9689143461811"></a>

**在Query参数中携带签名并上传加密对象**

```
PUT /destobject?AccessKeyId=UI3SN1SRUQE14OYBKTZB&Expires=1534152518&x-obs-server-side-encryption=kms&Signature=chvmG7%2FDA%2FDCQmTRJu3xngldJpg%3D HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-1.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:10:29 GMT
```

## 响应示例4<a name="section1970120340184"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB78000001648480AF3900CED7F15155
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-1:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: oRAXhgwdTLc9wKVHqTLSmQB7I35D+32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS
Date: Wed, 06 Jun 2018 09:10:29 GMT
Content-Length: 0
```

