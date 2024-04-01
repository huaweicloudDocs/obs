# 断点续传下载\(Java SDK\)<a name="obs_21_0709"></a>

## 功能说明<a name="section843754815437"></a>

1.  当下载大对象到本地文件时，经常出现因网络不稳定或程序崩溃导致下载失败的情况。失败后再次重新下载不仅浪费资源，而且当网络不稳定时仍然有下载失败的风险。断点续传下载接口能有效地解决此类问题引起的下载失败，其原理是将待下载的对象分成若干个分段分别下载，并实时地将每段下载结果统一记录在checkpoint文件中，仅当所有分段都下载成功时返回下载成功的结果，否则抛出异常提醒用户再次调用接口进行重新下载（重新下载时因为有checkpoint文件记录当前的下载进度，避免重新下载所有分段，从而节省资源提高效率）。
2.  断点续传下载接口是利用[范围下载\(Java SDK\)](范围下载(Java-SDK).md)特性实现的，是对范围下载的封装和加强。
3.  断点续传下载接口不仅能在失败重下时节省资源提高效率，还因其对分段进行并发下载的机制能加快下载速度，帮助用户快速完成下载业务；且其对用户透明，用户不用关心checkpoint文件的创建和删除、分段任务的切分、并发下载的实现等内部细节。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section118114249370"></a>

