# 列举分段上传任务\(Java SDK\)<a name="obs_21_0621"></a>

## 功能说明<a name="section40604315"></a>

列举指定桶中所有的初始化后还未合并或还未取消的分段上传任务。

通过列举桶中的多段上传任务，您可以获得已初始化多段上传任务的列表，已初始化多段上传任务是指初始化后还未合并以及未取消的多段上传任务。每个请求将返回最多1000个多段上传任务，如果正在进行的多段上传任务超过1000个，您需要发送其他请求以检索剩余的多段上传任务。

## 接口约束<a name="section74537595258"></a>

-   您必须是桶拥有者或拥有列举分段上传任务的权限，才能列举分段上传任务。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:ListBucketMultipartUploads权限，如果使用桶策略则需授予ListBucketMultipartUploads权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   默认情况下，允许桶所有者和多段上传任务的发起者执行此操作。除了默认情况之外，桶所有者可以允许其他委托人对桶执行_ListBucketMultipartUploads_操作。

## 方法定义<a name="section1651192020561"></a>

obsClient.listMultipartUploads\([ListMultipartUploadsRequest](#table1939650185220) [request](#table1939612065219)\)

## 请求参数说明<a name="section185581371117"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|ListMultipartUploadsRequest|必选|**参数解释：**列举上传段请求参数，详见ListMultipartUploadsRequest。|


**表 2**  ListMultipartUploadsRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|prefix|String|可选|**参数解释：**限定返回的分段上传任务中的对象名必须带有prefix前缀。例如，假设您拥有以下对象：logs/day1、logs/day2、logs/day3和ExampleObject.jpg。如果您将logs/指定为前缀，将返回以字符串“logs/”开头的三个对象所在的分段上传任务。如果您指定空的前缀且请求中没有其他过滤条件，将返回桶中的所有分段上传任务。**约束限制：**长度大于0且不超过1024的字符串。**默认取值：**无|
|delimiter|String|可选|**参数解释：**对分段上传任务中的对象名进行分组的字符。通常与前缀prefix搭配使用，如果指定了prefix，从prefix到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条commonPrefixes；如果没有指定prefix，从对象名的首字符到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条commonPrefixes。例如，桶中有3个对象，分别为abcd、abcde、bbcde。如果指定delimiter为d，prefix为a，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefixes；如果只指定delimiter为d，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefixes，而bbcde会被单独分成一组，形成一条前缀为bbcd的commonPrefixes。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|maxUploads|Integer|可选|**参数解释：**列举分段上传任务的最大数目。**约束限制：**当该参数超出1000时，按照默认的1000进行处理。**取值范围：**1~1000，单位：个。**默认取值：**1000|
|keyMarker|String|可选|**参数解释：**列举分段上传任务的起始位置。表示列举时返回指定的keyMarker之后的分段上传任务。**取值范围：**上次请求返回体的nextKeyMarker值。**默认取值：**无|
|uploadIdMarker|String|可选|**参数解释：**列举分段上传任务的起始位置（uploadId标识）。**约束限制：**只有与keyMarker参数一起使用时才有意义，即列举时返回指定keyMarker的uploadIdMarker之后的分段上传任务。**取值范围：**对象的分段上传任务ID，即上次请求返回体的nextUploadIdMarker值。**默认取值：**无|
|encodingType|String|可选|**参数解释：**响应中的部分元素进行指定类型的编码。如果 delimiter、keyMarker、prefix、nextKeyMarker 和 objectKey 包含xml 1.0标准不支持的控制字符，可通过设置 encodingType 对响应中的 delimiter、keyMarker、prefix（包括commonPrefixes 中的 prefix）、nextKeyMarker 和 objectKey 进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|


## 返回结果说明<a name="section8659182772410"></a>

**表 3**  MultipartUploadListing

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|bucket|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|keyMarker|String|**参数解释：**列举分段上传任务的起始位置，与请求中的该参数对应。表示列举时返回指定的keyMarker之后的分段上传任务。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|uploadIdMarker|String|**参数解释：**列举分段上传任务的起始位置（uploadId标识），与请求中的该参数对应。**取值范围：**长度大于0且不超过32的字符串。**默认取值：**无|
|nextKeyMarker|String|**参数解释：**下次列举分段上传任务请求的起始位置。如果本次没有返回全部结果，响应请求中将包含该元素，用于标明接下来请求的keyMarker值。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|nextUploadIdMarker|String|**参数解释：**下次列举分段上传任务请求的起始位置（uploadId标识）。与nextKeyMarker配合使用。如果本次没有返回全部结果，响应请求中将包含该元素，用于标明接下来请求的uploadIdMarker值。**取值范围：**长度大于0且不超过32的字符串。**默认取值：**无|
|prefix|String|**参数解释：**分段上传任务中的对象名前缀，与请求中的该参数对应。限定返回的分段上传任务中的对象名必须带有prefix前缀。例如，假设您拥有以下对象：logs/day1、logs/day2、logs/day3和ExampleObject.jpg。如果您将logs/指定为前缀，将返回以字符串“logs/”开头的三个对象所在的分段上传任务。如果您指定空的前缀且请求中没有其他过滤条件，将返回桶中的所有分段上传任务。**约束限制：**长度大于0且不超过1024的字符串。**默认取值：**无|
|maxUploads|int|**参数解释：**列举分段上传任务的最大数目，与请求中的该参数对应。**约束限制：**当该参数超出范围时，按照默认的1000进行处理。**取值范围：**1~1000，单位：个。**默认取值：**1000|
|truncated|boolean|**参数解释：**表明本次请求是否返回了全部结果。**取值范围：**true：表示没有返回全部结果。false：表示已返回了全部结果。**默认取值：**无|
|multipartTaskList|List<MultipartUpload>|**参数解释：**桶内分段上传任务列表，详见MultipartUpload。|
|delimiter|String|**参数解释：**用于对分段上传任务中的对象名进行分组的字符，与请求中的该参数对应。通常与前缀prefix搭配使用，如果指定了prefix，从prefix到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条commonPrefixes；如果没有指定prefix，从对象名的首字符到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条commonPrefixes。例如，桶中有3个对象，分别为abcd、abcde、bbcde。如果指定delimiter为d，prefix为a，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefixes；如果只指定delimiter为d，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefixes，而bbcde会被单独分成一组，形成一条前缀为bbcd的commonPrefixes。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|commonPrefixes|String[]|**参数解释：**当请求中设置了delimiter分组字符时，返回按Delimiter分组后的对象名称前缀列表。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|


**表 4**  MultipartUpload

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|bucketName|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|uploadId|String|**参数解释：**分段上传任务的ID，例如：000001648453845DBB78F2340DD460D8**取值范围：**长度大于0且不超过32的字符串。**默认取值：**无|
|initiatedDate|java.util.Date|**参数解释：**分段上传任务的初始化时间。**约束限制：**日期格式必须为ISO8601的格式。**默认取值：**无|
|storageClass|StorageClassEnum|**参数解释：**分段上传的对象的存储类别。**取值范围：**存储类别取值范围参见StorageClassEnum。**默认取值：**无|
|initiator|Owner|**参数解释：**分段上传任务的创建者，详见Owner。|
|owner|Owner|**参数解释：**和initiator相同，代表分段上传任务的创建者，详见Owner。|


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


## 代码示例：简单列举分段上传任务<a name="section72101939644"></a>

对examplebucket桶进行简单列举分段上传任务，至多返回1000个任务信息。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListMultipartUploadsRequest;
import com.obs.services.model.MultipartUpload;
import com.obs.services.model.MultipartUploadListing;
public class ListMultipartUploads001 {
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
            ListMultipartUploadsRequest request = new ListMultipartUploadsRequest("examplebucket");
            MultipartUploadListing result = obsClient.listMultipartUploads(request);
            for (MultipartUpload upload : result.getMultipartTaskList()) {
                System.out.println("UploadId:" + upload.getUploadId());
                System.out.println("ObjectKey:" + upload.getObjectKey());
                System.out.println("InitiatedDate:" + upload.getInitiatedDate());
            }
            System.out.println("ListMultipartUploads successfully");
        } catch (ObsException e) {
            System.out.println("ListMultipartUploads failed");
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
            System.out.println("ListMultipartUploads failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：分页列举所有已上传的段任务<a name="section18360439131520"></a>

由于ObsClient.listMultipartUploads只能列举至多1000个任务信息，如果列举段任务信息数量大于1000个，可采用分页全部列举。示例如下：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListMultipartUploadsRequest;
import com.obs.services.model.MultipartUpload;
import com.obs.services.model.MultipartUploadListing;
public class ListMultipartUploads002 {
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
            ListMultipartUploadsRequest request = new ListMultipartUploadsRequest("examplebucket");
            MultipartUploadListing result;
            do {
                result = obsClient.listMultipartUploads(request);
                for (MultipartUpload upload : result.getMultipartTaskList()) {
                    System.out.println("UploadId:" + upload.getUploadId());
                    System.out.println("ObjectKey:" + upload.getObjectKey());
                    System.out.println("InitiatedDate:" + upload.getInitiatedDate());
                }
                request.setKeyMarker(result.getNextKeyMarker());
                request.setUploadIdMarker(result.getNextUploadIdMarker());
            } while (result.isTruncated());
            System.out.println("ListMultipartUploads successfully");
        } catch (ObsException e) {
            System.out.println("ListMultipartUploads failed");
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
            System.out.println("ListMultipartUploads failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于分段上传-列举分段上传任务的API说明，请参见[列举桶中已初始化多段任务](https://support.huaweicloud.com/api-obs/obs_04_0097.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentUploadPartSample.java#L276)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

