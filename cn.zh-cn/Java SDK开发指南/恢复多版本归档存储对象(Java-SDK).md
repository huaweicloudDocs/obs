# 恢复多版本归档存储对象\(Java SDK\)<a name="obs_21_1006"></a>

## 功能说明<a name="section1691145214573"></a>

如果要下载归档存储对象，需要先将归档存储对象恢复。恢复归档存储对象的恢复选项可支持两类，见[RestoreTierEnum](#obs_21_0708_table81731855162317)：

您可以通过ObsClient.restoreObject接口传入版本号（versionId）来恢复多版本归档存储对象。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section1011804420594"></a>

-   您必须是桶拥有者或拥有恢复归档存储对象的权限，才能恢复归档存储对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:RestoreObject权限，如果使用桶策略则需授予RestoreObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的Region与Endpoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   ObsClient.restoreObject中指定的对象必须是归档存储类别，否则调用该接口会抛出异常。

>![](public_sys-resources/icon-caution.gif) **注意：** 
>重复恢复归档存储数据时在延长恢复有效期的同时，也将会对恢复时产生的恢复费用进行重复收取。产生的标准存储类别的对象副本有效期将会延长，并且收取延长时间段产生的标准存储副本费用。

## 方法定义<a name="section54232412"></a>

obsClient.restoreObject\([RestoreObjectRequest](#obs_21_0708_table14455523) [request](#obs_21_0708_table1210700)\)

## 请求参数说明<a name="section1719101014013"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|RestoreObjectRequest|必选|**参数解释：**恢复多版本归档存储对象请求参数，详见RestoreObjectRequest。|


**表 2**  RestoreObjectRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionId|String|可选|**参数解释：**待恢复归档存储对象的版本号。**取值范围：**长度为32的字符串。**默认取值：**无，如果不设置则默认指定最新版本的对象。|
|days|int|必选|**参数解释：**恢复对象后，会生成一个对象的标准存储副本，此参数指定恢复有效期，即标准存储副本的保存时间。**约束限制：**取值必须是正整数。**取值范围：**[1, 30]，单位：天。**默认取值：**无|
|tier|RestoreTierEnum|可选|**参数解释：**恢复选项，表示恢复对象所耗的时间。**取值范围：**详见RestoreTierEnum。**默认取值：**默认取值为标准恢复。|


**表 3**  RestoreTierEnum

|**可选值**|**原始值**|**描述**|
|--|--|--|
|EXPEDITED|Expedited|快速恢复，恢复耗时1~5分钟。|
|STANDARD|Standard|标准恢复，恢复耗时3~5小时。|


## 返回结果说明<a name="section1541117471006"></a>

**表 4**  RestoreObjectStatus

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section112870191519"></a>

使用快速恢复方式，恢复多版本对象，其中桶名为examplebucket，桶中对象为objectname，保留时间为1天。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ObsObject;
import com.obs.services.model.RestoreObjectRequest;
import com.obs.services.model.RestoreTierEnum;
public class RestoreObject001 {
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
            // 使用快速恢复方式，恢复多版本对象
            RestoreObjectRequest request = new RestoreObjectRequest("examplebucket", "objectname", 1);
            request.setRestoreTier(RestoreTierEnum.EXPEDITED);
            request.setVersionId("versionid");
            obsClient.restoreObject(request);
            System.out.println("RestoreObject successfully");
        } catch (ObsException e) {
            System.out.println("RestoreObject failed");
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
            System.out.println("RestoreObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于恢复归档存储对象的API说明，请参见[恢复归档存储对象](https://support.huaweicloud.com/api-obs/obs_04_0087.html)。
-   更多关于恢复归档存储对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/RestoreObjectSample.java)。
-   恢复归档存储对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

