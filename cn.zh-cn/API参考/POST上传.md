# POST上传<a name="obs_04_0081"></a>

## 功能介绍<a name="section1534875573"></a>

上传对象操作是指在指定的桶内增加一个对象，执行该操作需要用户拥有桶的写权限。

>![](public_sys-resources/icon-note.gif) **说明：** 
>同一个桶中存储的对象名是唯一的。

在桶未开启多版本的情况下，如果在指定的桶内已经有相同的对象键值的对象，用户上传的新对象会覆盖原来的对象；为了确保数据在传输过程中没有遭到破坏，用户可以在表单域中加入Content-MD5参数。在这种情况下，OBS收到上传的对象后，会对对象进行MD5校验，如果不一致则返回出错信息。用户还可以在上传对象时指定x-obs-acl参数，设置对象的权限控制策略。

用户除了可以用PUT直接上传对象外，还可以使用POST上传对象。

单次上传对象大小范围是\[0, 5GB\]，如果需要上传超过5GB的大文件，需要通过[多段操作](多段操作.md)来分段上传。

该操作支持服务端加密功能。

## 与PUT上传的区别<a name="section9125142514612"></a>

PUT上传中参数通过请求头域传递；POST上传则作为消息体中的表单域传递。

PUT上传需在URL中指定对象名；POST上传提交的URL为桶域名，无需指定对象名。两者的请求行分别为：

```
PUT /ObjectName HTTP/1.1
```

```
POST / HTTP/1.1
```

关于PUT上传的更多详细信息，请参考[PUT上传](PUT上传.md)。

## 多版本<a name="section28789840"></a>

如果桶的多版本状态是开启的，系统会自动为对象生成一个唯一的版本号；如果桶的多版本状态是暂停的，则系统生成的对象版本号为**null**，并由响应报头x-obs-version-id返回该版本号。关于桶的多版本状态，参见[设置桶的多版本状态](设置桶的多版本状态.md)。

## WORM<a name="section1475721115541"></a>

如果桶的WORM开关是开启的，则可以为对象配置WORM。您可以通过携带元素x-obs-object-lock-mode和x-obs-object-lock-retain-until-date在上传对象的同时指定对象的保护策略，如果您不携带这些元素，但配置了桶级默认WORM策略，则新上传的对象会自动应用默认策略。您还可以在上传后配置或修改对象级WORM保护策略。

>![](public_sys-resources/icon-note.gif) **说明：** 
>在桶的WORM开关开启时，系统会自动打开多版本功能。WORM保护是基于对象版本号的，配置WORM的版本受到WORM保护，没有配置WORM的版本可正常删除。例如，test.txt 001受到WORM保护。此时再次上传同名文件，产生新的对象版本test.txt 002，test.txt 002并未配置WORM，那么test.txt 002就不受保护可以正常删除。当您下载对象时，不指定版本号下载的是最新对象，也就是test.txt 002。

## 请求消息样式<a name="section57781973"></a>

```
POST / HTTP/1.1 
Host: bucketname.obs.cn-north-4.myhuaweicloud.com 
User-Agent: browser_data
Accept: file_types
Accept-Language: Regions
Accept-Encoding: encoding
Accept-Charset: character_set
Keep-Alive: 300 
Connection: keep-alive 
Content-Type: multipart/form-data; boundary=9431149156168 
Content-Length: length


--9431149156168 
Content-Disposition: form-data; name="key" 

acl 
--9431149156168 
Content-Disposition: form-data; name="success_action_redirect"
 
success_redirect 
--9431149156168 
Content-Disposition: form-data; name="content-Type" 

content_type 
--9431149156168 
Content-Disposition: form-data; name="x-obs-meta-uuid" 

uuid 
--9431149156168 
Content-Disposition: form-data; name="x-obs-meta-tag" 

metadata 
--9431149156168 
Content-Disposition: form-data; name="AccessKeyId" 

access-key-id 
--9431149156168 
Content-Disposition: form-data; name="policy" 

encoded_policy 
--9431149156168 
Content-Disposition: form-data; name="signature" 

signature= 
--9431149156168 
Content-Disposition: form-data; name="file"; filename="MyFilename" 
Content-Type: image/jpeg 

file_content 
--9431149156168 
Content-Disposition: form-data; name="submit" 

Upload to OBS 
--9431149156168--
```

