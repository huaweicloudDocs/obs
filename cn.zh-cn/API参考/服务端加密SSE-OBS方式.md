# 服务端加密SSE-OBS方式<a name="obs_04_0173"></a>

## 功能介绍<a name="section052314617525"></a>

SSE-OBS方式，OBS使用服务自身提供的密钥进行服务端加密。与SSE-KMS的区别在于SSE-OBS是OBS管理密钥，而非KMS。

## 新增头域<a name="section13281481530"></a>

SSE-OBS方式用户可以通过配置[表1](#table9548129165313)中的头域来实现SSE-OBS加密。

您也可以通过配置桶的默认加密方式来对桶内的对象进行加密。在为桶配置默认加密后，对于任何不带加密头域的上传对象的请求，将使用桶的默认加密配置进行加密。有关桶的加密配置的更多信息请参考[设置桶的加密配置](设置桶的加密配置.md)章节。

**表 1**  SSE-OBS方式使用的头域

|名称|描述|
|--|--|
|x-obs-server-side-encryption|使用该头域表示服务端加密是SSE-OBS方式。对象使用SSE-OBS方式加密。类型：String示例：x-obs-server-side-encryption：AES256|


## 支持头域的接口<a name="section15481741145315"></a>

以下接口支持配置SSE-OBS相关头域：

-   [PUT上传对象](PUT上传.md)
-   [POST上传对象](POST上传.md)（需要将x-obs-server-side-encryption放到表单中，而不是头域中）
-   [复制对象](复制对象.md)  （新增的头域针对目标对象）
-   [初始化上传段任务](初始化上传段任务.md)

您可以通过设置桶策略，来限制指定桶的请求头域，如果您要对桶中的所有对象执行服务端加密限制，则可通过设置桶策略达成。例如，如果要求本租户的上传对象请求不包含服务端加密 \(SSE-OBS\) 的相关头域x-obs-server-side-encryption:"AES256"，则可使用以下桶策略达成：

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
                    "x-obs-server-side-encryption": "AES256" 
                } 
            } 
        } 
    ] 
}
```

## 请求示例：使用默认密钥对上传的对象进行加密<a name="section145877075410"></a>

```
PUT /encryp1 HTTP/1.1 
User-Agent: curl/7.29.0 
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */* 
Date: Wed, 06 Jun 2018 09:08:21 GMT 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:f3/7eS6MFbW3JO4+7I5AtyAQENU= 
x-obs-server-side-encryption:AES256 
Content-Length: 5242 
Expect: 100-continue 
 
[5242 Byte object contents]
```

## 响应示例：使用默认密钥对上传的对象进行加密<a name="section35918055420"></a>

```
HTTP/1.1 200 OK 
Server: OBS 
x-obs-request-id: 8DF400000163D45AA81D038B6AE4C482 
ETag: "d8bffdfbab5345d91ac05141789d2477" 
x-obs-server-side-encryption: AES256 
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTv7cHmAnGfBAGXUHeibUsiETTNqlCqC 
Date: Wed, 06 Jun 2018 09:08:21 GMT 
Content-Length: 0
```

## 请求示例：将普通对象拷贝为加密对象<a name="section359216075411"></a>

```
PUT /destobject HTTP/1.1 
User-Agent: curl/7.29.0 
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
x-obs-server-side-encryption:AES256 
Accept: */* 
Date: Wed, 06 Jun 2018 09:10:29 GMT 
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:SH3uTrElaGWarVI1uTq325kTVCI= 
x-obs-copy-source: /bucket/srcobject1
```

## 响应示例：将普通对象拷贝为加密对象<a name="section12592140165415"></a>

```
HTTP/1.1 200 OK 
Server: OBS 
x-obs-request-id: BB78000001648480AF3900CED7F15155 
ETag: "d8bffdfbab5345d91ac05141789d2477" 
x-obs-server-side-encryption: AES256 
x-obs-id-2: oRAXhgwdaLc9wKVHqTLSmQB7I35D+32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS 
Date: Wed, 06 Jun 2018 09:10:29 GMT 
Content-Length: 0
```

## 请求示例：在URL中携带签名并上传加密对象<a name="section1859330175419"></a>

```
PUT /destobject?AccessKeyId=UI3SN1SRUQE14OYBKTZB&Expires=1534152518&x-obs-server-side-encryption=AES256&Signature=chvmG7%2FDA%2FDCQmTRJu3xngldJpg%3D HTTP/1.1 
User-Agent: curl/7.29.0 
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */* 
Date: Wed, 06 Jun 2018 09:10:29 GMT
```

## 响应示例：在URL中携带签名并上传加密对象<a name="section55941808545"></a>

```
HTTP/1.1 200 OK 
Server: OBS 
x-obs-request-id: BB78000001648480AF3900CED7F15155 
ETag: "d8bffdfbab5345d91ac05141789d2477" 
x-obs-server-side-encryption: AES256 
x-obs-id-2: oRAXhgwdaLc9wKVHqTLSmQB7I35D+32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS 
Date: Wed, 06 Jun 2018 09:10:29 GMT 
Content-Length: 0
```

