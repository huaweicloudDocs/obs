# 设置桶存储类别\(Java SDK\)<a name="obs_21_0411"></a>

## 功能说明<a name="section6703932"></a>

OBS提供了三种四种存储类别：标准存储、低频访问存储、归档存储、深度归档存储（受限公测中），从而满足客户业务对存储性能、成本的不同诉求，详情可参见OBS存储类别存储类别存储类别。

调用设置桶存储类别接口，可设置指定桶的存储类别。设置了桶的默认存储类别之后，如果上传对象、复制对象和初始化多段上传任务时未指定对象的存储类别，则该对象的存储类别默认与桶的存储类别保持一致。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

桶的存储类别分为三类，见下表：

|**类型**|**说明**|**OBS Java SDK对应值**|
|--|--|--|
|标准存储|标准存储拥有低访问时延和较高的吞吐量，适用于有大量热点对象（平均一个月多次）或小对象（<1MB），且需要频繁访问数据的业务场景。|StorageClassEnum.STANDARD|
|低频访问存储|低频访问存储适用于不频繁访问（平均一年少于12次）但在需要时也要求能够快速访问数据的业务场景。|StorageClassEnum.WARM|
|归档存储|归档存储适用于很少访问（平均一年访问一次）数据的业务场景。|StorageClassEnum.COLD|


更多关于桶存储类别的内容请参考[桶的存储类别](https://support.huaweicloud.com/ugobs-obs/obs_41_0006.html)。

## 接口约束<a name="section16603205942210"></a>

-   您必须是桶拥有者或拥有设置桶存储类别的权限，才能设置桶存储类别。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:PutBucketStoragePolicy权限，如果使用桶策略则需授予PutBucketStoragePolicy权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   桶的存储类别与桶中对象的存储类别是相互独立的。如果上传对象时，未设置对象的存储类别，该对象默认与桶的存储类别一致，但后续如果修改桶的存储类别，已上传的桶中对象的存储类别不会随之改变；如果后续修改桶中对象的存储类别时，该桶的存储类别也不会随之改变。

## 方法定义<a name="section54232412"></a>

obsClient.setBucketStoragePolicy\(String  [bucketName](#table14455523),  [BucketStoragePolicyConfiguration](#table94701456392) [bucketStorage](#table14455523)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  参数列表说明

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|bucketStorage|BucketStoragePolicyConfiguration（继承HeaderResponse）|必选|**参数解释：**桶的存储类别。**取值范围：**存储类别取值详见BucketStoragePolicyConfiguration。**默认取值：**无|


**表 2**  BucketStoragePolicyConfiguration

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|storageClass|StorageClassEnum|**参数解释：**桶的存储类别。**取值范围：**存储类别取值详见桶的StorageClassEnum。**默认取值：**无|


**表 3**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


## 返回结果说明<a name="section16729271982"></a>

**表 4**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section8517109534"></a>

本示例用于设置exampleBucket桶的桶存储类别。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.AccessControlList;
import com.obs.services.model.AvailableZoneEnum;
import com.obs.services.model.CreateBucketRequest;
import com.obs.services.model.ObsBucket;
import com.obs.services.model.StorageClassEnum;

public class CreateBucket001 {
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
            CreateBucketRequest request = new CreateBucketRequest();
            //示例桶名
            String exampleBucket = "examplebucket";
            //示例桶区域位置
            String exampleLocation = "cn-north-4";
            request.setBucketName(exampleBucket);
            // 设置桶访问权限为私有读写，默认也是私有读写
            request.setAcl(AccessControlList.REST_CANNED_PRIVATE);
            // 设置桶的存储类别为标准存储
            request.setBucketStorageClass(StorageClassEnum.STANDARD);
            // 设置桶区域位置(以区域为华北-北京四为例)，location 需要与 endpoint的位置信息一致
            request.setLocation(exampleLocation);
            // 指定创建多AZ桶，如果不设置，默认创建单AZ桶
            request.setAvailableZone(AvailableZoneEnum.MULTI_AZ);
            // 创建桶
            ObsBucket bucket = obsClient.createBucket(request);
            // 创建桶成功
            System.out.println("CreateBucket successfully");
            System.out.println("RequestId:"+bucket.getRequestId());


        } catch (ObsException e) {
            System.out.println("CreateBucket failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code: " + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message: " + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
        } catch (Exception e) {
            System.out.println("CreateBucket failed");
            // 其他异常信息打印
            e.printStackTrace();

        }
    }
}

```

## 相关链接<a name="section611332512211"></a>

-   关于设置桶存储类别的API说明，请参见[设置桶存储类别](https://support.huaweicloud.com/api-obs/obs_04_0044.html)。
-   更多关于桶存储类别的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   设置桶存储类别过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   桶和对象相关常见问题请参见[桶和对象相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1200.html)。