## 请求消息参数<a name="section50275709"></a>

该请求消息中不使用参数。

## 请求消息头<a name="section49828203"></a>

该请求使用公共的消息头，具体请参见[表3](构造请求.md#table25197309)。

如果想要获取CORS配置信息，则需要使用的消息头如下[表1](#table45572552212656)所示。

**表 1**  获取CORS配置的请求消息头

|消息头名称|描述|是否必选|
|--|--|--|
|Origin|预请求指定的跨域请求Origin（通常为域名）。类型：String|是|
|Access-Control-Request-Headers|实际请求可以带的HTTP头域，可以带多个头域。类型：String|否|


>![](public_sys-resources/icon-note.gif) **说明：** 
>配置后如果仍然提示跨域，请参考[为什么配置了跨域资源共享（CORS）仍然报错](https://support.huaweicloud.com/obs_faq/obs_faq_0163.html)处理。

## 请求消息元素<a name="section45800647"></a>

该请求消息的消息元素以表单形式组织，表单字段的具体含义如[表2](#table13225554)所示。

**表 2**  请求消息表单元素

|**参数名称**|**描述**|是否必选|
|--|--|--|
|file|上传的对象内容。文件名与文件路径均会被忽略，不会作为对象名称。对象名称是另一参数key的值。类型：二进制或文本类型。约束条件：此参数必须为最后一个参数，否则此参数之后的参数会被丢弃；一个请求中只能含有一个file参数。|是|
|key|通过此请求创建的对象名称。类型：String|是|
|AccessKeyId|用来指明请求发起者的Access Key。类型：String约束条件：如果该请求包括安全策略参数policy或signature时，则必须包括此参数。|是，有条件|
|policy|该请求的安全策略描述。policy格式请参考基于浏览器上传的表单中携带签名章节中policy格式类型：String限制：当Bucket提供了AccessKeyId(或signature)表单域时，则必须包括此参数。|是，有条件|
|signature|根据StringToSign计算出的签名字符串。类型：String限制：当Bucket提供了AccessKeyId(或policy)表单域时，则必须包括此参数。|是，有条件|
|token|用来统一指明请求发起者的Access Key，请求签名和请求的安全策略。token的优先级高于单独指定的Access Key，请求签名和请求的安全策略。类型：String示例：HTML中：<input type="text" name="token" value="ak:signature:policy" />|否|
|x-obs-acl|创建对象时，可以加上此消息头设置对象的权限控制策略，使用的策略为预定义的常用策略，包括：private；public-read；public-read-write；public-read-delivered ; public-read-write-delivered（各策略详细说明见ACL章节的“使用头域设置ACL”）。类型：String示例：POLICY中：{"acl": "public-read" },HTML中：<input type="text" name="acl" value="public-read" />|否|
|x-obs-grant-read|创建对象时，使用此头域授权domain下所有用户有读对象和获取对象元数据的权限。类型：String示例：POLICY中：{"grant-read": "id=domainId1" },HTML中：<input type="text" name="grant-read" value="id=domainId1" />|否|
|x-obs-grant-read-acp|创建对象时，使用此头域授权domain下所有用户有获取对象ACL的权限。类型：String示例：POLICY中：{"grant-read-acp": "id=domainId1" },HTML中：<input type="text" name="grant-read-acp" value="id=domainId1" />|否|
|x-obs-grant-write-acp|创建对象时，使用此头域授权domain下所有用户有写对象ACL的权限。类型：String示例：POLICY中：{"grant-write-acp": "id=domainId1" },HTML中：<input type="text" name="grant-write-acp" value="id=domainId1" />|否|
|x-obs-grant-full-control|创建对象时，使用此头域授权domain下所有用户有读对象、获取对象元数据、获取对象ACL、写对象ACL的权限。类型：String示例：POLICY中：{"grant-full-control": "id=domainId1" },HTML中：<input type="text" name="grant-full-control" value="id=domainId1" />|否|
|x-obs-storage-class|创建对象时，可以加上此头域设置对象的存储类型。如果未设置此头域，则以桶的默认存储类型作为对象的存储类型。类型：String说明：存储类型有4种：STANDARD（标准存储）、WARM（低频访问存储）、COLD（归档存储）、DEEP_ARCHIVE（深度归档存储）。因此这里可配置的值有：STANDARD、WARM和COLD、DEEP_ARCHIVE，注意大小写敏感。示例：POLICY中：{"storage-class": "STANDARD" },HTML中：<input type="text" name="x-obs-storage-class" value="STANDARD" />|否|
|Cache-Control,Content-Type,Content-Disposition,Content-EncodingExpires|这5个参数是HTTP标准消息头，OBS将这些参数记录下来，当用户下载此对象或Head Object时，在响应消息头中携带这些参数。类型：String示例：POLICY中：["starts-with", "$Content-Type", "text/"],HTML中：<input type="text" name="content-type" value="text/plain" />|否|
|success_action_redirect|此参数的值是一个URL，用于指定当此次请求操作成功响应后的重定向的地址。如果此参数值有效且操作成功，响应码为303，Location头域由此参数以及桶名、对象名、对象的ETag组成。如果此参数值无效，则OBS忽略此参数的作用，Location头域为对象地址，响应码根据操作成功或失败正常返回。类型：String示例：POLICY中：{"success_action_redirect": "http://123458.com"},HTML中：<input type="text" name="success_action_redirect" value="http://123458.com" />|否|
|x-obs-meta-*|创建对象时，可以在HTTP请求中加入“x-obs-meta-”消息头或以“x-obs-meta-”开头的消息头，用来加入自定义的元数据，以便对对象进行自定义管理。当用户获取此对象或查询此对象元数据时，加入的自定义元数据将会在返回消息的消息头中出现。更多说明详见对象自定义元数据介绍。类型：String示例：POLICY中：{" x-obs-meta-test ": " test metadata " },HTML中：<input type="text" name=" x-obs-meta-test " value=" test metadata " />|否|
|x-obs-persistent-headers|创建对象时，可以在HTTP请求中加入“x-obs-persistent-headers”消息头，用来加入一个或多个自定义的响应头，当用户获取此对象或查询此对象元数据时，加入的自定义响应头将会在返回消息的头域中出现。类型：String格式：x-obs-persistent-headers: key1:base64_encode(value1),key2:base64_encode(value2)....说明：其中key1/key2等为自定义header，如果含有非ASCII码或不可识别字符，可以采用URL编码或者Base64编码，服务端只会作为字符串处理，不会做解码。value1/value2等为对应自定义header的值，base64_encode指做base64编码，即将自定义header和对应值的base64编码作为一个key-value对用“:”连接，然后用“,”将所有的key-value对连接起来，放在x-obs-persistent-headers这个header中即可，服务端会对上传的value做解码处理。示例：POLICY中：{"x-obs-persistent-headers": "key1:dmFsdWUx,key2:dmFsdWUy" },HTML中：<input type="text" name="x-obs-persistent-headers" value="key1:dmFsdWUx,key2:dmFsdWUy" />下载此对象或获取此对象元数据时：返回两个头域分别为“key1:value1”与“key2:value2”约束：通过该方式指定的自定义响应头不能以“x-obs-”为前缀，比如可以指定“key1”，但是不能指定“x-obs-key1”不能指定http标准头，例如host/content-md5/origin/range/Content-Disposition等此头域和自定义元数据总长度不能超过8KB如果传入相同key，将value以“,”拼接后放入同一个key中返回如果value解码后存在非US-ASCII值或不可识别字符，则服务端只会作为字符串处理并通过“?UTF-8?B?<(str)>?=”包装，而不会做解码，例如key1:abbc，会返回key1: =?UTF-8?B?abbc?=value不支持包含的字符“空格”、“=”、“,”、“;”、“:”、"."，如果需要包含，请使用URL编码或者Base64编码|否|
|success_action_status|这个参数指定成功响应的状态码，允许设定的值为200，201，204。如果此参数值被设定为200或204，OBS响应消息中body为空。如果此参数值被设定为201，则OBS响应消息中包含一个XML文档描述此次请求的响应。当请求不携带此参数或参数无效时，OBS响应码为204。类型：String示例：POLICY中：["starts-with", "$success_action_status", ""],HTML中：<input type="text" name="success_action_status" value="200" />|否|
|x-obs-website-redirect-location|当桶设置了Website配置，可以将获取这个对象的请求重定向到桶内另一个对象或一个外部的URL，OBS将这个值从头域中取出，保存在对象的元数据中。默认值：无约束：必须以“/”、“http://”或“https://”开头，长度不超过2K。|否|
|x-obs-server-side-encryption|使用该头域表示服务端加密是SSE-KMS方式。类型：String示例：x-obs-server-side-encryption：kms|否。当使用SSE-KMS方式时，必选。|
|x-obs-server-side-data-encryption|SSE-KMS方式下使用该头域，该头域表示对象使用的数据加密算法，有效值为SM4。类型：String示例：x-obs-server-side-data-encryption：SM4|否|
|x-obs-server-side-encryption-kms-key-id|SSE-KMS方式下使用该头域，该头域表示主密钥，如果用户没有提供该头域，那么默认的主密钥将会被使用。如果默认主密钥不存在，将默认创建并使用。类型：String支持两种格式的描述方式：1. regionID:domainID(租户ID):key/key_id或者2.key_id其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是从数据加密服务创建的密钥ID。示例：1. x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0  或者2. x-obs-server-side-encryption-kms-key-id：4f1cd4de-ab64-4807-920a-47fc42e7f0d0|否|
|x-obs-server-side-encryption-customer-algorithm|SSE-C方式下使用该头域，该头域表示加密使用的算法。类型：String示例：x-obs-server-side-encryption-customer-algorithm：AES256约束：需要和x-obs-server-side-encryption-customer-key， x-obs-server-side-encryption-customer-key-MD5一起使用。|否。当使用SSE-C方式时，必选。|
|x-obs-server-side-encryption-customer-key|SSE-C方式下使用该头域，该头域表示加密使用的密钥。该密钥用于加密对象。类型：String示例：x-obs-server-side-encryption-customer-key:K7QkYpBkM5+hca27fsNkUnNVaobncnLht/rCB2o/9Cw=约束：该头域由256-bit的密钥经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key-MD5一起使用。|否。当使用SSE-C方式时，必选。|
|x-obs-server-side-encryption-customer-key-MD5|SSE-C方式下使用该头域，该头域表示加密使用的密钥的MD5值。MD5值用于验证密钥传输过程中没有出错。类型：String示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==约束: 该头域由密钥的128-bit MD5值经过base64-encoded得到，需要和x-obs-server-side-encryption-customer-algorithm，x-obs-server-side-encryption-customer-key一起使用。|否。当使用SSE-C方式时，必选。|
|x-obs-expires|表示对象的过期时间，单位是天。过期之后对象会被自动删除。（从对象最后修改时间开始计算）类型：Integer示例：x-obs-expires:3|否|
|x-obs-object-lock-mode|要应用于此对象的WORM模式，目前仅支持COMPLIANCE，即合规模式，需要和x-obs-object-lock-retain-until-date一同使用。类型：String示例：x-obs-object-lock-mode:COMPLIANCE|否, 携带x-obs-object-lock-retain-until-date时必带。|
|x-obs-object-lock-retain-until-date|此对象的锁定过期的截止时间，格式要求为UTC时间，并符合ISO 8601标准。如：2015-07-01T04:11:15Z，需要和x-obs-object-lock-mode一同使用。类型：String示例：x-obs-object-lock-retain-until-date:2015-07-01T04:11:15Z|否，携带x-obs-object-lock-mode时必带。|


## 响应消息样式<a name="section9552642"></a>

```
HTTP/1.1 status_code
Content-Type: application/xml 
Location: location
Date: date
ETag: etag
```

## 响应消息头<a name="section18864917"></a>

该请求的响应消息使用公共消息头，具体请参考[表1](返回结果.md#d0e686)。

除公共响应消息头之外，还可能使用如[表3](#table35215532173747)中的消息头。

**表 3**  附加响应消息头

|消息头名称|描述|
|--|--|
|x-obs-version-id|对象的版本号。如果桶的多版本状态为开启，则会返回对象的版本号。如果桶的多版本状态为暂停，则会返回**null**。类型：String|
|Access-Control-Allow-Origin|当桶设置了CORS配置，如果请求的Origin满足服务端的CORS配置，则在响应中包含这个Origin。类型：String|
|Access-Control-Allow-Headers|当桶设置了CORS配置，如果请求的headers满足服务端的CORS配置，则在响应中包含这个headers。类型：String|
|Access-Control-Max-Age|当桶设置了CORS配置，服务端CORS配置中的MaxAgeSeconds。类型：Integer|
|Access-Control-Allow-Methods|当桶设置了CORS配置，如果请求的Access-Control-Request-Method满足服务端的CORS配置，则在响应中包含这条rule中的Methods。类型：String有效值：GET、PUT、HEAD、POST 、DELETE|
|Access-Control-Expose-Headers|当桶设置了CORS配置，服务端CORS配置中的ExposeHeader。类型：String|
|x-obs-server-side-encryption|如果服务端加密是SSE-KMS方式，响应包含该头域。类型：String示例：x-obs-server-side-encryption：kms|
|x-obs-server-side-encryption-kms-key-id|如果服务端加密是SSE-KMS方式，响应包含该头域，该头域表示主密钥。类型：String格式为： regionID:domainID(租户ID):key/key_id其中regionID是使用密钥所属region的ID；domainID是使用密钥所属租户的租户ID；key_id是本次加密使用的密钥ID。示例： x-obs-server-side-encryption-kms-key-id：cn-north-4:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0|
|x-obs-server-side-encryption-customer-algorithm|如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的算法。类型：String示例：x-obs-server-side-encryption-customer-algorithm：AES256|
|x-obs-server-side-encryption-customer-key-MD5|如果服务端加密是SSE-C方式，响应包含该头域，该头域表示加密使用的密钥的MD5值。类型：String示例：x-obs-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==|


## 响应消息元素<a name="section35566529"></a>

该请求的响应消息中不带消息元素。

## 错误响应消息<a name="section51663312"></a>

无特殊错误，所有错误已经包含在[表2](错误码.md#d0e843)中。

## 请求示例：普通POST上传<a name="section14482163815396"></a>

```
POST / HTTP/1.1
Date: WED, 01 Jul 2015 04:15:23 GMT
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Content-Type: multipart/form-data; boundary=7db143f50da2
Content-Length: 2424
Origin: www.example.com
Access-Control-Request-Headers:acc_header_1

--7db143f50da2
Content-Disposition: form-data; name="key"

object01
--7db143f50da2
Content-Disposition: form-data; name="acl"

public-read
--7db143f50da2 
Content-Disposition: form-data; name="content-type"

text/plain
--7db143f50da2
Content-Disposition: form-data; name="expires"

WED, 01 Jul 2015 04:16:15 GMT
--7db143f50da2
Content-Disposition: form-data; name="AccessKeyId"

14RZT432N80TGDF2Y2G2
--7db143f50da2
Content-Disposition: form-data; name="policy"

ew0KICAiZXhaaXJhdGlvbiI6ICIyMDE1LTA3LTAxVDEyOjAwOjAwLjAwMFoiLA0KICAiY29uZGl0aW9ucyI6IFsNCiAgICB7ImJ1Y2tldCI6ICJleG1hcGxlYnVja2V0IiB9LA0KICAgIHsiYWNsIjogInB1YmxpYy1yZWFkIiB9LA0KICAgIHsiRXhaaXJlcyI6ICIxMDAwIiB9LA0KICAgIFsiZXEiLCAiJGtleSIsICJvYmplY3QwMSJdLA0KICAgIFsic3RhcnRzLXdpdGgiLCAiJENvbnRlbnQtVHlwZSIsICJ0ZXh0LyJdLA0KICBdDQp9DQo=
--7db143f50da2
Content-Disposition: form-data; name="signature"

Vk6rwO0Nq09BLhvNSIYwSJTRQ+k=
--7db143f50da2
Content-Disposition: form-data; name="x-obs-persistent-headers"
 
test:dmFsdWUx
--7db143f50da2
Content-Disposition: form-data; name="x-obs-grant-read"
 
id=52f24s3593as5730ea4f722483579xxx
--7db143f50da2
Content-Disposition: form-data; name="x-obs-server-side-encryption"
 
kms
--7db143f50da2
Content-Disposition: form-data; name="x-obs-website-redirect-location"
 
http://www.example.com/
--7db143f50da2
Content-Disposition: form-data; name="file"; filename="C:\Testtools\UpLoadFiles\object\1024Bytes.txt"
Content-Type: text/plain

01234567890
--7db143f50da2
Content-Disposition: form-data; name="submit"

Upload
--7db143f50da2--
```

## 响应示例：普通POST上传<a name="section76081155815"></a>

桶配置cors后，响应会包含Access-Control-\*的信息。

```
HTTP/1.1 204 No Content
x-obs-request-id: 90E2BA00C26C00000133B442A90063FD
x-obs-id-2: OTBFMkJBMDBDMjZDMDAwMDAxMzNCNDQyQTkwMDYzRkRBQUFBQUFBQWJiYmJiYmJi
Access-Control-Allow-Origin: www.example.com
Access-Control-Allow-Methods: POST,GET,HEAD,PUT
Access-Control-Allow-Headers: acc_header_01
Access-Control-Max-Age: 100
Access-Control-Expose-Headers: exp_header_01
Content-Type: text/xml
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/object01
Date: WED, 01 Jul 2015 04:15:23 GMT
ETag: "ab7abb0da4bca5323ab6119bb5dcd296"
```

## 请求示例：带x-obs-acl头域并指定存储类型<a name="section392181218378"></a>

**带x-obs-acl头域并指定存储类型，重定向头域，上传对象**

编码前，policy的内容为

```
{
    "expiration":"2018-07-17T04:54:35Z",
    "conditions":[
        {
            "content-type":"text/plain"
        },
        {
            "x-obs-storage-class":"WARM"
        },
        {
            "success_action_redirect":"http://www.example.com"
        },
        {
            "x-obs-acl":"public-read"
        },
        [
            "starts-with",
            "$bucket",
            ""
        ],
        [
            "starts-with",
            "$key",
            ""
        ]
    ]
}
```

请求示例：

```
POST / HTTP/1.1
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
Accept-Encoding: identity
Content-Length: 947
Content-Type: multipart/form-data; boundary=9431149156168
User-Agent: OBS/Test

--9431149156168
Content-Disposition: form-data; name="x-obs-acl"

public-read
--9431149156168
Content-Disposition: form-data; name="AccessKeyId"

H4IPJX0TQTHTHEBQQCEC
--9431149156168
Content-Disposition: form-data; name="key"

my-obs-object-key-demo
--9431149156168
Content-Disposition: form-data; name="signature"

WNwv8P1ZiWdqPQqjXeLmAfzPDAI=
--9431149156168
Content-Disposition: form-data; name="policy"

eyJleHBpcmF0aW9uIjoiMjAxOC0wNy0xN1QwODozNDoyM1oiLCAiY29uZGl0aW9ucyI6W3siY29udGVudC10eXBlIjoidGV4dC9wbGFpbiJ9LHsieC1vYnMtYWNsIjoicHVibGljLXJlYWQifSxbInN0YXJ0cy13aXRoIiwgIiRidWNrZXQiLCAiIl0sWyJzdGFydHMtd2l0aCIsICIka2V5IiwgIiJdXX0=
--9431149156168
Content-Disposition: form-data; name="content-type"

text/plain
--9431149156168
Content-Disposition: form-data; name="file"; filename="myfile"
Content-Type: text/plain

c2c6cd0f-898e-11e8-aab6-e567c91fb541
52b8e8a0-8481-4696-96f3-910635215a78

--9431149156168--
```

## 响应示例：带x-obs-acl头域并指定存储类型<a name="section1999141253715"></a>

```
HTTP/1.1 204 No Content
Server: OBS
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/my-obs-object-key-demo
ETag: "17a83fc8d431273405bd266114b7e034"
x-obs-request-id: 5DEB00000164A728A7C7F4E032214CFA
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSwj2PcBE0YcoLHUDO7GSj+rVByzjflA
Date: Tue, 17 Jul 2018 07:33:36 GMT
```

## 请求示例：使用token进行鉴权<a name="section430011014337"></a>

```
POST / HTTP/1.1
Content-Type:multipart/form-data; boundary=9431149156168
Content-Length: 634
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com
 
--9431149156168
Content-Disposition: form-data; name="key"
obj01
 
--9431149156168
Content-Disposition: form-data; name="token"
UDSIAMSTUBTEST002538:XsVcTzR2/A284oE4VH9qPndGcuE=:eyJjb25kaXRpb25zIjogW3siYnVja2V0IjogInRlc3QzMDAzMDU4NzE2NjI2ODkzNjcuMTIifSwgeyJDb250ZW50LVR5cGUiOiAiYXBwbGljYXRpb24veG1sIn0sIFsiZXEiLCAiJGtleSIsICJvYmoudHh0Il1dLCAiZXhwaXJhdGlvbiI6ICIyMDIyLTA5LTA5VDEyOjA5OjI3WiJ9
 
--9431149156168
Content-Disposition: form-data; name="file"; filename="myfile"
Content-Type: text/plain
01234567890
 
--9431149156168--
Content-Disposition: form-data; name="submit"
Upload to OBS
```

## 响应示例：使用token进行鉴权<a name="section47211218103213"></a>

```
HTTP/1.1 204 No Content
Server: OBS
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/my-obs-object-key-demo
ETag: "7eda50a430fed940023acb9c4c6a2fff"
x-obs-request-id: 000001832010443D80F30B649B969C47
x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCTj0yO9KJd5In+i9pzTgCDVG9vMnk7O/
Date: Fri,09Sep 2022 02: 24:40 GMT
```

## 请求示例：设置对象过期时间<a name="section29219401538"></a>

```
POST / HTTP/1.1 
Date: WED, 01 Jul 2015 04:15:23 GMT 
Host: examplebucket.obs.cn-north-4.myhuaweicloud.com 
Content-Type: multipart/form-data; boundary=148828969260233905620870
Content-Length: 1639 
Origin: www.example.com 
Access-Control-Request-Headers:acc_header_1 
 
--148828969260233905620870 
Content-Disposition: form-data; name="key" 
 
object01
--148828969260233905620870
Content-Disposition: form-data; name="ObsAccessKeyId"
 
55445349414d5354554254455354303030303033
--148828969260233905620870
Content-Disposition: form-data; name="signature"
 
396246666f6f42793872792f7a3958524f6c44334e4e69763950553d--7db143f50da2 
--148828969260233905620870
Content-Disposition: form-data; name="policy" 
 
65794a6c65484270636d463061573975496a6f694d6a41794d7930774e6930784e565178...
--148828969260233905620870
Content-Disposition: form-data; name="x-obs-expires"
 
4
--148828969260233905620870
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain 
 
01234567890
--148828969260233905620870
Content-Disposition: form-data; name="submit" 
 
Upload 
--148828969260233905620870--
```

## 响应示例：设置对象过期时间<a name="section179615402535"></a>

```
 
HTTP/1.1 204 No Content 
Server: OBS 
Date: Thu, 15 Jun 2023 12:39:03 GMT
Connection: keep-alive
Location: http://examplebucket.obs.cn-north-4.myhuaweicloud.com/my-obs-object-key-demo 
x-obs-expiration: expiry-date="Tue, 20 Jun 2023 00:00:00 GMT"
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-request-id: 00000188BF11049553064911000FC30D
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSwj2PcBE0YcoLHUDO7GSj+rVByzjflA 
x-forward-status: 0x40020000000001
x-dae-api-type: REST.POST.OBJECT
```

## 请求示例：指定状态码<a name="section199604065313"></a>

**指定成功响应的状态码为200**

```
POST /srcbucket HTTP/1.1
User-Agent: PostmanRuntime/7.26.8
Accept: */*
Postman-Token: 667dcc44-1c48-41ba-9e41-9f87d8975089
Host: obs.cn-north-4.myhuaweicloud.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: multipart/form-data; boundary=--------------------------285613759795901770404350
Content-Length: 1134
 
----------------------------285613759795901770404350
Content-Disposition: form-data; name="key"
 
obj
----------------------------285613759795901770404350
Content-Disposition: form-data; name="ObsAccessKeyId"
 
XXXXXXXXXXXXXXX000003
----------------------------285613759795901770404350
Content-Disposition: form-data; name="signature"
 
9rc4bVhDPQ7eHtw17hWtYxLnBWU=
----------------------------285613759795901770404350
Content-Disposition: form-data; name="policy"
 
eyJleHBpcmF0aW9uIjoiMjAyMy0wNi0xNVQxNDoxMTozNFoiLCAiY29uZGl0aW9ucyI6W3siYnVja2V0Ijoic3JjYnVja2V0MiJ9LHsic3VjY2Vzc19hY3Rpb25fc3RhdHVzIjoiMjAwIn0seyJjb250ZW50LXR5cGUiOiJ0ZXh0L3BsYWluIn0seyJrZXkiOiIzMzMifSxdfQ==
----------------------------285613759795901770404350
Content-Disposition: form-data; name="success_action_status"
 
200
----------------------------285613759795901770404350
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain
 
 
----------------------------285613759795901770404350
Content-Disposition: form-data; name="submit"
 
Upload to OBS
----------------------------285613759795901770404350--
```

## 响应示例：指定状态码<a name="section299114025312"></a>

**指定成功响应的状态码为200，响应消息**

```
HTTP/1.1 200 OK
Server: OBS
Date: Thu, 15 Jun 2023 13:12:51 GMT
Content-Length: 0
Connection: keep-alive
Location: http://obs.cn-north-4.myhuaweicloud.com/srcbucket/obj
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-request-id: 00000188BF2FF55F5306426E000FE366
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCScDjcXgZ7oMYSVnZnk4+HrClVwLVPTi
x-forward-status: 0x40020000000001
x-dae-api-type: REST.POST.OBJECT
```

## 请求示例：上传时配置对象级WORM保护策略<a name="section1299154075311"></a>

```
POST /srcbucket HTTP/1.1
User-Agent: PostmanRuntime/7.26.8
Accept: */*
Postman-Token: 4c2f4c7e-2e0b-46c0-b1a7-4a5da560b6a1
Host: obs.cn-north-4.myhuaweicloud.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: multipart/form-data; boundary=--------------------------940435396775653808840608
Content-Length: 1409
 
----------------------------940435396775653808840608
Content-Disposition: form-data; name="key"
 
obj
----------------------------940435396775653808840608
Content-Disposition: form-data; name="ObsAccessKeyId"
 
XXXXXXXXXXXXXXX000003
----------------------------940435396775653808840608
Content-Disposition: form-data; name="signature"
 
X/7QiyMYUvxUWk0R5fToeTcgMMU=
----------------------------940435396775653808840608
Content-Disposition: form-data; name="policy"
 
eyJleHBpcmF0aW9uIjoiMjAyMy0wNi0xNVQxNDoyMjo1MVoiLCAiY29uZGl0aW9ucyI6W3sieC1vYnMtb2JqZWN0LWxvY2stcmV0YWluLXVudGlsLWRhdGUiOiJUaHUsIDIwIEp1biAyMDIzIDEzOjEyOjUxIEdNVCJ9LHsieC1vYnMtb2JqZWN0LWxvY2stbW9kZSI6IkNPTVBMSUFOQ0UifSx7ImJ1Y2tldCI6InNyY2J1Y2tldDIifSx7ImNvbnRlbnQtdHlwZSI6InRleHQvcGxhaW4ifSx7ImtleSI6IjMzMyJ9LF19
----------------------------940435396775653808840608
Content-Disposition: form-data; name="x-obs-object-lock-mode"
 
COMPLIANCE
----------------------------940435396775653808840608
Content-Disposition: form-data; name="x-obs-object-lock-retain-until-date"
 
Thu, 20 Jun 2023 13:12:51 GMT
----------------------------940435396775653808840608
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain
 
 
----------------------------940435396775653808840608
Content-Disposition: form-data; name="submit"
 
Upload to OBS
----------------------------940435396775653808840608--
```

## 响应示例：上传时配置对象级WORM保护策略<a name="section1102140135316"></a>

```
HTTP/1.1 204 No Content
Server: OBS
Date: Thu, 15 Jun 2023 13:24:03 GMT
Connection: keep-alive
Location: http://obs.cn-north-4.myhuaweicloud.com/srcbucket/obj
ETag: "d41d8cd98f00b204e9800998ecf8427e"
x-obs-request-id: 00000188BF3A36EE5306427D000FEE0A
x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS/5pj0p0hAQcDVI3B6E5y167zy4eAQv
x-forward-status: 0x40020000000001
x-dae-api-type: REST.POST.OBJECT
```

