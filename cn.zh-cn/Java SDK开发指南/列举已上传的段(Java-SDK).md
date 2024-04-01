# 列举已上传的段\(Java SDK\)<a name="obs_21_0620"></a>

## 功能说明<a name="section31929956"></a>

通过分段上传任务的ID，列举指定桶中已上传的段。

您可以列出特定多段上传任务或所有正在进行的多段上传任务的分段。列举已上传的段操作将返回特定多段上传任务中正在进行上传的段信息，单次最多列举1000个分段。如果多段上传中的段超过1000个，您必须发送一系列列举已上传的段请求以检索所有段。请注意，返回的分段列表不包括已合并的分段。

## 接口约束<a name="section1920312338358"></a>

-   您必须是桶拥有者或拥有列举已上传的段的权限，才能列举已上传的段。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:ListMultipartUploadParts权限，如果使用桶策略则需授予ListMultipartUploadParts权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section13130317121018"></a>

obsClient.listParts\([ListPartsRequest](#table9747247160) [request](#table97462410166)\)

## 请求参数说明<a name="section9139191514158"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|ListPartsRequest|必选|**参数解释：**列举上传段请求参数，详见ListPartsRequest。|


**表 2**  ListPartsRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|uploadId|String|必选|**参数解释：**分段上传任务的ID，例如：000001648453845DBB78F2340DD460D8**取值范围：**长度大于0且不超过32的字符串。**默认取值：**无|
|maxParts|Integer|可选|**参数解释：**列举已上传段的返回结果最大段数目，即分页时每一页中段数目。**约束限制：**如果该参数超出1000时，则按照默认的1000进行处理。**取值范围：**[1，1000]**默认取值：**1000|
|partNumberMarker|Integer|可选|**参数解释：**列举已上传段的起始位置。**约束限制：**只有PartNumber数目大于该参数的段会被列出**默认取值：**无|
|encodingType|String|可选|**参数解释：**对响应中的对象名key进行指定类型的编码。如果key包含xml 1.0标准不支持的控制字符，可通过设置该参数对响应中的key进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|


## 返回结果说明<a name="section2426112416366"></a>

**表 3**  ListPartsResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|bucket|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|key|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|uploadId|String|**参数解释：**分段上传任务的ID，例如：000001648453845DBB78F2340DD460D8**取值范围：**长度为32的字符串。**默认取值：**无|
|initiator|Owner|**参数解释：**分段上传任务的创建者，详见Owner。**默认取值：**无|
|owner|Owner|**参数解释：**和initiator相同，代表分段上传任务的创建者，详见Owner。**默认取值：**无|
|storageClass|StorageClassEnum|**参数解释：**分段上传的对象的存储类别。**取值范围：**存储类别取值范围参见StorageClassEnum。**默认取值：**无|
|multipartList|List<Multipart>|**参数解释：**已上传段信息列表，详见Multipart。**默认取值：**无|
|maxParts|Integer|**参数解释：**列举段的返回结果最大段数目，与请求中的该参数对应。列举已上传段的返回结果最大段数目，即分页时每一页中段数目。**约束限制：**如果该参数超出取值范围时，按照默认的1000进行处理。**取值范围：**[1，1000]**默认取值：**1000|
|isTruncated|boolean|**参数解释：**表明本次请求是否返回了全部结果。**取值范围：**true：表示没有返回全部结果。false：表示已返回了全部结果。**默认取值：**无|
|partNumberMarker|String|**参数解释：**列举段的起始位置，与请求中的该参数对应。**默认取值：**无|
|nextPartNumberMarker|String|**参数解释：**下次列举段请求的起始位置。如果本次没有返回全部结果，响应请求中将包含此字段，用于标明接下来请求的partNumberMarker值。**默认取值：**无|


**表 4**  Multipart

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|partNumber|Integer|**参数解释：**段号。**取值范围：**取值范围是[1,10000]的非负整数。**默认取值：**无|
|lastModified|Date|**参数解释：**段的最后上传时间。**默认取值：**无|
|etag|String|**参数解释：**段的ETag值。分段的base64编码的128位MD5摘要。**取值范围：**长度为32的字符串。**默认取值：**无|
|size|Long|**参数解释：**段的大小。**默认取值：**无|


**表 5**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 6**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


## 代码示例：简单列举已上传的段（最多1000个）<a name="section888184412138"></a>

通过initiateMultipartUpload获取的uploadId对examplebucket桶下的objectname对象进行上传段的简单列举，至多列举1000个段。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListPartsRequest;
import com.obs.services.model.ListPartsResult;
import com.obs.services.model.Multipart;
public class ListParts001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("SECURITY_TOKEN");
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
            String uploadId = "upload id from initiateMultipartUpload";
            // 列举已上传的段，其中uploadId来自于initiateMultipartUpload
            ListPartsRequest request = new ListPartsRequest("examplebucket", "objectname");
            request.setUploadId(uploadId);
            ListPartsResult result = obsClient.listParts(request);
            for (Multipart part : result.getMultipartList()) {
                // 分段号，上传时候指定
                System.out.println("PartNumber:" + part.getPartNumber());
                // 段数据大小
                System.out.println("Size:" + part.getSize());
                // 分段的ETag值
                System.out.println("Etag:" + part.getEtag());
                // 段的最后上传时间
                System.out.println("LastModified:" + part.getLastModified());
            }
            System.out.println("listParts successfully");
        } catch (ObsException e) {
            System.out.println("listParts failed");
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
            System.out.println("listParts failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：列举所有已上传的段<a name="section16897171272915"></a>

由于ObsClient.listParts只能列举至多1000个段，如果列举段数量大于1000个，可采用分页全部列举。示例如下：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListPartsRequest;
import com.obs.services.model.ListPartsResult;
import com.obs.services.model.Multipart;
public class ListParts002 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("SECURITY_TOKEN");
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
            String uploadId = "upload id from initiateMultipartUpload";
            // 列举所有已上传的段，其中uploadId来自于initiateMultipartUpload
            ListPartsRequest request = new ListPartsRequest("examplebucket", "objectname");
            request.setUploadId(uploadId);
            ListPartsResult result;
            do {
                result = obsClient.listParts(request);
                for (Multipart part : result.getMultipartList()) {
                    // 分段号，上传时候指定
                    System.out.println("PartNumber:" + part.getPartNumber());
                    // 段数据大小
                    System.out.println("Size:" + part.getSize());
                    // 分段的ETag值
                    System.out.println("Etag:" + part.getEtag());
                    // 段的最后上传时间
                    System.out.println("LastModified:" + part.getLastModified());
                }
                request.setPartNumberMarker(Integer.parseInt(result.getNextPartNumberMarker()));
            } while (result.isTruncated());
            System.out.println("listParts successfully");
        } catch (ObsException e) {
            System.out.println("listParts failed");
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
            System.out.println("listParts failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于分段上传-列举已上传的段的API说明，请参见[列举已上传的段](https://support.huaweicloud.com/api-obs/obs_04_0101.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentUploadPartSample.java#L276)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

