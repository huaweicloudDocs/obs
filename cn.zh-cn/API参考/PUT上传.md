# PUT上传<a name="obs_04_0080"></a>

## 功能介绍<a name="section5584184924715"></a>

用户在OBS系统中创建了桶之后，可以采用PUT操作的方式将对象上传到桶中。上传对象操作是指在指定的桶内增加一个对象，执行该操作需要用户拥有桶的写权限。

>![](public_sys-resources/icon-note.gif) **说明：** 
>同一个桶中存储的对象名是唯一的。

在桶未开启多版本的情况下，如果在指定的桶内已经有相同的对象键值的对象，用户上传的新对象会覆盖原来的对象；为了确保数据在传输过程中没有遭到破坏，用户可以在请求消息头中加入Content-MD5参数。在这种情况下，OBS收到上传的对象后，会对对象进行MD5校验，如果不一致则返回出错信息。

用户还可以在上传对象时指定x-obs-acl参数，设置对象的权限控制策略。如果匿名用户在上传对象时未指定x-obs-acl参数，则该对象默认可以被所有OBS用户访问。

该操作支持服务端加密功能。

单次上传对象大小范围是\[0, 5GB\]，如果需要上传超过5GB的大文件，需要通过[多段操作](多段操作.md)来分段上传。

OBS没有文件夹的概念。为了使用户更方便进行管理数据，OBS提供了一种方式模拟文件夹：通过在对象的名称中增加“/”，例如“test/123.jpg”。此时，“test”就被模拟成了一个文件夹，“123.jpg”则模拟成“test”文件夹下的文件名了，而实际上，对象名称（Key）仍然是“test/123.jpg”。此类命名方式的对象，在控制台上会以文件夹的形式展示。当您上传此类方式命名的对象时，如果其大小不为0，控制台上会展示为空文件夹，但是存储总用量为对象大小。

