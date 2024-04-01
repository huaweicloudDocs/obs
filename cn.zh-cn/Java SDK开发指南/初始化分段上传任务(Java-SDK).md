# 初始化分段上传任务\(Java SDK\)<a name="obs_21_0615"></a>

## 功能说明<a name="section36461555173814"></a>

使用分段上传方式传输数据前，必须先通知OBS初始化一个分段上传任务。该操作会返回一个OBS服务端创建的全局唯一标识（Upload ID），用于标识本次分段上传任务。您可以根据这个唯一标识来发起相关的操作，如取消分段上传任务、列举分段上传任务、列举已上传的段等。

## 接口约束<a name="section1828605625916"></a>

-   您必须是桶拥有者或拥有初始化分段上传任务的权限，才能初始化分段上传任务。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:PutObject权限，如果使用桶策略则需授予PutObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   初始化上传段任务并上传一个或多个段之后，您必须合并段或取消多段上传任务，否则碎片会占用您的存储空间并产生一定的存储费用。

## 方法定义<a name="section54232412"></a>

obsClient.initiateMultipartUpload\([InitiateMultipartUploadRequest](#table152451312111) [request](#table1210700)\)

## 请求参数说明<a name="section964134015398"></a>

**表 1**  initiateMultipartUpload请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|InitiateMultipartUploadRequest|必选|**参数解释：**初始化分段上传任务，详见InitiateMultipartUploadRequest。|


**表 2**  InitiateMultipartUploadRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|metadata|ObjectMetadata|可选|**参数解释：**对象元数据，详见ObjectMetadata。**默认取值：**无|
|acl|AccessControlList|可选|**参数解释：**创桶时可指定桶的ACL访问策略，您可以使用预定义的ACL策略，也可以自定义ACL策略，有关访问控制列表（Access Control List，ACL）功能的详细信息可参见ACL功能介绍。**取值范围：**如果使用预定义ACL策略，则可选策略参见ACL预定义访问策略。如果选择自定义ACL策略，则可以根据AccessControlList参数描述，自行给参数赋值。**默认取值：**AccessControlList.REST_CANNED_PRIVATE|
|sseKmsHeader|SseKmsHeader|可选|**参数解释：**服务端加密头信息。详见SseKmsHeader。**默认取值：**无|
|sseCHeader|SseCHeader|可选|**参数解释：**服务端加密头信息。详见SseCHeader。**默认取值：**无|
|extensionPermissionMap|Map<ExtensionObjectPermissionEnum, Set<String>>|可选|**参数解释：**桶ACL的授权Map，您可以为一个或多个账号授予桶权限。Map的ExtensionObjectPermissionEnum用于指定权限，Map的Set<String>用于说明该权限授予的账号ID列表，即domain_id列表。**取值范围：**授予权限的范围详见ExtensionObjectPermissionEnum。如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|expires|int|可选|**参数解释：**表示对象的过期时间（从对象最后修改时间开始计算）。过期之后对象会被自动删除。**约束限制：**此字段对于每个对象支持上传时配置，也支持后期通过修改元数据接口附带头域x-obs-expires修改。**取值范围：**大于0的整型数，单位：天。**默认取值：**无|
|encodeHeaders|boolean|可选|**参数解释：**是否开启OBS对请求头域的自动编码。由于HTTP编码规范限制，无法发送非ASCII码字符，SDK会在发送请求时对您头域中的**中文汉字**进行url编码，发送编码后数据。如您设置的值content-disposition为“attachment; filename="中文.txt"”，则对象元数据中存储的信息为“attachment; filename="%E4%B8%AD%E6%96%87.txt"”。使用浏览器访问时浏览器将会自动解码。**取值范围：**true：启用SDK编码。false：不启用SDK编码。**默认取值：**true|


**表 3**  ACL预定义访问策略

|**常量名**|**说明**|
|--|--|
|AccessControlList.REST_CANNED_PRIVATE|私有读写。桶或对象的所有者拥有完全控制的权限，其他任何人都没有访问权限。|
|AccessControlList.REST_CANNED_PUBLIC_READ|公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE|公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_DELIVERED|桶公共读，桶内对象公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据，可以获取该桶内对象的内容和元数据。不能应用于对象。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE_DELIVERED|桶公共读写，桶内对象公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象、删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务，可以获取该桶内对象的内容和元数据。不能应用于对象。|


**表 4**  ExtensionObjectPermissionEnum

|**常量值**|**说明**|
|--|--|
|GRANT_READ|授权指定租户有读对象和获取对象元数据的权限。|
|GRANT_READ_ACP|授权指定租户有获取对象ACL的权限。|
|GRANT_WRITE_ACP|授权指定租户有写对象ACL的权限。|
|GRANT_FULL_CONTROL|授权指定租户有读对象、获取对象元数据、获取对象ACL、写对象ACL的权限。|


**表 5**  SseCHeader

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|algorithm|ServerAlgorithm|必选|**参数解释：**表示服务端加密是SSE-C方式，对象使用SSE-C加密方式。**取值范围：**可选值：AES256，即选择SSE-C方式，使用高级加密标准（Advanced Encryption Standard，AES）加密对象。详见ServerAlgorithm。**默认取值：**无|
|sseAlgorithm|SSEAlgorithmEnum|可选|**参数解释：**加密算法。**约束限制：**只支持AES256。**取值范围：**详见SSEAlgorithmEnum。**默认取值：**无|
|sseCKey|byte[]|必选|**参数解释：**SSE-C方式下加密使用的原始密钥，byte[]形式，该密钥用于加密对象。**默认取值：**无|
|sseCKeyBase64|String|可选|**参数解释：**SSE-C方式下的密钥，由原始密钥经过Base64编码后得到，该密钥用于加密对象。**默认取值：**无|


**表 6**  SseKmsHeader

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|encryption|ServerEncryption|必选|**参数解释：**表示服务端加密是SSE-KMS方式。对象使用SSE-KMS方式加密。**取值范围：**可选值：kms，即选择SSE-KMS方式加密对象，详见ServerEncryption。**默认取值：**无|
|sseAlgorithm|SSEAlgorithmEnum|可选|**参数解释：**加密算法。**约束限制：**只支持kms。**取值范围：**详见SSEAlgorithmEnum。**默认取值：**无|
|kmsKeyId|String|可选|**参数解释：**SSE-KMS加密方式下使用的KMS主密钥的ID值。**取值范围：**有效值支持两种格式：regionID:domainID(账号ID):key/key_idkey_id其中：regionID是使用密钥所属region的ID，可在地区和终端节点页面获取；domainID是使用密钥所属账号的账号ID，获取方法参见如何获取账号ID和用户ID?；key_id是从数据加密服务创建的密钥ID，获取方法请参见查看密钥。**默认取值：**如果用户没有提供该头域，那么默认的主密钥将会被使用。如果默认主密钥不存在，将默认创建并使用。|


**表 7**  ServerAlgorithm

|**常量值**|**原始值**|
|--|--|
|AES256|AES256|


**表 8**  ServerEncryption

|**常量值**|**原始值**|
|--|--|
|OBS_KMS|kms|


**表 9**  SSEAlgorithmEnum

|**常量值**|**原始值**|
|--|--|
|KMS|kms|
|AES256|AES256|


**表 10**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 11**  ObjectMetadata

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|contentLength|Long|可选|**参数解释：**对象数据的长度。**约束限制：**单次上传对象大小范围是[0, 5GB]。如果需要上传超过5GB的大文件，需要通过多段操作来分段上传。**默认取值：**如果不设置，则SDK会自动计算对象数据的长度。|
|contentType|String|可选|**参数解释：**对象的文件类型（MIME类型）。contentType（MIME）用于标识发送或接收数据的类型，浏览器根据该参数来决定数据的打开方式。**取值范围：**常见的contentType（MIME）列表参见如何理解Content-Type（MIME）？(Java SDK)。**默认取值：**如果未指定Content-Type，SDK会根据指定Object名称的后缀来判定文件类型并自动填充Content-Type（如.xml判断为application/xml文件；.html判断为text/html文件）。|
|contentEncoding|String|可选|**参数解释：**响应中的Content-Encoding头。指定对象内容编码格式。**默认取值：**无|
|contentDisposition|String|可选|**参数解释：**为请求的对象提供一个默认的文件名赋值给该对象，当下载对象或者访问对象时，以默认文件名命名的文件将直接在浏览器上显示，或在弹出文件下载对话框时显示。**默认取值：**无|
|cacheControl|String|可选|**参数解释：**响应中的Cache-Control头。指定对象被下载时的网页的缓存行为。**默认取值：**无|
|contentLanguage|String|可选|**参数解释：**说明访问者希望采用的语言或语言组合，以根据自己偏好的语言来定制。详情请参见HTTP协议中关于ContentLanguage的定义。**默认取值：**无|
|expires|String|可选|**参数解释：**指对象在网页中的缓存过期时间。**约束限制：**日期格式为GMT的格式。**默认取值：**无|
|contentMd5|String|可选|**参数解释：**对象数据的MD5值（经过Base64编码），提供给OBS服务端，校验数据完整性。OBS服务端会将该MD5值与对象数据计算出的MD5值进行对比，如果不匹配则上传失败，返回HTTP 400错误。**约束限制：**对象数据的MD5值必须经过Base64编码。如果不设置对象的MD5值，OBS服务端会忽略对对象数据的MD5值校验。**取值范围：**按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过Base64编码后得到的字符串。示例：n58IG6hfM7vqI4K0vnWpog==**默认取值：**无|
|storageClass|StorageClassEnum|可选|**参数解释：**对象的存储类别。创建对象时，可以加上此头域设置对象的存储类别。如果未设置此头域，则以桶的默认存储类别作为对象的存储类别。**取值范围：**可选择的存储类别参见StorageClassEnum。**默认取值：**无|
|webSiteRedirectLocation|String|可选|**参数解释：**当桶设置了Website配置，可以将获取这个对象的请求重定向到桶内另一个对象或一个外部的URL，该参数指明对象的重定向地址。例如，重定向请求到桶内另一对象：WebsiteRedirectLocation:/anotherPage.html或重定向请求到一个外部URL：WebsiteRedirectLocation:http://www.example.com/**约束限制：**必须以“/”、“http://”或“https://”开头，长度不超过2KB。OBS仅支持为桶根目录下的对象设置重定向，不支持为桶中文件夹下的对象设置重定向。**默认取值：**无|
|nextPosition|long|可选|**参数解释：**下次追加上传的位置。**取值范围：**0~对象长度，单位：字节。**默认取值：**无|
|appendable|boolean|可选|**参数解释：**对象是否为可追加上传的对象。**取值范围：**true：是，可追加上传。false：否，不可追加上传。**默认取值：**无|
|userMetadata|Map<String, Object>|可选|**参数解释：**对象的自定义元数据，OBS支持用户使用以“x-obs-meta-”开头的消息头来加入自定义的元数据，以便对对象进行自定义管理。Map中的String代表以“x-obs-meta-”开头的自定义元数据名称，Object代表自定义元数据的值。对象的自定义元数据可以通过ObsClient.getObjectMetadata获取，参见获取对象元数据。**约束限制：**一个对象可以有多个元数据，总大小不能超过8KB。使用ObsClient.getObject下载对象时，对象的自定义元数据也会同时下载。**默认取值：**无|


**表 12**  AccessControlList

|**参数名称**|**参数类型**|**是否必选**|**参数类型**|
|--|--|--|--|
|owner|Owner|可选|**参数解释：**桶所有者的信息，详见Owner。|
|delivered|boolean|可选|**参数解释：**桶的ACL是否向桶内对象传递，作用于桶内所有对象。**取值范围：**true：是，桶ACL向桶内对象传递。false：否，桶ACL不向桶内对象传递，仅作用于桶。**默认取值：**false|
|grants|Set<GrantAndPermission>|可选|**参数解释：**被授权用户相关信息，详见GrantAndPermission。|


**表 13**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 14**  GrantAndPermission

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantee|GranteeInterface|必选|**参数解释：**被授权用户或用户组，详见GranteeInterface。|
|permission|Permission|必选|**参数解释：**用户或用户组被授予的权限。**取值范围：**详见Permission。**默认取值：**无|
|delivered|boolean|可选|**参数解释：**桶的ACL是否向桶内对象传递，作用于桶内所有对象。**取值范围：**true：是，桶ACL向桶内对象传递。false：否，桶ACL不向桶内对象传递，仅作用于桶。**默认取值：**false|


**表 15**  Permission

|**常量名**|**原始值**|**说明**|
|--|--|--|
|PERMISSION_READ|READ|读权限。如果有桶的读权限，则可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。如果有对象的读权限，则可以获取该对象内容和元数据。|
|PERMISSION_WRITE|WRITE|写权限。如果有桶的写权限，则可以上传、覆盖和删除该桶内任何对象和段。此权限在对象上不适用。|
|PERMISSION_READ_ACP|READ_ACP|读取ACL配置的权限。如果有读ACP的权限，则可以获取对应的桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有读对应桶或对象ACP的权限。|
|PERMISSION_WRITE_ACP|WRITE_ACP|修改ACL配置的权限。如果有写ACP的权限，则可以更新对应桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有写对应桶或对象的ACP的权限。拥有了写ACP的权限，由于可以更改权限控制策略，实际上意味着拥有了完全访问的权限。|
|PERMISSION_FULL_CONTROL|FULL_CONTROL|完全控制权限，包括对桶或对象的读写权限，以及对桶或对象ACL配置的读写权限。如果有桶的完全控制权限意味着拥有READ、WRITE、READ_ACP和WRITE_ACP的权限。如果有对象的完全控制权限意味着拥有READ、READ_ACP和WRITE_ACP的权限。|


**表 16**  GranteeInterface

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|CanonicalGrantee|CanonicalGrantee|必选|**参数解释：**被授权用户的用户信息，详见CanonicalGrantee。|
|GroupGrantee|GroupGrantee|必选|**参数解释：**被授权用户组的用户组信息。**取值范围：**详见GroupGrantee。**默认取值：**无|


**表 17**  CanonicalGrantee

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantId|String|如果Type为用户类型则必选|**参数解释：**被授权用户的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数描述：**被授权用户的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 18**  GroupGrantee

|**常量名**|**说明**|
|--|--|
|ALL_USERS|所有用户。|
|AUTHENTICATED_USERS|授权用户，已废弃。|
|LOG_DELIVERY|日志投递组，已废弃。|


## 返回结果<a name="section1934265119215"></a>

**表 19**  返回值类型 InitiateMultipartUploadResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|uploadId|String|**参数解释：**OBS服务端创建的全局唯一标识（Upload ID），用于标识本次分段上传任务**取值范围：**长度大于0且不超过32的字符串。**默认取值：**无|
|bucketName|String|**参数解释：**分段上传任务的桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|**参数解释：**分段上传任务的对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符。**默认取值：**无|


## 代码示例<a name="section35571451102319"></a>

本示例用于对examplebucket桶中的objectname对象做多段上传初始化，并获取uploadId。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.InitiateMultipartUploadRequest;
import com.obs.services.model.InitiateMultipartUploadResult;
import com.obs.services.model.ObjectMetadata;
public class InitiateMultipartUpload001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        // String securityToken = System.getenv("SECURITY_TOKEN");
        // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
        String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
        // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
        //String endPoint = System.getenv("ENDPOINT");
        
        // 创建ObsClient实例
        // 使用永久AK/SK初始化客户端
        ObsClient obsClient = new ObsClient(ak, sk,endPoint);
        // 使用临时AK/SK和SecurityToken初始化客户端
        // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

        try {
            InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest("examplebucket", "objectname");
            ObjectMetadata metadata = new ObjectMetadata();
            metadata.addUserMetadata("property", "property-value");
            metadata.setContentType("text/plain");
            request.setMetadata(metadata);
            InitiateMultipartUploadResult result = obsClient.initiateMultipartUpload(request);
            String uploadId = result.getUploadId();
            System.out.println("initiateMultipartUpload successfully");
            System.out.println("uploadId:" + uploadId);
        } catch (ObsException e) {
            System.out.println("initiateMultipartUpload failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code:" + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message:" + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
            e.printStackTrace();
        } catch (Exception e) {
            System.out.println("initiateMultipartUpload failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于分段上传-初始化分段上传任务的API说明，请参见[初始化上传段任务](https://support.huaweicloud.com/api-obs/obs_04_0098.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentUploadPartSample.java#L276)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

