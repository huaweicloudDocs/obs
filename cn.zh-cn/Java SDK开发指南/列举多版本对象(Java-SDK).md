# 列举多版本对象\(Java SDK\)<a name="obs_21_1007"></a>

## 功能说明<a name="section4647122210617"></a>

用列举桶内对象接口，可列举指定桶内的部分或所有多版本对象的描述信息。您还可以通过设置前缀、数量、起始位置等参数，返回符合您筛选条件的多版本对象信息。返回结果以多版本对象名的字典序排序。

ObsClient.listVersions返回结果包含多版本对象和对象删除标记。

## 接口约束<a name="section326152964516"></a>

-   您必须是桶拥有者或拥有列举桶内多版本对象的权限，才能列举桶内多版本对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:ListBucketVersions权限，如果使用桶策略则需授予ListBucketVersions权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   每次至多返回1000个多版本对象，如果指定桶包含的对象数量大于1000，可以采用[分页列举](#section1031716453513)的方式返回桶中所有多版本对象。列举时，ListVersionsResult.isTruncated为true表明本次没有返回全部对象，可以通过ListVersionsResult.getNextKeyMarker和ListVersionsResult.getNextVersionIdMarker获取下次列举的起始位置。

## 方法定义<a name="section54232412"></a>

obsClient.listVersions\([ListVersionsRequest](#table5211124474317) [request](#obs_21_0708_table1210700)\)

## 请求参数说明<a name="section654003413147"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|ListVersionsRequest|必选|**参数解释：**列举多版本对象请求参数，详见ListVersionsRequest。|


**表 2**  请求参数ListVersionsRequest成员说明

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|prefix|String|可选|**参数解释：**限定返回的对象名必须带有prefix前缀。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|keyMarker|String|可选|**参数解释：**列举多版本对象的起始位置，返回的对象列表将是对象名按照字典序排序后该参数以后的所有对象。**约束限制：**该字段仅用于多版本列举。**取值范围：**上次请求返回体的nextKeyMarker值。**默认取值：**无|
|maxKeys|int|可选|**参数解释：**列举多版本对象的最大数目，返回的对象列表将是按照字典顺序的最多前maxKeys个对象。**取值范围：**1~1000，当超出范围时，按照默认的1000进行处理。**默认取值：**1000|
|delimiter|String|可选|**参数解释：**将对象名进行分组的分隔符。如果指定了prefix，从prefix到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes；如果没有指定prefix，从对象名的首字符到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes。例如，桶中有3个对象，分别为abcd、abcde、bbcde。如果指定delimiter为d，prefix为a，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefix；如果只指定delimiter为d，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefix，而bbcde会被单独分成一组，形成一条前缀为bbcd的commonPrefix。对于并行文件系统，不携带此参数时默认列举是递归列举此目录下所有内容，会列举子目录。在大数据场景下（目录层级深、目录下文件多）的列举，建议设置[delimiter=/]，只列举当前目录下的内容，不列举子目录，提高列举效率。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionIdMarker|String|可选|**参数解释：**与keyMarker配合使用，返回的对象列表将是对象名和版本号按照字典序排序后该参数以后的所有对象。keyMarker指定对象名，versionIdMarker指定该对象的具体版本号，两者共同确定对象版本。**约束限制：**该字段只适用于多版本列举场景。如果versionIdMarker不是keyMarker的一个版本号，则该参数无效。**取值范围：**对象的版本号，即上次请求返回体的nextVersionIdMarker值。**默认取值：**无|
|encodingType|String|可选|**参数解释：**对响应中的部分元素进行指定类型的编码。如果 delimiter、keyMarker、prefix、nextKeyMarker 和 key 包含 xml 1.0 标准不支持的控制字符，可通过设置 encodingType 对响应中的 delimiter、keyMarker、prefix（包括 commonPrefixes 中的 prefix）、nextKeyMarker 和 key 进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|


## 返回结果说明<a name="section191961924191715"></a>

**表 3**  ListVersionsResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|bucketName|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|prefix|String|**参数解释：**对象名的前缀，与请求中的该参数对应。例如，假设您拥有以下对象：logs/day1、logs/day2、logs/day3和ExampleObject.jpg。如果您将logs/指定为前缀，将返回以字符串“logs/”开头的三个对象。如果您指定空的前缀且请求中没有其他过滤条件，将返回桶中的所有对象。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionIdMarker|String|**参数解释：**keyMarker对象的对应版本号。与KeyMarker配合使用。返回的对象列表将是对象名和版本号按照字典序排序后该参数以后的所有对象。KeyMarker指定对象名，versionIdMarker指定该对象的具体版本号，两者共同确定对象版本**约束限制：**该字段只适用于多版本列举场景。如果versionIdMarker不是keyMarker的一个版本号，则该参数无效。**取值范围：**长度为32的字符串。**默认取值：**无|
|nextVersionIdMarker|String|**参数解释：**下次列举多版本对象请求的起始位置（versionIdMarker），与nextKeyMarker配合使用。如果本次没有返回全部结果，响应请求中将包含该元素，用于标明接下来请求的versionIdMarker值。**约束限制：**该字段只适用于多版本列举场景。**取值范围：**长度为32的字符串。**默认取值：**无|
|objectSummaries|List<ObsObject>|**参数解释：**对象信息，详见ObsObject。|
|commonPrefixes|List<String>|**参数解释：**当请求中设置了delimiter分组字符时，返回按Delimiter分组后的对象名称前缀列表。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|truncated|boolean|**参数解释：**表明本次请求是否返回了全部结果。因为每次列举返回对象的数量上限是1000个，如果对象个数大于1000，则无法通过一次请求返回全部结果。**取值范围：**true：表示没有返回全部结果。false：表示已返回了全部结果。**默认取值：**无|
|keyMarker|String|**参数解释：**列举多版本对象的起始位置，与请求中的该参数对应。返回的对象列表将是对象名按照字典序排序后该参数以后的所有对象。**约束限制：**该字段仅用于多版本列举。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|maxKeys|int|**参数解释：**列举对象的最大数目，与请求中的该参数对应。返回的对象列表将是按照字典顺序的最多前maxKeys个对象。**取值范围：**1~1000，当超出范围时，按照默认的1000进行处理。**默认取值：**1000|
|delimiter|String|**参数解释：**对象名按照此标识符进行分组。通常与prefix参数搭配使用，如果指定了prefix，从prefix到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes；如果没有指定prefix，从对象名的首字符到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes。例如，桶中有3个对象，分别为abcd、abcde、bbcde。如果指定delimiter为d，prefix为a，abcd、abcde会被分成一组，形成一条前缀为abcd的CommonPrefixes；如果只指定delimiter为d，abcd、abcde会被分成一组，形成一条前缀为abcd的CommonPrefixes，而bbcde会被单独分成一组，形成一条前缀为bbcd的CommonPrefixes。对于并行文件系统，不携带此参数时默认列举是递归列举此目录下所有内容，会列举子目录。在大数据场景下（目录层级深、目录下文件多）的列举，建议设置[delimiter=/]，只列举当前目录下的内容，不列举子目录，提高列举效率。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|nextKeyMarker|String|**参数解释：**下次列举多版本对象请求的起始位置。如果本次没有返回全部结果，响应请求中将包含该元素，用于标明接下来请求的keyMarker值。**约束限制：**该字段仅用于多版本列举。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|location|String|**参数解释：**桶所在的区域。**约束限制：**该参数定义了桶将会被创建在哪个区域，如果使用的终端节点是obs.myhuaweicloud.com，可以不携带此参数；如果使用的终端节点不是obs.myhuaweicloud.com，则必须携带此参数。**取值范围：**当前有效的OBS区域和终端节点的更多信息，请参考地区和终端节点。终端节点即调用API的请求地址，不同服务不同区域的终端节点不同，您可以向企业管理员获取区域和终端节点信息。**默认取值：**终端节点为obs.myhuaweicloud.com且用户未设定区域时，默认为华北-北京一（cn-north-1）。|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|versions|VersionOrDeleteMarker[]|**参数解释：**对象多版本信息，详见VersionOrDeleteMarker。|


**表 4**  ObsObject

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|bucketName|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|owner|Owner|**参数解释：**所有者，详见Owner。|
|metadata|ObjectMetadata|**参数解释：**对象元数据，详见ObjectMetadata。|
|objectContent|InputStream|**参数解释：**对象数据流。**默认取值：**无|


**表 5**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 6**  ObjectMetadata

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


**表 7**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 8**  VersionOrDeleteMarker

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|bucketName|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|key|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionId|String|**参数解释：**对象的版本号。**取值范围：**长度为32的字符串。**默认取值：**无|
|isLatest|boolean|**参数解释：**标识对象是否是最新的版本。**取值范围：**true：代表是最新的版本。false：代表非最新版本。**默认取值：**false|
|lastModified|Date|**参数解释：**对象最近一次被修改的时间（UTC时间）。**取值范围：**UTC时间**默认取值：**无|
|owner|Owner|**参数解释：**用户信息，包含对象拥有者DomainId和对象拥有者名称，详见Owner。|
|etag|String|**参数解释：**对象的Base64编码的128位MD5摘要。ETag是对象内容的唯一标识，可以通过该值识别对象内容是否有变化。实际标签是对象的哈希。比如上传对象时ETag为A，下载对象时ETag为B，则说明对象内容发生了变化。ETag只反映变化的内容，而不是其元数据。上传的对象或拷贝操作创建的对象，通过MD5加密后都有唯一的ETag。**约束限制：**当对象是服务端加密的对象时，ETag值不是对象的MD5值。**取值范围：**长度为32的字符串。**默认取值：**无|
|size|long|**参数解释：**对象的字节数。**取值范围：**0~48.8TB，单位：字节。**默认取值：**无|
|storageClass|StorageClassEnum|**参数解释：**对象的存储类别。创建对象时，可以加上此头域设置对象的存储类别。如果未设置此头域，则以桶的默认存储类别作为对象的存储类别。**取值范围：**可选择的存储类别参见StorageClassEnum。**默认取值：**无|
|isDeleteMarker|boolean|**参数解释：**是否为删除标记。**取值范围：**true：为删除标记。false：不为删除标记。**默认取值：**无|


## 代码示例：简单列举多版本对象<a name="section1131134512511"></a>

以下代码展示如何简单列举examplebucket桶中的多版本对象，最多返回1000个对象。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions001 {
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
            // 简单列举
            ListVersionsResult result = obsClient.listVersions("examplebucket");
            System.out.println("listVersions successfully");
            for (VersionOrDeleteMarker v : result.getVersions()) {
                System.out.println("Key:" + v.getKey());
                System.out.println("Owner:" + v.getOwner());
                System.out.println("isDeleteMarker:" + v.isDeleteMarker());
            }
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：指定数目列举多版本对象<a name="section103137452516"></a>

以下代码展示如何向examplebucket桶中指定数目列举多版本对象。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions002 {
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
            // 指定数目列举
            ListVersionsResult result = obsClient.listVersions("examplebucket", 100);
            System.out.println("listVersions successfully");
            for (VersionOrDeleteMarker v : result.getVersions()) {
                System.out.println("Key:" + v.getKey());
                System.out.println("Owner:" + v.getOwner());
                System.out.println("isDeleteMarker:" + v.isDeleteMarker());
            }
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：指定前缀列举多版本对象<a name="section53141645145118"></a>

以下代码展示如何指定带有prefix前缀列举examplebucket桶中的多版本对象，最大数目为100个。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsRequest;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions003 {
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
            // 指定前缀列举
            // 列举带有prefix前缀的100个多版本对象
            ListVersionsRequest request = new ListVersionsRequest("examplebucket", 100);
            request.setPrefix("prefix");
            ListVersionsResult result = obsClient.listVersions(request);
            System.out.println("listVersions successfully");
            for (VersionOrDeleteMarker v : result.getVersions()) {
                System.out.println("Key:" + v.getKey());
                System.out.println("Owner:" + v.getOwner());
                System.out.println("isDeleteMarker:" + v.isDeleteMarker());
            }
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：指定起始位置列举多版本对象<a name="section183151845125112"></a>

以下代码展示如何指定起始位置列举examplebucket桶中对象名字典序在test之后的100个多版本对象。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsRequest;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions004 {
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
            // 指定起始位置列举
            // 列举对象名字典序在"test"之后的100个多版本对象
            ListVersionsRequest request = new ListVersionsRequest("examplebucket", 100);
            request.setKeyMarker("test");
            ListVersionsResult result = obsClient.listVersions(request);
            System.out.println("listVersions successfully");
            for (VersionOrDeleteMarker v : result.getVersions()) {
                System.out.println("Key:" + v.getKey());
                System.out.println("Owner:" + v.getOwner());
                System.out.println("isDeleteMarker:" + v.isDeleteMarker());
            }
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：分页列举全部多版本对象<a name="section1031716453513"></a>

以下代码展示如何指定起始位置列举examplebucket桶中对象名字典序在test之后的100个多版本对象。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsRequest;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions005 {
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
            // 分页列举全部对象
            ListVersionsResult result;
            ListVersionsRequest request = new ListVersionsRequest("examplebucket", 100);
            do {
                result = obsClient.listVersions(request);
                System.out.println("listVersions successfully");
                for (VersionOrDeleteMarker v : result.getVersions()) {
                    System.out.println("Key:" + v.getKey());
                    System.out.println("Owner:" + v.getOwner());
                    System.out.println("isDeleteMarker:" + v.isDeleteMarker());
                }
                request.setKeyMarker(result.getNextKeyMarker());
                request.setVersionIdMarker(result.getNextVersionIdMarker());
            } while (result.isTruncated());
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：列举文件夹中的所有多版本对象<a name="section13191845105113"></a>

OBS本身是没有文件夹的概念的，桶中存储的元素只有对象。文件夹对象实际上是一个大小为0且对象名以“/”结尾的对象，将这个文件夹对象名作为前缀，即可模拟列举文件夹中对象的功能。以下代码展示如何列举文件夹中的多版本对象：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsRequest;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions006 {
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
            // 列举文件夹中的所有对象
            ListVersionsResult result;
            ListVersionsRequest request = new ListVersionsRequest("examplebucket", 100);
            // 设置文件夹对象名"dir/"为前缀
            request.setPrefix("dir/");
            do {
                result = obsClient.listVersions(request);
                System.out.println("listVersions successfully");
                for (VersionOrDeleteMarker v : result.getVersions()) {
                    System.out.println("Key:" + v.getKey());
                    System.out.println("Owner:" + v.getOwner());
                    System.out.println("isDeleteMarker:" + v.isDeleteMarker());
                }
                request.setKeyMarker(result.getNextKeyMarker());
                request.setVersionIdMarker(result.getNextVersionIdMarker());
            } while (result.isTruncated());
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：按文件夹分组列举所有多版本对象<a name="section1932111454510"></a>

以下代码展示如何按文件夹分组，列举examplebucket桶下的所有多版本对象：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListVersionsRequest;
import com.obs.services.model.ListVersionsResult;
import com.obs.services.model.VersionOrDeleteMarker;
public class ListVersions007 {
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
            // 按文件夹分组列举所有对象
            ListVersionsRequest request = new ListVersionsRequest("examplebucket", 1000);
            request.setDelimiter("/");
            ListVersionsResult result = obsClient.listVersions(request);
            System.out.println("listVersions successfully");
            System.out.println("Objects in the root directory:");
            for (VersionOrDeleteMarker v : result.getVersions()) {
                System.out.println("Key:" + v.getKey());
                System.out.println("Owner:" + v.getOwner());
                System.out.println("isDeleteMarker:" + v.isDeleteMarker());
            }
            listVersionsByPrefix(obsClient, result);
        } catch (ObsException e) {
            System.out.println("listVersions failed");
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
            System.out.println("listVersions failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
```

## 代码示例：递归列出子文件夹中多版本对象<a name="section52988344396"></a>

递归列出子文件夹中多版本对象的函数_listVersionsByPrefix_的示例代码如下：

```
    // 递归列出子文件夹中多版本对象
    static void listVersionsByPrefix(ObsClient obsClient, ListVersionsResult result) throws ObsException {
        for (String prefix : result.getCommonPrefixes()) {
            System.out.println("Objects in folder [" + prefix + "]:");
            ListVersionsRequest request = new ListVersionsRequest("examplebucket", 1000);
            request.setDelimiter("/");
            request.setPrefix(prefix);
            result = obsClient.listVersions(request);
            for (VersionOrDeleteMarker v : result.getVersions()) {
                System.out.println("Key:" + v.getKey());
                System.out.println("Owner:" + v.getOwner());
                System.out.println("isDeleteMarker:" + v.isDeleteMarker());
            }
            listVersionsByPrefix(obsClient, result);
        }
    }
}
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   以上代码示例不包含文件夹中多版本对象数超过1000个的情况。
>-   由于是需要列举出文件夹中的对象和子文件夹，且文件夹对象总是以“/”结尾，因此delimiter总是为“/”。
>-   每次递归的返回结果中ListVersionsResult.getVersions包含的是文件夹中的多版本对象；ListVersionsResult.getCommonPrefixes包含的是文件夹的子文件夹。

## 相关链接<a name="section72611512281"></a>

-   关于列举对象的其他说明，请参见[授权码列举对象](https://support.huaweicloud.com/utiltg-obs/obs_11_0063.html)。
-   更多关于列举多版本对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ListVersionsSample.java)。
-   获取桶列表过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

