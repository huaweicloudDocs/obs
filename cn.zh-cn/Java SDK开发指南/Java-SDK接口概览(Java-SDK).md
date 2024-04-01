# Java SDK接口概览\(Java SDK\)<a name="obs_21_0002"></a>

## 桶相关接口<a name="section896914512375"></a>

桶相关接口如下[表](#table89211431419)所示。

**表 1**  桶相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|创建桶|obsClient.createBucket(CreateBucketRequest request)|在当前账号按照用户指定的桶名创建一个新桶，接口支持根据用户诉求，在创建桶的同时配置桶的存储类别、区域及桶的访问权限等参数。|BucketOperationsSample|
|列举桶|obsClient.listBuckets(ListBucketsRequest request)|列举当前账号所有地域下符合指定条件的桶。返回结果以桶名的字典序排序。|BucketOperationsSample|
|删除桶|obsClient.deleteBucket(String bucketName)|桶为空时，用户可以删除桶，以免占用桶数量配额。删除桶后需要等待30分钟才能创建同名桶。|BucketOperationsSample|
|判断桶是否存在|obsClient.headBucket(String bucketName)|判断指定桶名的桶是否存在，返回的结果中HTTP状态码为200表明桶存在，否则返回404表明桶不存在。|BucketOperationsSample|
|获取桶元数据|obsClient.getBucketMetadata(BucketMetadataInfoRequest request)|获取指定桶的相关信息，包括指定桶的存储类别、区域位置、跨域资源共享（CORS）规则、冗余策略等信息。|BucketOperationsSample|
|设置桶ACLs|obsClient.setBucketAcl(String bucketName,AccessControlList acl)|设置指定桶的ACL策略。|BucketOperationsSample|
|获取桶ACLs|obsClient.getBucketAcl(String bucketName)|获取指定桶的ACL策略。|BucketOperationsSample|
|设置桶策略|obsClient.setBucketPolicy(String bucketName, String policy)|配置桶的策略，如果桶已存在策略，那么当前请求中的策略将完全覆盖桶中现存的策略。|BucketOperationsSample|
|获取桶策略|obsClient.getBucketPolicy(String bucketName)|获取指定桶的桶策略。|BucketOperationsSample|
|删除桶策略|obsClient.deleteBucketPolicy(String bucketName)|删除指定桶的桶策略。无论桶的策略本身是否存在，删除成功后系统都直接返回“204 No Content”的结果。|BucketOperationsSample|
|获取桶区域位置|obsClient.getBucketLocation(String bucketName)|获取桶所在的区域位置。|BucketOperationsSample|
|获取桶存量信息|obsClient.getBucketStorageInfo(String bucketName)|获取桶的存量信息，包括桶已使用的空间大小以及桶包含的对象个数。|BucketOperationsSample|
|设置桶配额|obsClient.setBucketQuota(String bucketName, BucketQuota bucketQuota)|设置桶的配额限制来控制桶内允许上传的对象总容量，超过设置的对象容量后，上传对象会失败。|BucketOperationsSample|
|获取桶配额|obsClient.getBucketQuota(String bucketName)|获取指定桶的配额值。桶配额为0代表桶容量没有上限。|BucketOperationsSample|
|设置桶存储类别|obsClient.setBucketStoragePolicy(String bucketName, BucketStoragePolicyConfiguration bucketStorage)|设置指定桶的存储类别。设置桶的存储类别后，如果上传对象、复制对象和初始化多段上传任务时未指定对象的存储类别，则该对象的存储类别默认与桶的存储类别保持一致。|BucketOperationsSample|
|获取桶存储类别|obsClient.getBucketStoragePolicy(String bucketName)|获取指定桶的存储类别。|BucketOperationsSample|
|设置桶清单规则|obsClient.setInventoryConfiguration(SetInventoryConfigurationRequest request)|定期生成桶内对象的相关信息，保存在CSV格式的文件中，并上传到您指定的桶中，方便您管理桶内对象。指定的对象内容包括对象版本、大小、上次修改时间、存储类别、标签、加密状态等。|BucketOperationsSample|
|获取桶清单规则|obsClient.getInventoryConfiguration(GetInventoryConfigurationRequest  request)|获取指定桶的清单规则，可以通过配置规则id来选择指定清单规则。|BucketOperationsSample|
|列举桶清单规则|obsClient.listInventoryConfiguration(ListInventoryConfigurationRequest request)|列举指定桶的所有清单配置，获取到的清单配置一次性返回，不分页。|BucketOperationsSample|
|删除桶清单规则|obsClient.deleteInventoryConfiguration(DeleteInventoryConfigurationRequest request)|删除指定桶的清单配置（通过清单规则id来指定确认要删除的桶清单规则）。|BucketOperationsSample|


## 并行文件系统相关接口<a name="section14894740114118"></a>

并行文件系统相关接口如下[表](#table151521173453)所示。

**表 2**  并行文件系统相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|创建并行文件系统|obsClient.createBucket(CreateBucketRequest request)|在当前账号按照用户指定的并行文件系统名称创建一个新并行文件系统，接口支持根据用户诉求，在创建并行文件系统的同时配置并行文件系统的区域及桶的访问权限等参数。|PFSBucketAndObjectOperationSample|
|列举并行文件系统|obsClient.listBuckets(ListBucketsRequest request)|列举当前账号下符合指定条件的并行文件系统。返回结果以文件系统名的字典序排列。|PFSBucketAndObjectOperationSample|
|列举并行文件系统内对象|obsClient.listObjects(final ListObjectsRequest  request)|列举出指定并行文件系统里的对象。|PFSBucketAndObjectOperationSample|
|修改写对象|obsClient.modifyObject(ModifyObjectRequest request)|将指定并行文件系统内的一个对象从指定位置起修改为其他内容。|PFSBucketAndObjectOperationSample|
|重命名对象|obsClient.renameObject(RenameObjectRequest request)|重命名对象操作是指将指定并行文件系统内的一个对象重命名为其他对象名。|PFSBucketAndObjectOperationSample|
|截断对象|obsClient.truncateObject(TruncateObjectRequest request)|截断对象操作是指将指定并行文件系统内的一个对象截断到指定大小。|PFSBucketAndObjectOperationSample|


## 对象相关接口<a name="section71835584020"></a>

对象相关接口如下[表](#table934312264110)所示。

**表 3**  对象相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|流式上传|obsClient.putObject(PutObjectRequest  request)|通过流式上传方式将本地文件上传至OBS指定的位置，支持上传小于5GB的文件。待上传的文件可以是任何类型：文本文件、图片、视频等。|ObjectOperationsSample|
|文件上传|obsClient.putObject(PutObjectRequest  request)|将本地文件直接通过Internet上传至OBS指定的桶中。待上传的文件可以是任何类型：文本文件、图片、视频等。|-|
|获取上传进度|PutObjectRequest.setProgressListener(ProgressListener progressListener)|获取指定对象的上传进度。|-|
|创建文件夹|obsClient.putObject(PutObjectRequest  request)|在已创建的桶中新建一个文件夹，从而更方便的对存储在OBS中的数据进行分类管理。|CreateFolderSample|
|设置对象元数据|obsClient.setObjectMetadata(SetObjectMetadataRequest  request)|在上传对象时设置对象属性。对象属性包含对象长度、对象MIME类型、对象MD5值（用于校验）、对象存储类别、对象自定义元数据。对象属性可以在多种上传方式下（流式上传、文件上传、分段上传），或复制对象时进行设置。|ObjectMetaSample|
|初始化分段上传任务|obsClient.initiateMultipartUpload(InitiateMultipartUploadRequest request)|使用分段上传方式传输数据前，必须先通知OBS初始化一个分段上传任务。该操作会返回一个OBS服务端创建的全局唯一标识（Upload ID），用于标识本次分段上传任务。|SimpleMultipartUploadSample|
|上传段|obsClient.uploadPart(UploadPartRequest  request)|初始化分段上传任务后，通过分段上传任务的ID，上传段到指定桶中。|SimpleMultipartUploadSample|
|合并段|obsClient.completeMultipartUpload(CompleteMultipartUploadRequest  request)|通过分段上传任务的ID和对应已上传的段信息（包括PartNumber和ETag），合并成一个完整的对象。|SimpleMultipartUploadSample|
|取消分段上传任务|obsClient.abortMultipartUpload(AbortMultipartUploadRequest    request)|通过分段上传任务的ID，取消指定桶中的分段上传任务。|-|
|列举已上传的段|obsClient.listParts(ListPartsRequest   request)|通过分段上传任务的ID，列举指定桶中已上传的段。|ConcurrentUploadPartSample|
|列举分段上传任务|obsClient.listMultipartUploads(ListMultipartUploadsRequest  request)|列举指定桶中所有的初始化后还未合并或还未取消的分段上传任务。|-|
|设置对象生命周期|obsClient.putObject(PutObjectRequest request)|OBS支持用户配置指定的规则，实现定时删除桶中的对象或者定时转换对象的存储类别，从而节省存储费用。此接口设置的对象过期时间，其优先级高于桶生命周期规则。|-|
|追加上传|obsClient.appendObject(AppendObjectRequest  request)|对同一个对象追加数据内容。|-|
|断点续传上传|obsClient.uploadFile(UploadFileRequest  request)|对分段上传的封装和加强，解决上传大文件时由于网络不稳定或程序崩溃导致上传失败的问题。|-|
|基于表单上传|obsClient.createPostSignature(PostSignatureRequest   request)|使用HTML表单形式上传对象到指定桶中，对象最大不能超过5GB。|PostObjectSample|
|流式下载|obsClient.getObject(GetObjectRequest request)|根据需要通过流式下载将存储在OBS中的指定对象下载到本地。接口返回的ObsObject实例包含对象所在的桶、对象名、对象属性、对象输入流等内容，同时可以通过操作对象输入流将对象的内容读取到本地文件或者内存中。|DownloadSample|
|范围下载|obsClient.getObject(GetObjectRequest  request)|如果只需要下载对象的其中一部分数据，可以使用范围下载，下载指定范围的数据。|-|
|获取下载进度|GetObjectRequest.setProgressListener(ProgressListener  progressListener)|获取指定对象的下载进度。|-|
|限定条件下载|obsClient.getObject(GetObjectRequest  request)|下载对象时，可以指定一个或多个限定条件，满足限定条件时则进行下载，否则返回异常码，下载对象失败。|-|
|重写响应头|obsClient.getObject(GetObjectRequest   request)|下载对象时，可以重写HTTP/HTTPS中部分响应头的信息：Content-Type、Content-Language、Expires、Cache-Control、Content-Disposition、Content-Encoding。|-|
|获取自定义元数据|obsClient.getObject(GetObjectRequest request)|本接口可以在下载对象成功后返回对象的自定义元数据。|ObjectMetaSample|
|恢复归档存储对象|obsClient.restoreObject(RestoreObjectRequest   request)|如果要下载归档存储对象，需要先将归档存储对象恢复。恢复归档存储对象的恢复选项可支持标准恢复、快速恢复。|RestoreObjectSample|
|断点续传下载|obsClient.downloadFile(DownloadFileRequest   request)|对范围下载的封装和加强，解决下载大对象到本地时由于网络不稳定或程序崩溃导致下载失败的问题。|-|
|下载对象接口实现图片处理|obsClient.getObject(GetObjectRequest   request)|下载图片文件时，通过传入图片处理参数对图片文件进行图片剪切、图片缩放、图片水印、格式转换等处理。|-|
|临时授权方式实现图片处理|obsClient.createTemporarySignature(TemporarySignatureRequest request)|通过临时授权方式传入图片处理参数，对图片文件进行图片剪切、图片缩放、图片水印、格式转换等处理。|-|
|设置对象元数据|obsClient.setObjectMetadata(SetObjectMetadataRequest  request)|对指定桶中的对象发送HEAD请求，设置对象的元数据信息。|-|
|获取对象元数据|obsClient.getObjectMetadata(GetObjectMetadataRequest  request)|对指定桶中的对象发送HEAD请求，获取对象的元数据信息。|-|
|设置对象ACLs|obsClient.setObjectAcl(SetObjectAclRequest   request)|在上传对象时设置权限控制策略，也可以通过ACL操作API接口对已存在的对象更改ACL 。|ObjectOperationsSample|
|获取对象ACLs|obsClient.getObjectAcl(GetObjectAclRequest  request)|通过接口获取指定桶中对象的ACL访问权限，返回信息包含指定对象的权限控制列表信息。|ObjectOperationsSample|
|列举对象|obsClient.listObjects(ListObjectsRequest   request)|列举指定桶内的部分或所有对象的描述信息。还可以通过设置前缀、数量、起始位置等参数，返回符合筛选条件的对象信息。返回结果以对象名的字典序排序。|ListObjectsSample|
|删除对象|obsClient.deleteObject(DeleteObjectRequest  request)|根据需要删除指定桶中的对象，节省空间和成本。|ObjectOperationsSample|
|批量删除对象|obsClient.deleteObjects(DeleteObjectsRequest  deleteRequest)|根据需要批量删除指定桶中的多个对象，节省空间和成本。批量删除对象用于将一个桶内的部分对象一次性删除，删除后不可恢复。批量删除对象要求返回结果里包含每个对象的删除结果。|DeleteObjectsSample|
|复制对象|obsClient.copyObject(CopyObjectRequest   request)|为指定桶中的对象创建一个副本。在单次操作中，可以创建最大5GB的对象副本。|ObjectOperationsSample|
|分段复制|obsClient.copyPart(CopyPartRequest  request)|初始化分段上传任务后，通过分段上传任务的ID，复制段到指定桶中。|ConcurrentCopyPartSample|
|判断对象是否存在|doesObjectExist(final GetObjectMetadataRequest  request)|判断对象是否存在，返回的结果中HTTP状态码为200表明对象存在，否则返回404表明对象或桶不存在。|-|


## 临时授权访问相关接口<a name="section165991833111718"></a>

临时授权访问相关接口如下[表](#table1158520575219)所示。

**表 4**  临时授权访问相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|通过临时URL访问OBS|obsClient.createTemporarySignature(TemporarySignatureRequest  request)|通过访问密钥、请求方法类型、请求参数等信息生成一个在Query参数中携带鉴权信息的URL，可将该URL提供给其他用户进行临时访问。在生成URL时，您需要指定URL的有效期来限制访客用户的访问时长。如果您想授予其他用户对桶或对象临时进行其他操作的权限（例如上传或下载对象），则需要生成带对应请求的URL后（例如使用生成PUT请求的URL上传对象），将该URL提供给其他用户。|TemporarySignatureSample|


## 多版本控制相关接口<a name="section1699943620175"></a>

多版本控制相关接口如下[表](#table2878128181819)所示。

**表 5**  多版本控制相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|设置桶多版本状态|obsClient.setBucketVersioning(final SetBucketVersioningRequest  request)|为指定桶设置多版本状态。在一个桶中保留对象的多个版本，可方便地检索和还原各个版本，在意外操作或应用程序故障时快速恢复数据。|BucketOperationsSample|
|获取桶多版本状态|obsClient.getBucketVersioning(final BaseBucketRequest   request)|获取指定桶的多版本状态。|BucketOperationsSample|
|获取多版本对象|obsClient.getObject(GetObjectRequest request)|获取指定多版本对象。|-|
|复制多版本对象|obsClient.copyObject(CopyObjectRequest   request)|为指定桶中的多版本对象创建一个副本。在单次操作中，可以创建最大5GB的对象副本。|-|
|恢复多版本归档存储对象|obsClient.restoreObject(RestoreObjectRequest   request)|通过接口传入版本号，恢复多版本归档存储对象。如果要下载归档存储对象，需要先将归档存储对象恢复。恢复归档存储对象的恢复选项可支持标准恢复、快速恢复。|-|
|列举多版本对象|obsClient.listVersions(ListVersionsRequest  request)|列举指定桶内的部分或所有多版本对象的描述信息。还可以通过设置前缀、数量、起始位置等参数，返回符合您筛选条件的多版本对象信息。返回结果以多版本对象名的字典序排序。|ListVersionsSample|
|设置多版本对象权限|obsClient.setObjectAcl(SetObjectAclRequest    request)|在上传多版本对象时，设置权限控制策略，也可以通过ACL操作API接口对已存在的对象更改或者获取ACL。|-|
|获取多版本对象权限|obsClient.getObjectAcl(GetObjectAclRequest    request)|获取指定桶的获取多版本对象权限。|-|
|删除多版本对象|obsClient.deleteObject(DeleteObjectRequest request)|根据需要删除指定桶中的多版本对象，节省空间和成本。|-|
|批量删除多版本对象|obsClient.deleteObjects(DeleteObjectsRequest  deleteRequest)|根据需要批量删除指定桶中的多个多版本对象，节省空间和成本。批量删除对象用于将一个桶内的部分多版本对象一次性删除，删除后不可恢复。批量删除多版本对象要求返回结果里包含每个多版本对象的删除结果。|ListVersionsSample|


## 生命周期管理相关接口<a name="section512815593195"></a>

生命周期管理相关接口如下[表](#table678511151920)所示。

**表 6**  生命周期管理相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|设置生命周期规则|obsClient.setBucketLifecycle(final SetBucketLifecycleRequest request)|为指定桶设置生命周期规则，实现定时删除桶中的对象或者定时转换对象的存储类别，从而节省存储费用。|BucketOperationsSample|
|获取生命周期规则|obsClient.getBucketLifecycle(final BaseBucketRequest   request)|获取指定桶的生命周期规则。|BucketOperationsSample|
|删除生命周期规则|obsClient.deleteBucketLifecycle(final BaseBucketRequest request)|删除指定桶的生命周期规则。|BucketOperationsSample|


## 跨域资源共享相关接口<a name="section746515134227"></a>

跨域资源共享相关接口如下[表](#table6639334361)所示。

**表 7**  跨域资源共享相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|设置跨域资源共享规则|obsclient.setBucketCors(final SetBucketCorsRequest  request)|设置桶的跨域资源共享规则，允许客户端浏览器进行跨域请求。设置成功后，如果原规则存在则覆盖原规则。|BucketOperationsSample|
|获取跨域资源共享规则|obsclient.getBucketCors(final BaseBucketRequest  request)|获取指定桶的跨域资源共享规则。|BucketOperationsSample|
|删除跨域规则|obsclient.deleteBucketCors(final BaseBucketRequest request)|删除指定桶的跨域资源共享规则。|BucketOperationsSample|


## 桶日志相关接口<a name="section7505113232"></a>

设置访问日志相关接口如下[表](#table1596561414238)所示。

**表 8**  桶日志相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|设置桶日志规则|obsClient.setBucketLogging(final  SetBucketLoggingRequest  request)|为指定桶打开桶日志功能，并配置日志存放的目标桶。桶日志功能开启后，桶的每次操作将会产生一条日志，并将多条日志打包成一个日志文件。日志文件存放到开启日志功能的桶中，也可以存放到其他您有权限的桶中，但需要和开启日志功能的桶在同一个region中。您还可以根据需要配置日志文件的访问权限，以及日志文件的文件名前缀。|BucketOperationsSample|
|获取桶日志规则|obsClient.getBucketLogging(final  BaseBucketRequest  request)|获取指定桶的日志配置。|BucketOperationsSample|


## 静态网站托管相关接口<a name="section161711158182318"></a>

静态网站托管相关接口如下[表](#table13550747112413)所示。

**表 9**  静态网站托管相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|网站文件托管|obsClient.putObject(PutObjectRequest  request)obsClient.setObjectAcl(SetObjectAclRequest   acl)|将静态网站文件上传至OBS的桶中作为对象，并对这些对象赋予公共读权限，然后将该桶配置成静态网站托管模式，以实现在OBS上托管静态网站的目的。|-|
|设置托管配置|obsClient.setBucketWebsite(final SetBucketWebsiteRequest request)|为指定桶设置网站配置信息。|BucketOperationsSample|
|获取托管配置|obsClient.getBucketWebsite(final BaseBucketRequest  request)|获取指定桶的网站配置信息。|BucketOperationsSample|
|删除托管配置|obsClient.deleteBucketWebsite(final BaseBucketRequest  request)|删除指定桶的网站配置。|BucketOperationsSample|


## 标签管理相关接口<a name="section89498165245"></a>

标签管理相关接口如下[表](#table1198423822515)所示。

**表 10**  标签管理相关接口概览

|**接口名**|**方法**|**功能描述**|**示例代码源代码**|
|--|--|--|--|
|设置桶标签|obsClient.setBucketTagging(final SetBucketTaggingRequest request)|为桶添加标签，该桶上所有请求产生的计费话单里都会带上这些标签，从而可以针对话单报表做分类筛选，进行更详细的成本分析。|BucketOperationsSample|
|获取桶标签|obsClient.getBucketTagging(final BaseBucketRequest   request)|获取指定桶的标签。|BucketOperationsSample|
|删除桶标签|obsClient.deleteBucketTagging(final  BaseBucketRequest   request)|删除指定桶的标签。|BucketOperationsSample|


