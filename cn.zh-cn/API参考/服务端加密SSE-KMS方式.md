# 服务端加密SSE-KMS方式<a name="obs_04_0106"></a>

## 功能介绍<a name="section372413345714"></a>

SSE-KMS方式，OBS使用KMS（Key Management Service）服务提供的密钥进行服务端加密。用户可以创建自定义密钥，用于SSE-KMS加密。如果未指定，则用户首次向区域中的桶上传SSE-KMS加密的对象时，OBS将自动为您创建一个默认密钥。自定义密钥或默认密钥用于加密和解密KMS生成的数据加解密密钥。

>![](public_sys-resources/icon-note.gif) **说明：** 
>使用非默认IAM项目下的自定义密钥对桶内对象进行SSE-KMS加密，只有密钥拥有者可以对加密后的对象进行上传下载类操作，非密钥拥有者不能对加密对象进行上传下载类操作。
>使用默认密钥向区域中的桶上传SSE-KMS加密的对象时，该默认密钥归属于对象上传者，非密钥拥有者不能对使用默认密钥加密的对象进行上传下载类操作。

## 新增头域<a name="section1132124805718"></a>

SSE-KMS方式新增加两个头域，用户可以通过配置[表1](#table1716921114398)中的头域来实现SSE-KMS加密。

您也可以通过配置桶的默认加密方式来对桶内的对象进行加密。在为桶配置默认加密后，对于任何不带加密头域的上传对象的请求，将使用桶的默认加密配置进行加密。有关桶的加密配置的更多信息请参考[设置桶的加密配置](设置桶的加密配置.md)章节。

**表 1**  SSE-KMS方式使用的头域

|名称|描述|
|--|--|
|x-obs-server-side-encryption|使用该头域表示服务端加密是SSE-KMS方式。对象使用SSE-KMS方式加密。类型：String示例：x-obs-server-side-encryption：kms|
|x-obs-server-side-data-encryption|SSE-KMS方式下使用该头域，该头域表示对象使用的数据加密算法，有效值为SM4。类型：String示例：x-obs-server-side-data-encryption：SM4|
|x-obs-server-side-encryption-kms-key-id|SSE-KMS方式下使用该头域，该头域表示加密对象使用的主密钥，如果用户没有提供该头域，那么默认的主密钥将会被使用。如果默认主密钥不存在，将默认创建并使用。类型：String支持两种格式的描述方式：1. regionID:domainID(租户ID):key/key_id或者2.key_id其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是从数据加密服务创建的密钥ID。示例：1. x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0  或者2. x-obs-server-side-encryption-kms-key-id：4f1cd4de-ab64-4807-920a-47fc42e7f0d0|


## 支持头域的接口<a name="section8313163616591"></a>

以下接口支持配置SSE-KMS相关头域：

-   [PUT上传对象](PUT上传.md)
-   [POST上传对象](POST上传.md)（需要将x-obs-server-side-encryption、x-obs-server-side-data-encryption和x-obs-server-side-encryption-kms-key-id放到表单中，而不是头域中）
-   [复制对象](复制对象.md)  （新增的头域针对目标对象）
-   [初始化上传段任务](初始化上传段任务.md)

您可以通过设置桶策略，来限制指定桶的请求头域，如果您要对桶中的所有对象执行服务端加密限制，则可通过设置桶策略达成。例如，如果要求本租户的上传对象请求不包含服务端加密 \(SSE-KMS\) 的相关头域x-obs-server-side-encryption:"kms"，则可使用以下桶策略达成：

```
{
    "Statement": [
        {
            "Sid": "DenyUnEncryptedObjectUploads",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "PutObject",
            "Resource": "YourBucket/*",
            "Condition": {
                "StringNotEquals": {
                    "x-obs-server-side-encryption": "kms"
                }
            }
        }
    ]
}
```

## 请求示例：使用默认密钥对上传的对象进行加密<a name="section9676048111413"></a>

```
PUT /encryp1 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:08:21 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:f3/7eS6MFbW3JO4+7I5AtyAQENU=
x-obs-server-side-encryption:kms
Content-Length: 5242
Expect: 100-continue

[5242 Byte object contents]
```

## 响应示例：使用默认密钥对上传的对象进行加密<a name="section5769165793118"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D45AA81D038B6AE4C482
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-4:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTv7cHmAnGfBAGXUHeibUsiETTNqlCqC
Date: Wed, 06 Jun 2018 09:08:21 GMT
Content-Length: 0
```

## 请求示例：使用指定密钥对上传的对象进行加密<a name="section1066121573210"></a>

```
PUT /encryp1 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:08:50 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:f3/PWjkXYTYGs5lPOctTNEI2QENU=
x-obs-server-side-encryption:kms
x-obs-server-side-encryption-kms-key-id: 522d6070-5ad3-4765-43a7-a7d1-ab21f498482d
Content-Length: 5242
Expect: 100-continue

[5242 Byte object contents]
```

## 响应示例：使用指定密钥对上传的对象进行加密<a name="section3936203519339"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: 8DF400000163D45AA81D038B6AE4C482
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-4:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-43a7-a7d1-ab21f498482d
x-obs-id-2: 32AAAUJAIAABAdiAEAABA09AEAABCTv7cHmAn12BAG83ibUsiET5eqlCqg
Date: Wed, 06 Jun 2018 09:08:50 GMT
Content-Length: 0
```

## 请求示例：将普通对象拷贝为加密对象，且指定加密密钥<a name="section1354925617332"></a>

```
PUT /destobject HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
x-obs-server-side-encryption:kms
x-obs-server-side-encryption-kms-key-id: cn-north-4:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
Accept: */*
Date: Wed, 06 Jun 2018 09:10:29 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:SH3uTrElaGWarVI1uTq325kTVCI=
x-obs-copy-source: /bucket/srcobject1
```

## 响应示例：将普通对象拷贝为加密对象，且指定加密密钥<a name="section1665573753412"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB78000001648480AF3900CED7F15155
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-4:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: oRAXhgwdaLc9wKVHqTLSmQB7I35D+32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS
Date: Wed, 06 Jun 2018 09:10:29 GMT
Content-Length: 0
```

## 请求示例：在URL中携带签名并上传加密对象<a name="section9689143461811"></a>

```
PUT /destobject?AccessKeyId=UI3SN1SRUQE14OYBKTZB&Expires=1534152518&x-obs-server-side-encryption=kms&Signature=chvmG7%2FDA%2FDCQmTRJu3xngldJpg%3D HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: Wed, 06 Jun 2018 09:10:29 GMT
```

## 响应示例：在URL中携带签名并上传加密对象<a name="section1970120340184"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB78000001648480AF3900CED7F15155
ETag: "d8bffdfbab5345d91ac05141789d2477"
x-obs-server-side-encryption: kms
x-obs-server-side-encryption-kms-key-id: cn-north-4:783fc6652cf246c096ea836694f71855:key/522d6070-5ad3-4765-9737-9312ddc72cdb
x-obs-id-2: oRAXhgwdaLc9wKVHqTLSmQB7I35D+32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS
Date: Wed, 06 Jun 2018 09:10:29 GMT
Content-Length: 0
```

