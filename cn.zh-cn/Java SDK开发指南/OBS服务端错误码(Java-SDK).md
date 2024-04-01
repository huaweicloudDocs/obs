# OBS服务端错误码\(Java SDK\)<a name="obs_21_2002"></a>

在向OBS服务端发出请求后，如果遇到错误，会在响应中包含响应的错误码描述错误信息。详细的错误码及其对应的描述和HTTP状态码见下表：

|HTTP状态码|错误码|错误信息|处理措施|
|--|--|--|--|
|301 Moved Permanently|PermanentRedirect|尝试访问的桶必须使用指定的地址，请将以后的请求发送到这个地址。|按照返回的重定向地址发送请求。|
|301 Moved Permanently|WebsiteRedirect|Website请求缺少bucketName。|携带桶名后重试。|
|307 Moved Temporarily|TemporaryRedirect|临时重定向，当DNS更新时，请求将被重定向到桶。|会自动重定向，也可以将请求发送到重定向地址。|
|400 Bad Request|BadDigest|客户端指定的对象内容的MD5值与系统接收到的内容MD5值不一致。|检查头域中携带的MD5与消息体计算出来的MD5是否一致。|
|400 Bad Request|BadDomainName|域名不合法。|使用合法的域名。|
|400 Bad Request|BadRequest|请求参数不合法。|根据返回的错误消息体提示进行修改。|
|400 Bad Request|CustomDomainAreadyExist|配置了已存在的域。|已经配置过了，不需要再配置。|
|400 Bad Request|CustomDomainNotExist|删除不存在的域。|未配置或已经删除，无需删除。|
|400 Bad Request|EntityTooLarge|用户POST上传的对象大小超过了条件允许的最大大小。|修改POST上传的policy中的条件或者减少对象大小。|
|400 Bad Request|EntityTooSmall|用户POST上传的对象大小小于条件允许的最小大小。|修改POST上传的policy中的条件或者增加对象大小。|
|400 Bad Request|IllegalLocationConstraintException|用户未带Location在非默认Region创桶。|请求发往默认Region创桶或带非默认Region的Location创桶。|
|400 Bad Request|IncompleteBody|由于网络原因或其他问题导致请求体未接受完整。|重新上传对象。|
|400 Bad Request|IncorrectNumberOfFilesInPost Request|每个POST请求都需要带一个上传的文件。|带上一个上传文件。|
|400 Bad Request|InvalidArgument|无效的参数。|根据返回的错误消息体提示进行修改。|
|400 Bad Request|InvalidBucket|请求访问的桶已不存在。|更换桶名。|
|400 Bad Request|InvalidBucketName|请求中指定的桶名无效，超长或带不允许的特殊字符。|更换桶名。|
|400 Bad Request|InvalidEncryptionAlgorithmError|错误的加密算法。下载SSE-C加密的对象，携带的加密头域错误，导致不能解密。|携带正确的加密头域下载对象。|
|400 Bad Request|InvalidLocationConstraint|创建桶时，指定的Location不合法或不存在。|指定正确的Location创桶。|
|400 Bad Request|InvalidPart|一个或多个指定的段无法找到。这些段可能没有上传，或者指定的entity tag与段的entity tag不一致。|按照正确的段和entity tag合并段。|
|400 Bad Request|InvalidPartOrder|段列表的顺序不是升序，段列表必须按段号升序排列。|按段号升序排列后重新合并。|
|400 Bad Request|InvalidPolicyDocument|表单中的内容与策略文档中指定的条件不一致。|根据返回的错误消息体提示修改构造表单的policy重试。|
|400 Bad Request|InvalidRedirectLocation|无效的重定向地址。|指定正确的地址。|
|400 Bad Request|InvalidRequest|无效请求。|根据返回的错误消息体提示进行修改。|
|400 Bad Request|InvalidRequestBody|请求体无效，需要消息体的请求没有上传消息体。|按照正确的格式上传消息体。|
|400 Bad Request|InvalidTargetBucketForLogging|delivery group对目标桶无ACL权限。|对目标桶配置ACL权限后重试。|
|400 Bad Request|KeyTooLongError|提供的Key过长。|使用较短的Key。|
|400 Bad Request|KMS.DisabledException|SSE-KMS加密方式下，主密钥被禁用。|更换密钥后重试，或联系技术支持。|
|400 Bad Request|KMS.NotFoundException|SSE-KMS加密方式下，主密钥不存在。|携带正确的主密钥重试。|
|400 Bad Request|MalformedACLError|提供的XML格式错误，或者不符合要求的格式。|使用正确的XML格式重试。|
|400 Bad Request|MalformedError|请求中携带的XML格式不正确。|使用正确的XML格式重试。|
|400 Bad Request|MalformedLoggingStatus|Logging的XML格式不正确。|使用正确的XML格式重试。|
|400 Bad Request|MalformedPolicy|Bucket policy检查不通过。|根据返回的错误消息体提示结合桶policy的要求进行修改。|
|400 Bad Request|MalformedQuotaError|Quota的XML格式不正确。|使用正确的XML格式重试。|
|400 Bad Request|MalformedXML|当用户发送了一个配置项的错误格式的XML会出现这样的错误。|使用正确的XML格式重试。|
|400 Bad Request|MaxMessageLengthExceeded|拷贝对象，带请求消息体。|拷贝对象不带消息体重试。|
|400 Bad Request|MetadataTooLarge|元数据消息头超过了允许的最大元数据大小。|减少元数据消息头。|
|400 Bad Request|MissingRegion|请求中缺少Region信息，且系统无默认Region。|请求中携带Region信息。|
|400 Bad Request|MissingRequestBodyError|当用户发送一个空的XML文档作为请求时会发生。|提供正确的XML文档。|
|400 Bad Request|MissingRequiredHeader|请求中缺少必要的头域。|提供必要的头域。|
|400 Bad Request|MissingSecurityHeader|请求缺少一个必须的头。|提供必要的头域。|
|400 Bad Request|TooManyBuckets|用户拥有的桶的数量达到了系统的上限，并且请求试图创建一个新桶。|删除部分桶后重试。|
|400 Bad Request|TooManyCustomDomains|配置了过多的用户域|删除部分用户域后重试。|
|400 Bad Request|TooManyWrongSignature|因高频错误请求被拒绝服务。|更换正确的Access Key后重试。|
|400 Bad Request|UnexpectedContent|该请求需要消息体而客户端没带，或该请求不需要消息体而客户端带了。|根据说明重试。|
|400 Bad Request|AZRedundancyTypeNotSupported|当前region不支持此AZRedundancy的桶|选择合适的AZ Redundancy创桶|
|400 Bad Request|UserKeyMustBeSpecified|该操作只有特殊用户可使用。|请联系技术支持。|
|403 Forbidden|AccessDenied|拒绝访问，请求没有携带日期头域或者头域格式错误。|请求携带正确的日期头域。|
|403 Forbidden|AccessForbidden|权限不足，桶未配置CORS或者CORS规则不匹配。|修改桶的CORS配置，或者根据桶的CORS配置发送匹配的OPTIONS请求。|
|403 Forbidden|AllAccessDisabled|用户无权限执行某操作。桶名为禁用关键字。|更换桶名。|
|403 Forbidden|DeregisterUserId|用户已经注销。|充值或重新开户。|
|403 Forbidden|InArrearOrInsufficientBalance|用户欠费或余额不足而没有权限进行某种操作。|充值。|
|403 Forbidden|InsufficientStorageSpace|存储空间不足。|超过配额限制，增加配额或删除部分对象。|
|403 Forbidden|InvalidAccessKeyId|系统记录中不存在客户提供的Access Key Id。|携带正确的Access Key Id。|
|403 Forbidden|NotSignedUp|你的账户还没有在系统中注册，必须先在系统中注册了才能使用该账户。|先注册OBS服务。|
|403 Forbidden|RequestTimeTooSkewed|请求的时间与服务器的时间相差太大。|检查客户端时间是否与当前时间相差太大。|
|403 Forbidden|SignatureDoesNotMatch|请求中带的签名与系统计算得到的签名不一致。|检查你的Secret Access Key和签名计算方法。|
|403 Forbidden|Unauthorized|用户未实名认证。|请实名认证后重试。|
|404 Not Found|NoSuchBucket|指定的桶不存在。|先创桶再操作。|
|404 Not Found|NoSuchBucketPolicy|桶policy不存在。|先配置桶policy。|
|404 Not Found|NoSuchCORSConfiguration|CORS配置不存在。|先配置CORS。|
|404 Not Found|NoSuchCustomDomain|请求的用户域不存在。|先设置用户域。|
|404 Not Found|NoSuchKey|指定的Key不存在。|先上传对象。|
|404 Not Found|NoSuchLifecycleConfiguration|请求的LifeCycle不存在。|先配置LifeCycle。|
|404 Not Found|NoSuchUpload|指定的多段上传不存在。Upload ID不存在，或者多段上传已经终止或完成。|使用存在的段或重新初始化段。|
|404 Not Found|NoSuchVersion|请求中指定的version ID与现存的所有版本都不匹配。|使用正确的version ID。|
|404 Not Found|NoSuchWebsiteConfiguration|请求的Website不存在。|先配置Website。|
|405 Method Not Allowed|MethodNotAllowed|指定的方法不允许操作在请求的资源上。对应返回的Message为：Specified method is not supported.|方法不允许。|
|408 Request Timeout|RequestTimeout|用户与Server之间的socket连接在超时时间内没有进行读写操作。|检查网络后重试，或联系技术支持。|
|409 Conflict|BucketAlreadyExists|请求的桶名已经存在。桶的命名空间是系统中所有用户共用的，选择一个不同的桶名再重试一次。|更换桶名。|
|409 Conflict|BucketAlreadyOwnedByYou|发起该请求的用户已经创建过了这个名字的桶，并拥有这个桶。|不需要再创桶了。|
|409 Conflict|BucketNotEmpty|用户尝试删除的桶不为空。|先删除桶中对象，然后再删桶。|
|409 Conflict|FsObjectConflict|用户上传或创建文件失败|检查创建文件规则。例如是否在不允许覆盖的场景下覆盖文件、是否在POSIX语义下在文件下上传文件（将文件当作目录）|
|409 Conflict|InvalidBucketState|无效的桶状态，配置跨Region复制后不允许关闭桶多版本。|不关闭桶的多版本或取消跨Region复制。|
|409 Conflict|OperationAborted|另外一个冲突的操作当前正作用在这个资源上，请重试。|等待一段时间后重试。|
|409 Conflict|ServiceNotSupported|请求的方法服务端不支持。|服务端不支持，请联系技术支持。|
|411 Length Required|MissingContentLength|必须要提供HTTP消息头中的Content-Length字段。|提供Content-Length消息头。|
|412 Precondition Failed|PreconditionFailed|用户指定的先决条件中至少有一项没有包含。|根据返回消息体中的Condition提示进行修改。|
|416 Client Requested Range Not Satisfiable|InvalidRange|请求的range不可获得。|携带正确的range重试。|
|500 Internal Server Error|InternalError|系统遇到内部错误，请重试。|请联系技术支持。|
|501 Not Implemented|ServiceNotImplemented|请求的方法服务端没有实现。|当前不支持，请联系技术支持。|
|503 Service Unavailable|ServiceUnavailable|服务器过载或者内部错误异常。|等待一段时间后重试，或联系技术支持。|
|503 Service Unavailable|SlowDown|请降低请求频率。|请降低请求频率。|


