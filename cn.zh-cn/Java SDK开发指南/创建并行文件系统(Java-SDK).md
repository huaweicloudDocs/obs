# 创建并行文件系统\(Java SDK\)<a name="obs_21_0501"></a>

## 功能说明<a name="section790912182111"></a>

并行文件系统（Parallel File System）是对象存储服务（Object Storage Service，OBS）提供的一种经过优化的高性能文件系统，提供毫秒级别访问时延，TB/s级别带宽和百万级别的IOPS，能够快速处理高性能计算（HPC）工作负载。

作为对象存储服务的子产品，并行文件系统支持用户按照标准的OBS接口读取数据。也支持通过部署在弹性云服务器中的PFS客户端（obsfs工具），按照POSIX文件语义读写数据；通过obsfs用户可以将创建的并行文件系统挂载到云端Linux服务器上，并能像操作本地文件系统一样对并行文件系统内的文件和目录进行在线处理，包括：创建和删除文件/目录，重命名文件/目录，修改写文件等操作。

您可以通过ObsClient.createBucket创建并行文件系统。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section15140193132415"></a>

-   您必须拥有obs:bucket:CreateBucket权限，才能创建并行文件系统。建议使用IAM进行授权，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

-   不支持将已有的OBS桶修改为并行文件系统。
-   并行文件系统暂不支持配额配置功能，默认无配额限制。
-   同一账号下，可以创建多个桶，数量上限是100个（包括对象桶和并行文件系统，不区分地域），存储桶中的对象数量和大小没有限制。
-   新创建并行文件系统的桶名在OBS中必须是唯一的。如果是同一个用户重复创建同一区域的同名桶时返回HTTP状态码200。除此以外的其他场景重复创建同名桶返回HTTP状态码409，表明桶已存在。
-   用户删除并行文件系统后，需要等待30分钟才能创建同名桶和并行文件系统。
-   并不是所有区域都支持创建多AZ并行文件系统，你可以在[产品价格详情](https://www.huaweicloud.com/pricing.html?tab=detail#/obs)页面，查询指定区域是否支持多AZ。

## 方法定义<a name="section54232412"></a>

obsClient.createBucket\([CreateBucketRequest](#table14455523) [request](#table47528147)\)

## 请求参数说明<a name="section13072760"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|CreateBucketRequest|是|**参数解释：**创建并行文件系统相关信息。详见CreateBucketRequest。|


**表 2**  CreateBucketRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**并行文件系统的桶名。**约束限制：**需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名并行文件系统不会报错，创建的并行文件系统属性以第一次请求为准。**默认取值：**无|
|location|String|如果请求的OBS服务地址所在区域为默认区域，则可为空，否则为必选。|**参数解释：**并行文件系统所在的区域。**约束限制：**该参数定义了并行文件系统将会被创建在哪个区域，如果使用的终端节点是obs.myhuaweicloud.com，可以不携带此参数；如果使用的终端节点不是obs.myhuaweicloud.com，则必须携带此参数。**取值范围：**当前有效的OBS区域和终端节点的更多信息，请参考地区和终端节点。终端节点即调用API的请求地址，不同服务不同区域的终端节点不同，您可以向企业管理员获取区域和终端节点信息。**默认取值：**终端节点为obs.myhuaweicloud.com且用户未设定区域时，默认为华北-北京一（cn-north-1）。|
|acl|AccessControlList|可选|**参数解释：**创并行文件系统时可指定并行文件系统的ACL访问策略，您可以使用预定义的ACL策略，也可以自定义ACL策略，有关访问控制列表（Access Control List，ACL）功能的详细信息可参见ACL功能介绍。**取值范围：**如果使用预定义ACL策略，则可选策略参见ACL预定义访问策略。如果选择自定义ACL策略，则可以根据AccessControlList参数描述，自行给参数赋值。**默认取值：**AccessControlList.REST_CANNED_PRIVATE|
|storageClass|StorageClassEnum|可选|**参数解释：**创建并行文件系统时暂不支持配置并行文件系统默认存储类别。您可以通过设置桶存储类别(Java SDK)接口配置并行文件系统存储类别。**默认取值：**无|
|extensionPermissionMap|Map<ExtensionBucketPermissionEnum, Set<String>>|可选|**参数解释：**并行文件系统ACL的授权Map，您可以为一个或多个账号授予并行文件系统权限。Map的ExtensionBucketPermissionEnum用于指定权限，Map的Set<String>用于说明该权限授予的账号ID列表，即domain_id列表。**取值范围：**授予权限的范围详见ExtensionBucketPermissionEnum。如何获取账号ID请参见如何获取账号ID和用户ID?**默认取值：**无|
|epid|String|可选|**参数解释：**创并行文件系统时可指定的企业项目ID，开通企业项目的用户可以从企业项目服务获取。**约束限制：**Epid格式为uuid，未开通企业项目的用户可以不带该头域。示例：9892d768-2d13-450f-aac7-ed0e44c2585f**默认取值：**无|
|availableZone|AvailableZoneEnum|可选|**参数解释：**创并行文件系统时可指定的数据冗余类型，即AZ类型。**约束限制：**归档存储不支持多AZ。如果并行文件系统所在区域不支持多AZ存储，则该并行文件系统的存储类别默认为单AZ。**取值范围：**如果将并行文件系统配置为多AZ，则取值为"MULTI_AZ"。如果将并行文件系统配置为单AZ，则无需选择此选项，系统默认赋值。**默认取值：**不设置该参数，则默认设置并行文件系统为单AZ。|
|bucketType|BucketTypeEnum|可选|**参数解释：**创建的并行文件系统类型。**取值范围：**创建并行文件系统时，bucketType必须选择PFS。**默认取值：**无|


**表 3**  ACL预定义访问策略

|**常量名**|**说明**|
|--|--|
|AccessControlList.REST_CANNED_PRIVATE|私有读写。桶或对象的所有者拥有完全控制的权限，其他任何人都没有访问权限。|
|AccessControlList.REST_CANNED_PUBLIC_READ|公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE|公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_DELIVERED|桶公共读，桶内对象公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据，可以获取该桶内对象的内容和元数据。不能应用于对象。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE_DELIVERED|桶公共读写，桶内对象公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象、删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务，可以获取该桶内对象的内容和元数据。不能应用于对象。|


**表 4**  ExtensionBucketPermissionEnum

|**常量名**|**描述**|
|--|--|
|GRANT_READ|授予对应账号ID的账号READ权限。账号被授予READ权限后，针对当前正在创建的桶，允许列举桶内对象、列举桶中多段任务、列举桶中多版本对象、获取桶元数据。|
|GRANT_WRITE|授予对应账号ID的账号READ权限。账号被授予WRITE权限后，针对当前正在创建的桶，允许创建、删除、覆盖桶内所有对象，允许初始化段、上传段、拷贝段、合并段、取消多段上传任务。|
|GRANT_READ_ACP|授予对应账号ID的账号READ_ACP权限。账号被授予READ_ACP权限后，针对当前正在创建的桶，允许读桶的ACL信息。|
|GRANT_WRITE_ACP|授予对应账号ID的账号WRITE_ACP权限。账号被授予WRITE_ACP权限后，针对当前正在创建的桶，允许修改桶的ACL信息。|
|GRANT_FULL_CONTROL|授予对应账号ID的账号FULL_CONTROL权限。账号被授予FULL_CONTROL权限后，针对当前正在创建的桶，允许进行任何操作。|
|GRANT_READ_DELIVERED|授予对应账号ID的账号READ权限，并且在默认情况下，该READ权限将传递给桶内所有对象。|
|GRANT_FULL_CONTROL_DELIVERED|授予对应账号ID的账号FULL_CONTROL权限，并且在默认情况下，该FULL_CONTROL权限将传递给桶内所有对象。|


**表 5**  AccessControlList

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|owner|Owner|可选|**参数解释：**并行文件系统所有者的信息，详见Owner。|
|delivered|boolean|可选|**参数解释：**并行文件系统的ACL是否向并行文件系统内对象传递，作用于并行文件系统内所有对象。**取值范围：**true：是，并行文件系统ACL向并行文件系统内对象传递。false：否，并行文件系统ACL不向并行文件系统内对象传递，仅作用于并行文件系统。**默认取值：**false|
|grants|Set<GrantAndPermission>|可选|**参数解释：**被授权用户相关信息，详见GrantAndPermission。|


**表 6**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 7**  GrantAndPermission

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantee|GranteeInterface|必选|**参数解释：**被授权用户或用户组，详见GranteeInterface。|
|permission|Permission|必选|**参数解释：**用户或用户组被授予的权限。**取值范围：**详见Permission。**默认取值：**无|
|delivered|boolean|可选|**参数解释：**并行文件系统的ACL是否向并行文件系统内对象传递，作用于并行文件系统内所有对象。**取值范围：**true：是，并行文件系统ACL向并行文件系统内对象传递。false：否，并行文件系统ACL不向并行文件系统内对象传递，仅作用于并行文件系统。**默认取值：**false|


**表 8**  GranteeInterface

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|CanonicalGrantee|CanonicalGrantee|必选|**参数解释：**被授权用户的用户信息，详见CanonicalGrantee。|
|GroupGrantee|GroupGrantee|必选|**参数解释：**被授权用户组的用户组信息。**取值范围：**详见GroupGrantee。**默认取值：**无|


**表 9**  CanonicalGrantee

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantId|String|如果Type为用户类型则必选|**参数解释：**被授权用户的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数描述：**被授权用户的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 10**  GroupGrantee

|**常量名**|**说明**|
|--|--|
|ALL_USERS|所有用户。|
|AUTHENTICATED_USERS|授权用户，已废弃。|
|LOG_DELIVERY|日志投递组，已废弃。|


**表 11**  Permission

|**常量名**|**原始值**|**说明**|
|--|--|--|
|PERMISSION_READ|READ|读权限。如果有桶的读权限，则可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。如果有对象的读权限，则可以获取该对象内容和元数据。|
|PERMISSION_WRITE|WRITE|写权限。如果有桶的写权限，则可以上传、覆盖和删除该桶内任何对象和段。此权限在对象上不适用。|
|PERMISSION_READ_ACP|READ_ACP|读取ACL配置的权限。如果有读ACP的权限，则可以获取对应的桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有读对应桶或对象ACP的权限。|
|PERMISSION_WRITE_ACP|WRITE_ACP|修改ACL配置的权限。如果有写ACP的权限，则可以更新对应桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有写对应桶或对象的ACP的权限。拥有了写ACP的权限，由于可以更改权限控制策略，实际上意味着拥有了完全访问的权限。|
|PERMISSION_FULL_CONTROL|FULL_CONTROL|完全控制权限，包括对桶或对象的读写权限，以及对桶或对象ACL配置的读写权限。如果有桶的完全控制权限意味着拥有READ、WRITE、READ_ACP和WRITE_ACP的权限。如果有对象的完全控制权限意味着拥有READ、READ_ACP和WRITE_ACP的权限。|


**表 12**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 13**  AvailableZoneEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|MULTI_AZ|3az|多az类型|


## 返回结果说明<a name="section1155011051819"></a>

**表 14**  response

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|bucketName|String|**参数解释：**并行文件系统名。**约束限制：**并行文件系统的名字需全局唯一，不能与已有的任何并行文件系统名称重复，包括其他用户创建的并行文件系统。并行文件系统命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名并行文件系统不会报错，创建的并行文件系统属性以第一次请求为准。**默认取值：**无|
|owner|Owner|**参数解释：**并行文件系统拥有者信息，详见Owner。|
|creationDate|java.util.Date|**参数解释：**并行文件系统创建时间。**默认取值：**无|
|location|String|**参数解释：**并行文件系统所在的区域。**约束限制：**该参数定义了并行文件系统将会被创建在哪个区域，如果使用的终端节点是obs.myhuaweicloud.com，可以不携带此参数；如果使用的终端节点不是obs.myhuaweicloud.com，则必须携带此参数。**取值范围：**当前有效的OBS区域和终端节点的更多信息，请参考地区和终端节点。终端节点即调用API的请求地址，不同服务不同区域的终端节点不同，您可以向企业管理员获取区域和终端节点信息。**默认取值：**终端节点为obs.myhuaweicloud.com且用户未设定区域时，默认为华北-北京一（cn-north-1）。|
|storageClass|StorageClassEnum|**参数解释：**创建并行文件系统时暂不支持配置并行文件系统默认存储类别。您可以通过设置桶存储类别(Java SDK)接口配置并行文件系统存储类别。**默认取值：**无|
|acl|AccessControlList|**参数解释：**创并行文件系统时可指定并行文件系统的ACL访问策略，您可以使用预定义的ACL策略，也可以自定义ACL策略，有关访问控制列表（Access Control List，ACL）功能的详细信息可参见ACL功能介绍。**取值范围：**如果使用预定义ACL策略，则可选策略参见ACL预定义访问策略。如果选择自定义ACL策略，则可以根据AccessControlList参数描述，自行给参数赋值。**默认取值：**AccessControlList.REST_CANNED_PRIVATE|
|bucketTypeEnum|BucketTypeEnum|**参数解释：**创建的并行文件系统类型。**取值范围：**创建并行文件系统时，bucketType为PFS。**默认取值：**无|


## 代码示例<a name="section5551173017239"></a>

本示例用于新建名为examplebucket的并行文件系统。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.BucketTypeEnum;
import com.obs.services.model.CreateBucketRequest;
import com.obs.services.model.HeaderResponse;
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
            // 创建并行文件系统成功
            CreateBucketRequest request = new CreateBucketRequest();
            request.setBucketName("examplebucket");
            request.setBucketType(BucketTypeEnum.PFS);
            // 指定所属区域，location 需要与 endpoint的位置信息 一致
            request.setLocation("your_region");
            HeaderResponse response = obsClient.createBucket(request);
            System.out.println("CreateBucket successfully");
            System.out.println("StatusCode:" + response.getStatusCode());
            System.out.println("RequestId:" + response.getRequestId());
        } catch (ObsException e) {
            System.out.println("CreateBucket failed");
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
            System.out.println("CreateBucket failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于并行文件系统的更多说明，请参见[什么是并行文件系统](https://support.huaweicloud.com/pfsfg-obs/obs_13_0007.html)。
-   更多关于创建并行文件系统的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/PFSBucketAndObjectOperationSample.java)。
-   创建并行文件系统过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   创建并行文件系统常见问题请参见[并行文件系统常见问题](https://support.huaweicloud.com/pfsfg-obs/obs_13_0015.html)。