对象名中包含[特殊字符](https://support.huaweicloud.com/ugobs-obs/obs_41_0015.html)时需要进行URL编码，例如：\#obj需要编码为%23obj。

## 与POST上传的区别<a name="section9125142514612"></a>

PUT上传中参数通过请求头域传递；POST上传则作为消息体中的表单域传递。

PUT上传需在URL中指定对象名；POST上传提交的URL为桶域名，无需指定对象名。两者的请求行分别为：

```
PUT /ObjectName HTTP/1.1
```

```
POST / HTTP/1.1
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>使用PUT上传请求时，消息体中如果使用POST格式，则上传到OBS中的对象会以表单形式呈现。

关于POST上传的更多详细信息，请参考[POST上传](POST上传.md)。

## 多版本<a name="section27143284"></a>

如果桶的多版本状态是开启的，系统会自动为对象生成一个唯一的版本号，并且会在响应报头x-obs-version-id返回该版本号。如果桶的多版本状态是暂停的，则对象的版本号为**null**。关于桶的多版本状态，参见[设置桶的多版本状态](设置桶的多版本状态.md)。

## WORM<a name="section1475721115541"></a>

如果桶的WORM开关是开启的，则可以为对象配置WORM。您可以通过携带头域x-obs-object-lock-mode和x-obs-object-lock-retain-until-date在上传对象的同时指定对象的保护策略，如果您不携带这些头域，但配置了桶级默认WORM策略，则新上传的对象会自动应用默认策略。您还可以在上传后配置或修改对象级WORM保护策略。

>![](public_sys-resources/icon-note.gif) **说明：** 
>在桶的WORM开关开启时，系统会自动打开多版本功能。WORM保护是基于对象版本号的，配置WORM的版本受到WORM保护，没有配置WORM的版本可正常删除。例如，test.txt 001受到WORM保护。此时再次上传同名文件，产生新的对象版本test.txt 002，test.txt 002并未配置WORM，那么test.txt 002就不受保护可以正常删除。当您下载对象时，不指定版本号下载的是最新对象，也就是test.txt 002。

## 请求消息样式<a name="section42962965"></a>

```
PUT /ObjectName HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
Content-Type: application/xml 
Content-Length: length
Authorization: authorization
Date: date
<Optional Additional Header> 
<object Content>
```

## 请求消息参数<a name="section51122366"></a>

该请求消息中不使用参数。

## 请求消息头<a name="section57448112"></a>

该请求使用公共的消息头，具体请参见[表3](构造请求.md#table25197309)。该请求可以使用附加的消息头，具体如[表1](#table21799862)所示。

>![](public_sys-resources/icon-note.gif) **说明：** 
>OBS支持在上传对象时在请求里携带HTTP协议规定的6个请求头：Cache-Control、Expires、Content-Encoding、Content-Disposition、Content-Type、Content-Language。如果上传Object时设置了这些请求头，OBS会直接将这些头域的值保存下来。这6个值也可以通过OBS提供的修改对象元数据API接口进行修改。在该Object被下载或者HEAD的时候，这些保存的值将会被设置到对应的HTTP头域中返回客户端。

**表 1**  请求消息头

|**消息头名称**|**描述**|**是否必选**|
|--|--|--|
|Content-MD5|按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串。类型：String示例：n58IG6hfM7vqI4K0vnWpog==。|否|
|x-obs-acl|创建对象时，可以加上此消息头设置对象的权限控制策略，使用的策略为预定义的常用策略，包括：private；public-read；public-read-write（各策略详细说明见ACL章节的“使用头域设置ACL”）。类型：String说明：字符串形式的预定义策略。示例：x-obs-acl: public-read。|否|
|x-obs-grant-read|创建对象时，使用此头域授权租户下所有用户有读对象和获取对象元数据的权限。类型：String示例：x-obs-grant-read: id=domainID。如果授权给多个租户，需要通过“,”分割。|否|
|x-obs-grant-read-acp|创建对象时，使用此头域授权租户下所有用户有获取对象ACL的权限。类型：String示例：x-obs-grant-read-acp: id=domainID。如果授权给多个租户，需要通过“,”分割。|否|
|x-obs-grant-write-acp|创建对象时，使用此头域授权domain下所有用户有写对象ACL的权限。类型：String示例：x-obs-grant-write-acp: id=domainID。如果授权给多个租户，需要通过“,”分割。|否|
|x-obs-grant-full-control|创建对象时，使用此头域授权domain下所有用户有读对象、获取对象元数据、获取对象ACL、写对象ACL的权限。类型：String示例：x-obs-grant-full-control: id=domainID。如果授权给多个租户，需要通过“,”分割。|否|
|x-obs-storage-class|创建对象时，可以加上此头域设置对象的存储类型。如果未设置此头域，则以桶的默认存储类型作为对象的存储类型。类型：String说明：存储类型有4种：STANDARD（标准存储）、WARM（低频访问存储）、COLD（归档存储）、DEEP_ARCHIVE（深度归档存储）。因此这里可配置的值有：STANDARD、WARM和COLD、DEEP_ARCHIVE，注意大小写敏感。示例：x-obs-storage-class: STANDARD|否|
|x-obs-meta-*|创建对象时，可以在HTTP请求中加入以“x-obs-meta-”开头的消息头，用来加入自定义的元数据，以便对对象进行自定义管理。当用户获取此对象或查询此对象元数据时，加入的自定义元数据将会在返回消息的头中出现。更多说明详见对象自定义元数据介绍。类型：String示例：x-obs-meta-test: test metadata约束：自定义元数据key-value对都必须符合US-ASCII。|否|
|x-obs-persistent-headers|创建对象时，可以在HTTP请求中加入“x-obs-persistent-headers”消息头，用来加入一个或多个自定义的响应头，当用户获取此对象或查询此对象元数据时，加入的自定义响应头将会在返回消息的头域中出现。类型：String格式：x-obs-persistent-headers: key1:base64_encode(value1),key2:base64_encode(value2)....说明：其中key1/key2等为自定义header，如果含有非ASCII码或不可识别字符，可以采用URL编码或者Base64编码，服务端只会作为字符串处理，不会做解码。value1/value2等为对应自定义header的值，base64_encode指做base64编码，即将自定义header和对应值的base64编码作为一个key-value对用“:”连接，然后用“,”将所有的key-value对连接起来，放在x-obs-persistent-headers这个header中即可，服务端会对上传的value做解码处理。示例： x-obs-persistent-headers: key1:dmFsdWUx,key2:dmFsdWUy下载此对象或获取此对象元数据时：返回两个头域分别为“key1:value1”与“key2:value2”约束：通过该方式指定的自定义响应头不能以“x-obs-”为前缀，比如可以指定“key1”，但是不能指定“x-obs-key1”不能指定http标准头，例如host/content-md5/origin/range/Content-Disposition等此头域和自定义元数据总长度不能超过8KB如果传入相同key，将value以“,”拼接后放入同一个key中返回如果value解码后存在非US-ASCII值或不可识别字符，则服务端只会作为字符串处理并通过“?UTF-8?B?<(str)>?=”包装，而不会做解码，例如key1:abbc，会返回key1: =?UTF-8?B?abbc?=value不支持包含的字符“空格”、“=”、“,”、“;”、“:”、"."，如果需要包含，请使用URL编码或者Base64编码|否|
|x-obs-website-redirect-location|当桶设置了Website配置，可以将获取这个对象的请求重定向到桶内另一个对象或一个外部的URL，OBS将这个值从头域中取出，保存在对象的元数据中。例如，重定向请求到桶内另一对象：x-obs-website-redirect-location:/anotherPage.html或重定向请求到一个外部URL：x-obs-website-redirect-location:http://www.example.com/类型：String默认值：无约束：必须以“/”、“http://”或“https://”开头，长度不超过2KB。|否|
|x-obs-server-side-encryption|使用该头域表示服务端加密是SSE-KMS方式。类型：String示例：x-obs-server-side-encryption: kms|否。当使用SSE-KMS方式时，必选。|
|x-obs-server-side-data-encryption|SSE-KMS方式下使用该头域，该头域表示对象使用的数据加密算法，有效值为SM4。类型：String示例：x-obs-server-side-data-encryption：SM4|否|
|x-obs-server-side-encryption-kms-key-id|**参数描述：**此头域指定用哪一个密钥来加密对象。支持两种格式的描述方式：1. “regionID:domainID(租户ID):key/key_id”，其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是从数据加密服务密钥管理服务创建的密钥ID。 示例：x-obs-server-side-encryption-kms-key-id: cn-north-4:exampledomainid:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d02.“key_id”，key_id是从数据加密服务密钥管理服务创建的密钥ID。示例：x-obs-server-side-encryption-kms-key-id: 4f1cd4de-ab64-4807-920a-47fc42e7f0d0**约束限制：**当您设置了x-obs-server-side-encryption头域且赋值为“kms”，即选择kms加密方式时，才能使用该头域指定加密密钥。**默认值：**当您选择使用kms加密方式，但未设置此头域时，默认的主密钥将会被使用。如果默认主密钥不存在，系统将默认创建并使用。|否|
|x-obs-server-side-encryption-customer-algorithm|SSE-C方式下使用该头域，该头域表示加密使用的算法。类型：String示例：x-obs-server-side-encryption-customer-algorithm: AES256约束：需要和x-obs-server-side-encryption-customer-key， x-obs-server-side-encryption-customer-key-MD5一起使用。|否。当使用SSE-C方式时，必选|
|x-obs-server-side-encryption-customer-key|SSE-C方式下使用该头域，该头域表示加密使用的密钥。该密钥用于加密对象。类型：String示例：x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=约束：该头域由256-bit的密钥经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key-MD5一起使用。|否。当使用SSE-C方式时，必选。|
|x-obs-server-side-encryption-customer-key-MD5|SSE-C方式下使用该头域，该头域表示加密使用的密钥的MD5值。MD5值用于验证密钥传输过程中没有出错。类型：String示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==约束: 该头域由密钥的128-bit MD5值经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key一起使用。|否。当使用SSE-C方式时，必选。|
|success-action-redirect|此参数的值是一个URL，用于指定当此次请求操作成功响应后的重定向的地址。如果此参数值有效且操作成功，响应码为303，Location头域由此参数以及桶名、对象名、对象的ETag组成。如果此参数值无效，则OBS忽略此参数的作用，Location头域为对象地址，响应码根据操作成功或失败正常返回。类型：String|否|
|x-obs-expires|表示对象的过期时间，单位是天。过期之后对象会被自动删除。（从对象创建时间开始计算）此字段对于每个对象支持上传时配置，也支持后期通过修改元数据接口修改。类型：Integer示例：x-obs-expires:3|否|
|x-obs-object-lock-mode|要应用于此对象的WORM模式，目前仅支持COMPLIANCE，即合规模式，需要和x-obs-object-lock-retain-until-date一同使用。类型：String示例：x-obs-object-lock-mode:COMPLIANCE|否，携带x-obs-object-lock-retain-until-date头域时必带|
|x-obs-object-lock-retain-until-date|此对象的锁定过期的截止时间，格式要求为UTC时间，并符合ISO 8601标准。如：2015-07-01T04:11:15Z，需要和x-obs-object-lock-mode一同使用。类型：String示例：x-obs-object-lock-retain-until-date:2015-07-01T04:11:15Z|否，携带x-obs-object-lock-mode头域时必带|


## 请求消息元素<a name="section47270964"></a>

该请求消息中不使用消息元素，在消息体中带的是对象的数据。

## 响应消息样式<a name="section22785500"></a>

```
HTTP/1.1 status_code
Content-Length: length
Content-Type: type
```

## 响应消息头<a name="section3742912"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

除公共响应消息头之外，还可能使用如[表2](#table24122936102344)中的消息头。

**表 2**  附加响应消息头

|消息头名称|描述|
|--|--|
|x-obs-version-id|对象的版本号。如果桶的多版本状态为开启，则会返回对象的版本号。类型：String|
|x-obs-server-side-encryption|如果服务端加密是SSE-KMS方式，响应包含该头域。类型：String示例：x-obs-server-side-encryption:kms|
|x-obs-server-side-encryption-kms-key-id|如果服务端加密是SSE-KMS方式，响应包含该头域，该头域表示主密钥。类型：String格式为： regionID:domainID(租户ID):key/key_id其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是本次加密使用的密钥ID。示例： x-obs-server-side-encryption-kms-key-id:cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0|
|x-obs-server-side-encryption-customer-algorithm|如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的算法。类型：String示例：x-obs-server-side-encryption-customer-algorithm: AES256|
|x-obs-server-side-encryption-customer-key-MD5|如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的密钥的MD5值。类型：String示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==|
|x-obs-storage-class|对象为非标准存储对象时，会返回此头域，可取值为：WARM或者COLD、DEEP_ARCHIVE类型：String|


## 响应消息元素<a name="section33686208"></a>

该请求的响应消息不带消息元素。

## 错误响应消息<a name="section34740423"></a>

该请求的返回无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例：上传对象<a name="section14482163815396"></a>

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:11:15 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例：上传对象<a name="section11653102613112"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF2600000164364C10805D385E1E3C67
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: 32AAAWJAMAABAAAQAAEAABAAAQAAEAABCTzu4Jp2lquWuXsjnLyPPiT3cfGhqPoY
Date: WED, 01 Jul 2015 04:11:15 GMT
Content-Length: 0
```

## 请求示例：上传对象的同时设置ACL<a name="section9978114711117"></a>

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:13:55 GMT
x-obs-grant-read:id=52f24s3593as5730ea4f722483579ai7,id=a93fcas852f24s3596ea8366794f7224
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例：上传对象的同时设置ACL<a name="section17245101261216"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164845759E4F3B39ABEE55E
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSReVRNuas0knI+Y96iXrZA7BLUgj06Z
Date: WED, 01 Jul 2015 04:13:55 GMT
Content-Length: 0
```

## 请求示例：桶开启多版本时上传对象<a name="section18923277137"></a>

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-storage-class: WARM
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例：桶开启多版本时上传对象<a name="section16530173215133"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
ETag: "d41d8cd98f00b204e9800998ecf8427e"
X-OBS-ID-2: GcVgfeOJHx8JZHTHrRqkPsbKdB583fYbr3RBbHT6mMrBstReVILBZbMAdLiBYy1l
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
Content-Length: 0
```

## 请求示例：上传对象时携带MD5<a name="section17724204519133"></a>

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:17:50 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10
Content-MD5: 6Afx/PgtEy+bsBjKZzihnw==
Expect: 100-continue

1234567890
```

## 响应示例：上传对象时携带MD5<a name="section3283216161415"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164B165971F91D82217D105
X-OBS-ID-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSEKhBpS4BB3dSMNqMtuNxQDD9XvOw5h
ETag: "1072e1b96b47d7ec859710068aa70d57"
Date: WED, 01 Jul 2015 04:17:50 GMT
Content-Length: 0
```

## 请求示例：上传时配置website实现下载对象重定向<a name="section2272113211413"></a>

**当桶设置了Website配置，您可以在上传对象时进行以下设置，设置后用户在下载对象时会重定向**

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-website-redirect-location: http://www.example.com/
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例：上传时配置website实现下载对象重定向<a name="section632052520159"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTmxB5ufMj/7/GzP8TFwTbp33u0xhn2Z
ETag: "1072e1b96b47d7ec859710068aa70d57"
Date: WED, 01 Jul 2015 04:17:12 GMT
x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
Content-Length: 0
```

## 请求示例：在URL中携带签名并上传对象<a name="section9838237181513"></a>

```
PUT /object02?AccessKeyId=H4IPJX0TQTHTHEBQQCEC&Expires=1532688887&Signature=EQmDuOhaLUrzrzRNZxwS72CXeXM%3D HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Content-Length: 1024

[1024 Byte data content]
```

## 响应示例：在URL中携带签名并上传对象<a name="section96529021618"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTmxB5ufMj/7/GzP8TFwTbp33u0xhn2Z
ETag: "1072e1b96b47d7ec859710068aa70d57"
Date: Fri, 27 Jul 2018 10:52:31 GMT
x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
Content-Length: 0
```

## 请求示例：上传指定存储类型的对象<a name="section74231427201219"></a>

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:15:07 GMT
x-obs-storage-class: WARM
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
Content-Length: 10240
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例：上传指定存储类型的对象<a name="section1526805513128"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BB7800000164846A2112F98BF970AA7E
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: a39E0UgAIAABAAAQAAEAABAAAQAAEAABCTPOUJu5XlNyU32fvKjM/92MQZK2gtoB
Date: WED, 01 Jul 2015 04:15:07 GMT
Content-Length: 0
```

## 请求示例：上传时配置对象级WORM保护策略<a name="section66011687493"></a>

```
PUT /object01 HTTP/1.1
User-Agent: curl/7.29.0
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept: */*
Date: WED, 01 Jul 2015 04:11:15 GMT
Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
Content-Length: 10240
x-obs-object-lock-mode:COMPLIANCE
x-obs-object-lock-retain-until-date:2022-09-24T16:10:25Z
Expect: 100-continue

[1024 Byte data content]
```

## 响应示例 ：上传时配置对象级WORM保护策略<a name="section1848934125211"></a>

```
HTTP/1.1 200 OK
Server: OBS
x-obs-request-id: BF2600000164364C10805D385E1E3C67
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-id-2: 32AAAWJAMAABAAAQAAEAABAAAQAAEAABCTzu4Jp2lquWuXsjnLyPPiT3cfGhqPoY
Date: WED, 01 Jul 2015 04:11:15 GMT
Content-Length: 0
```