-   您必须是桶拥有者或拥有下载对象的权限，才能下载对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:GetObject权限，如果使用桶策略则需授予GetObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.downloadFile\([DownloadFileRequest](#table14455523) [request](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|DownloadFileRequest|必选|**参数解释：**下载大对象请求参数列表，详见DownloadFileRequest。|


**表 2**  DownloadFileRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|downloadFile|String|可选|**参数解释：**下载对象的本地文件全路径。**默认取值：**当该值为空时，默认为当前程序的运行目录。|
|partSize|long|可选|**参数解释：**分段大小。**取值范围：**取值范围是100KB~5GB，单位：字节。**默认取值：**9MB|
|taskNum|int|可选|**参数解释：**分段下载时的最大并发数。**取值范围：**(0, 文件大小/分段大小]，即大于0小于等于文件大小除以分段大小向上取整。**默认取值：**1，即不设置则默认单任务下载。|
|enableCheckpoint|boolean|可选|**参数解释：**是否开启断点续传模式。**取值范围：**true：开启断点续传模式。false：关闭断点续传模式。**默认取值：**false|
|checkpointFile|String|可选|**参数解释：**断点续传过程中，会生成一个进度记录文件，文件中会记录段的上传进度和段的相关信息。checkpointFile参数为该记录文件的文件路径。**约束限制：**仅在断点续传模式下有效。**默认取值：**当该值为空时，默认为当前目录。|
|enableCheckSum|boolean|可选|**参数解释：**是否校验待上传文件的内容，如果开启该参数，会在每次任务重新开始前对待上传文件进行校验，验证是否与任务初始化时使用文件为同一文件。**约束限制：**仅在断点续传模式下有效。**取值范围：**true：校验待上传文件的内容。false：不校验待上传文件的内容。**默认取值：**false|
|versionId|String|可选|**参数解释：**对象的版本号，用于获取指定版本号的对象。例如：G001117FCE89978B0000401205D5DC9。**取值范围：**长度为32的字符串。**默认取值：**无，如果不设置则默认获取最新版本的对象。|
|encodeHeaders|boolean|可选|**参数解释：**是否自动解码响应头**默认取值：**无|
|ifModifiedSince|Date|可选|**参数解释：**如果对象的修改时间晚于该参数值指定的时间，则返回对象内容，否则返回错误。**默认取值：**无|
|ifUnmodifiedSince|Date|可选|**参数解释：**如果对象的修改时间早于该参数值指定的时间，则返回对象内容，否则返回错误。**默认取值：**无|
|ifMatchTag|String|可选|**参数解释：**如果对象的ETag值与该参数值相同，则返回对象内容，否则抛出异常。**默认取值：**无|
|ifNoneMatchTag|String|可选|**参数解释：**如果对象的ETag值与该参数值不相同，则返回对象内容，否则抛出异常。**默认取值：**无|
|progressListener|ProgressListener|可选|**参数解释：**设置数据传输监听器，用于获取下载进度。详见ProgressListener。|
|encodeHeaders|boolean|可选|**参数解释：**是否开启OBS对请求头域的自动编码。由于HTTP编码规范限制，无法发送非ASCII码字符，SDK会在发送请求时对您头域中的**中文汉字**进行url编码，发送编码后数据。如您设置的值content-disposition为“attachment; filename="中文.txt"”，则对象元数据中存储的信息为“attachment; filename="%E4%B8%AD%E6%96%87.txt"”。使用浏览器访问时浏览器将会自动解码。**取值范围：**true：启用SDK编码。false：不启用SDK编码。**默认取值：**true|


**表 3**  ProgressListener\(传输进度接口\)成员如下

|**方法名称**|**返回值类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressChanged|void|必选|**参数解释：**获取上传进度，详见progressChanged**默认取值：**无|


**表 4**  progressChanged参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|status|ProgressStatus|必选|**参数解释：**传输进度数据，详见ProgressStatus**默认取值：**无|


**表 5**  ProgressStatus方法

|**方法名称**|**返回值类型**|**说明**|
|--|--|--|
|getAverageSpeed()|double|上传平均速率。|
|getInstantaneousSpeed()|double|上传瞬时速率。|
|getTransferPercentage()|int|上传进度百分比。|
|getNewlyTransferredBytes()|long|新增的字节数。|
|getTransferredBytes()|long|已传输的字节数。|
|getTotalBytes()|long|待传输的字节数。|


**表 6**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 7**  ObjectMetadata

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|contentLength|Long|可选|**参数解释：**对象数据的长度。**默认取值：**如果不设置，则SDK会自动计算对象数据的长度。|
|contentType|String|可选|**参数解释：**对象的文件类型（MIME类型）。contentType（MIME）用于标识发送或接收数据的类型，浏览器根据该参数来决定数据的打开方式。**取值范围：**常见的contentType（MIME）列表参见如何理解Content-Type（MIME）？(Java SDK)。**默认取值：**如果未指定Content-Type，SDK会根据指定Object名称的后缀来判定文件类型并自动填充Content-Type（如.xml判断为application/xml文件；.html判断为text/html文件）。|
|contentEncoding|String|可选|**参数解释：**响应中的Content-Encoding头。指定对象内容编码格式。**默认取值：**无|
|contentDisposition|String|可选|**参数解释：**为请求的对象提供一个默认的文件名赋值给该对象，当下载对象或者访问对象时，以默认文件名命名的文件将直接在浏览器上显示，或在弹出文件下载对话框时显示。**默认取值：**无|
|cacheControl|String|可选|**参数解释：**响应中的Cache-Control头。指定对象被下载时的网页的缓存行为。**默认取值：**无|
|contentLanguage|String|可选|**参数解释：**说明访问者希望采用的语言或语言组合，以根据自己偏好的语言来定制。详情请参见HTTP协议中关于ContentLanguage的定义。**默认取值：**无|
|expires|String|可选|**参数解释：**指对象在网页中的缓存过期时间。**约束限制：**日期格式为GMT的格式。**默认取值：**无|
|contentMd5|String|可选|**参数解释：**对象数据的MD5值（经过Base64编码），提供给OBS服务端，校验数据完整性。OBS服务端会将该MD5值与对象数据计算出的MD5值进行对比，如果不匹配，返回HTTP 400错误。**约束限制：**对象数据的MD5值必须经过Base64编码。如果不设置对象的MD5值，OBS服务端会忽略对对象数据的MD5值校验。**取值范围：**按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过Base64编码后得到的字符串。示例：n58IG6hfM7vqI4K0vnWpog==**默认取值：**无|
|storageClass|StorageClassEnum|可选|**参数解释：**对象的存储类别。创建对象时，可以加上此头域设置对象的存储类别。如果未设置此头域，则以桶的默认存储类别作为对象的存储类别。**取值范围：**可选择的存储类别参见StorageClassEnum。**默认取值：**无|
|webSiteRedirectLocation|String|可选|**参数解释：**当桶设置了Website配置，可以将获取这个对象的请求重定向到桶内另一个对象或一个外部的URL，该参数指明对象的重定向地址。例如，重定向请求到桶内另一对象：WebsiteRedirectLocation:/anotherPage.html或重定向请求到一个外部URL：WebsiteRedirectLocation:http://www.example.com/**约束限制：**必须以“/”、“http://”或“https://”开头，长度不超过2KB。OBS仅支持为桶根目录下的对象设置重定向，不支持为桶中文件夹下的对象设置重定向。**默认取值：**无|
|nextPosition|long|可选|**参数解释：**下次追加上传的位置。**取值范围：**0~对象长度，单位：字节。**默认取值：**无|
|appendable|boolean|可选|**参数解释：**对象是否为可追加上传的对象。**取值范围：**true：是，可追加上传。false：否，不可追加上传。**默认取值：**无|
|userMetadata|Map<String, Object>|可选|**参数解释：**对象的自定义元数据，OBS支持用户使用以“x-obs-meta-”开头的消息头来加入自定义的元数据，以便对对象进行自定义管理。Map中的String代表以“x-obs-meta-”开头的自定义元数据名称，Object代表自定义元数据的值。对象的自定义元数据可以通过ObsClient.getObjectMetadata获取，参见获取对象元数据。**约束限制：**一个对象可以有多个元数据，总大小不能超过8KB。使用ObsClient.getObject下载对象时，对象的自定义元数据也会同时下载。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 8**  DownloadFileResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|objectMetadata|ObjectMetadata|**参数解释：**对象元数据，详见ObjectMetadata。|


## 代码示例<a name="section6384172717422"></a>

本示例展示了使用断点续传方式将examplebucket桶里的objectname对象下载到本地文件localfile中。示例代码如下：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.DownloadFileRequest;
import com.obs.services.model.DownloadFileResult;
public class DownloadFile001 {
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
            DownloadFileRequest request = new DownloadFileRequest("examplebucket", "objectname");
            // 设置下载对象的本地文件路径
            request.setDownloadFile("localfile");
            // 设置分段下载时的最大并发数
            request.setTaskNum(5);
            // 设置分段大小为10MB
            request.setPartSize(10 * 1024 * 1024);
            // 开启断点续传模式
            request.setEnableCheckpoint(true);
            // 进行断点续传下载
            DownloadFileResult result = obsClient.downloadFile(request);
            System.out.println("downloadFile successfully");
            System.out.println("Etag:" + result.getObjectMetadata().getEtag());
        } catch (ObsException e) {
            System.out.println("downloadFile failed");
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
            System.out.println("downloadFile failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于下载对象的API说明，请参见[获取对象内容](https://support.huaweicloud.com/api-obs/obs_04_0083.html)。
-   更多关于下载对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/DownloadSample.java)。
-   下载对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   下载对象常见问题请参见[下载对象失败](https://support.huaweicloud.com/obs_faq/obs_faq_0135.html)。

