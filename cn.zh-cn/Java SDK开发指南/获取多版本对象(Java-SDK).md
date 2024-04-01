# 获取多版本对象\(Java SDK\)<a name="obs_21_1004"></a>

## 功能说明<a name="section4772222164213"></a>

您可以通过ObsClient.getObject接口传入版本号（versionId）来获取桶中指定版本的对象。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section13191182151314"></a>

-   您必须是桶拥有者或拥有下载对象的权限，才能下载对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:GetObject权限，如果使用桶策略则需授予GetObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

-   对于存储类别为归档存储的对象，需要确认对象的状态为“已恢复”才能对其进行下载。

## 方法定义<a name="section54232412"></a>

obsClient.getObject\([GetObjectRequest](#table14455523) [request](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|GetObjectRequest|必选|**参数解释：**桶下载对象时请求参数，详见GetObjectRequest。|


**表 2**  GetObjectRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionId|String|可选|**参数解释：**对象的版本号。版本号为空，默认下载最新版本的对象。**取值范围：**长度为32的字符串。**默认取值：**无。|
|imageProcess|String|可选|**参数解释：**图片处理参数，描述针对对象的图片处理命令或处理样式。例如表示对图片依次进行缩放、旋转，取值：image/resize,m_fixed,w_100,h_100/rotate,90。**取值范围：**命令方式：image/命令参数。样式方式：style/样式名称。详细参数说明参见处理图片。**默认取值：**如果不输入处理命令，将返回原图。|
|rangeStart|Long|可选|**参数解释：**指定下载对象的起始位置。**取值范围：**非负整数。**默认取值：**无|
|rangeEnd|Long|可选|**参数解释：**指定下载对象的结束位置。**约束限制：**如果该值大于对象长度-1，实际仍取对象长度-1。**默认取值：**无|
|ifMatchTag|String|可选|**参数解释：**指定一个预设的Etag值，如果下载对象的ETag值与该参数值相同，则返回对象内容，否则返回错误。**取值范围：**长度为32的字符串。**默认取值：**无|
|ifNoneMatchTag|String|可选|**参数解释：**指定一个预设的Etag值，如果下载对象的ETag值与该参数值不相同，则返回对象内容，否则返回错误。**取值范围：**长度为32的字符串。**默认取值：**无|
|IfModifiedSince|Date|可选|**参数解释：**如果对象的修改时间晚于该参数值指定的时间，则返回对象内容，否则返回错误。**默认取值：**无|
|IfUnmodifiedSince|Date|可选|**参数解释：**如果对象的修改时间早于该参数值指定的时间，则返回对象内容，否则返回错误。**默认取值：**无|
|sseCHeader|SseCHeader|可选|**参数解释：**服务端解密头信息，详见SseCHeader。|
|replaceMetadata|ObjectRepleaceMetadata|可选|**参数解释：**指定OBS返回请求的相关信息，详见ObjectRepleaceMetadata。|
|progressListener|ProgressListener|可选|**参数解释**：设置数据传输监听器，用于获取下载进度，详见ProgressListener。|


**表 3**  ObjectRepleaceMetadata

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|contentType|String|可选|**参数解释：**对象的文件类型（MIME类型）。contentType（MIME）用于标识发送或接收数据的类型，浏览器根据该参数来决定数据的打开方式。**取值范围：**常见的contentType（MIME）列表参见如何理解Content-Type（MIME）？(Java SDK)。**默认取值：**无|
|contentLanguage|String|可选|**参数解释：**说明访问者希望采用的语言或语言组合，以根据自己偏好的语言来定制。详情请参见HTTP协议中关于ContentLanguage的定义。**默认取值：**无|
|expires|String|可选|**参数解释：**响应中的Expires头。指定对象被下载时的网页的缓存过期时间。**默认取值：**无|
|cacheControl|String|可选|**参数解释：**响应中的Cache-Control头，指定对象被下载时的网页的缓存行为。**默认取值：**无|
|contentDisposition|String|可选|**参数解释：**为请求的对象提供一个默认的文件名赋值给该对象，当下载对象或者访问对象时，以默认文件名命名的文件将直接在浏览器上显示或在访问时弹出文件下载对话框。**默认取值：**无|
|contentEncoding|String|可选|**参数解释：**响应中的Content-Encoding头。指定对象被下载时的内容编码格式。**默认取值：**无|


**表 4**  ProgressListener\(传输进度接口\)成员如下

|**方法名称**|**返回值类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressChanged|void|必选|**参数解释：**获取上传进度，详见progressChanged。**默认取值：**无|


**表 5**  progressChanged参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|status|ProgressStatus|必选|**参数解释：**传输进度数据，详见ProgressStatus。**默认取值：**无|


**表 6**  ProgressStatus方法

|**方法名称**|**返回值类型**|**说明**|
|--|--|--|
|getAverageSpeed()|double|上传平均速率。|
|getInstantaneousSpeed()|double|上传瞬时速率。|
|getTransferPercentage()|int|上传进度百分比。|
|getNewlyTransferredBytes()|long|新增的字节数。|
|getTransferredBytes()|long|已传输的字节数。|
|getTotalBytes()|long|待传输的字节数。|


**表 7**  SseCHeader

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|algorithm|ServerAlgorithm|必选|**参数解释：**表示服务端加密是SSE-C方式，对象使用SSE-C加密方式。**取值范围：**可选值：AES256，即选择SSE-C方式，使用高级加密标准（Advanced Encryption Standard，AES）加密对象。详见ServerAlgorithm。**默认取值：**无|
|sseAlgorithm|SSEAlgorithmEnum|可选|**参数解释：**加密算法。**约束限制：**只支持AES256。**取值范围：**详见SSEAlgorithmEnum。**默认取值：**无|
|sseCKey|byte[]|必选|**参数解释：**SSE-C方式下加密使用的原始密钥，byte[]形式，该密钥用于加密对象。**默认取值：**无|
|sseCKeyBase64|String|可选|**参数解释：**SSE-C方式下的密钥，由原始密钥经过Base64编码后得到，该密钥用于加密对象。**默认取值：**无|


**表 8**  SSEAlgorithmEnum

|**常量值**|**原始值**|
|--|--|
|KMS|kms|
|AES256|AES256|


**表 9**  ServerAlgorithm

|**常量值**|**原始值**|
|--|--|
|AES256|AES256|


**表 10**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 11**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 12**  ObjectMetadata

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


## 返回结果说明<a name="section1275864334715"></a>

**表 13**  ObsObject

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|bucketName|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|owner|Owner|**参数解释：**所有者，详见Owner。|
|metadata|ObjectMetadata|**参数解释：**对象元数据，详见ObjectMetadata。|
|objectContent|InputStream|**参数解释：**对象数据流。**默认取值：**无|


## 代码示例<a name="section17365124615456"></a>

以下代码展示了如何通过设置versionId获取多版本对象查看examplebucket桶内对象objectname的多版本状态。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ObsObject;
public class GetObject001 {
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
            // 设置versionId获取多版本对象
            ObsObject obsObject = obsClient.getObject("examplebucket", "objectname", "versionid1");
            System.out.println("getObject successfully");
            obsObject.getObjectContent().close();
        } catch (ObsException e) {
            System.out.println("getObject failed");
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
            System.out.println("getObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于下载多版本对象的API说明，请参见[获取多版本对象内容](https://support.huaweicloud.com/api-obs/obs_04_0083.html)。
-   下载对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   下载多版本对象常见问题请参见[下载对象失败](https://support.huaweicloud.com/obs_faq/obs_faq_0135.html)。

