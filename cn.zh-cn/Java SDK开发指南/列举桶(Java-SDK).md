# 列举桶\(Java SDK\)<a name="obs_21_0402"></a>

## 功能说明<a name="section11453143514395"></a>

OBS桶是对象的容器，您上传的文件都存放在桶中。调用列举桶接口，可列举当前账号所有地域下符合指定条件的桶。返回结果以桶名的字典序排序。

## 接口约束<a name="section419615157204"></a>

-   您必须拥有obs:bucket:ListAllMyBuckets权限，才能获取桶列表。建议使用IAM进行授权，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)。

-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

-   设置ListBucketsRequest.setQueryLocation参数为true后，可在列举桶时查询桶的区域位置。

## 方法定义<a name="section54232412"></a>

obsClient.listBuckets\([ListBucketsRequest](#table14455523) [request](#table16553037152015)\)

## 请求参数说明<a name="section35537379207"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|ListBucketsRequest|必选|**参数解释：**获取桶列表请求参数，详见ListBucketsRequest。|


**表 2**  ListBucketsRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|queryLocation|boolean|可选|**参数解释：**是否同时查询桶的区域位置。**取值范围：**true：同时查询桶的区域位置false：不查询桶的区域位置**默认取值：**false|
|bucketType|BucketTypeEnum|可选|**参数解释：**列举指定类型的桶。**取值范围：**详见BucketTypeEnum。**默认取值：**OBJECT，即对象桶。|


**表 3**  BucketTypeEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|OBJECT|OBJECT|对象桶|
|PFS|POSIX|并行文件系统|


## 返回结果说明<a name="section1155011051819"></a>

**表 4**  ListBucketsResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|owner|Owner|**参数解释：**桶拥有者信息，详见Owner。**默认取值：**无|
|buckets|List<ObsBucket>|**参数解释：**桶列表信息。详见ObsBucket。**默认取值：**无|


**表 5**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 6**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 7**  AccessControlList

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|owner|Owner|可选|**参数解释：**桶所有者的信息，详见Owner。|
|delivered|boolean|可选|**参数解释：**桶的ACL是否向桶内对象传递，作用于桶内所有对象。**取值范围：**true：是，桶ACL向桶内对象传递。false：否，桶ACL不向桶内对象传递，仅作用于桶。**默认取值：**false|
|grants|Set<GrantAndPermission>|可选|**参数解释：**被授权用户相关信息，详见GrantAndPermission。|


**表 8**  GrantAndPermission

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantee|GranteeInterface|必选|**参数解释：**被授权用户或用户组，详见GranteeInterface。|
|permission|Permission|必选|**参数解释：**用户或用户组被授予的权限。**取值范围：**详见Permission。**默认取值：**无|
|delivered|boolean|可选|**参数解释：**桶的ACL是否向桶内对象传递，作用于桶内所有对象。**取值范围：**true：是，桶ACL向桶内对象传递。false：否，桶ACL不向桶内对象传递，仅作用于桶。**默认取值：**false|


**表 9**  GranteeInterface

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|CanonicalGrantee|CanonicalGrantee|必选|**参数解释：**被授权用户的用户信息，详见CanonicalGrantee。|
|GroupGrantee|GroupGrantee|必选|**参数解释：**被授权用户组的用户组信息。**取值范围：**详见GroupGrantee。**默认取值：**无|


**表 10**  CanonicalGrantee

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantId|String|如果Type为用户类型则必选|**参数解释：**被授权用户的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数描述：**被授权用户的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 11**  GroupGrantee

|**常量名**|**说明**|
|--|--|
|ALL_USERS|所有用户。|
|AUTHENTICATED_USERS|授权用户，已废弃。|
|LOG_DELIVERY|日志投递组，已废弃。|


**表 12**  Permission

|**常量名**|**原始值**|**说明**|
|--|--|--|
|PERMISSION_READ|READ|读权限。如果有桶的读权限，则可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。如果有对象的读权限，则可以获取该对象内容和元数据。|
|PERMISSION_WRITE|WRITE|写权限。如果有桶的写权限，则可以上传、覆盖和删除该桶内任何对象和段。此权限在对象上不适用。|
|PERMISSION_READ_ACP|READ_ACP|读取ACL配置的权限。如果有读ACP的权限，则可以获取对应的桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有读对应桶或对象ACP的权限。|
|PERMISSION_WRITE_ACP|WRITE_ACP|修改ACL配置的权限。如果有写ACP的权限，则可以更新对应桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有写对应桶或对象的ACP的权限。拥有了写ACP的权限，由于可以更改权限控制策略，实际上意味着拥有了完全访问的权限。|
|PERMISSION_FULL_CONTROL|FULL_CONTROL|完全控制权限，包括对桶或对象的读写权限，以及对桶或对象ACL配置的读写权限。如果有桶的完全控制权限意味着拥有READ、WRITE、READ_ACP和WRITE_ACP的权限。如果有对象的完全控制权限意味着拥有READ、READ_ACP和WRITE_ACP的权限。|


**表 13**  ACL预定义访问策略

|**常量名**|**说明**|
|--|--|
|AccessControlList.REST_CANNED_PRIVATE|私有读写。桶或对象的所有者拥有完全控制的权限，其他任何人都没有访问权限。|
|AccessControlList.REST_CANNED_PUBLIC_READ|公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE|公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_DELIVERED|桶公共读，桶内对象公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据，可以获取该桶内对象的内容和元数据。不能应用于对象。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE_DELIVERED|桶公共读写，桶内对象公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象、删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务，可以获取该桶内对象的内容和元数据。不能应用于对象。|


**表 14**  ObsBucket

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|bucketName|String|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|owner|Owner|**参数解释：**桶拥有者信息，详见Owner。|
|creationDate|java.util.Date|**参数解释：**桶创建时间。**默认取值：**无|
|location|String|**参数解释：**桶所在的区域。**约束限制：**该参数定义了桶将会被创建在哪个区域，如果使用的终端节点是obs.myhuaweicloud.com，可以不携带此参数；如果使用的终端节点不是obs.myhuaweicloud.com，则必须携带此参数。**取值范围：**当前有效的OBS区域和终端节点的更多信息，请参考地区和终端节点。终端节点即调用API的请求地址，不同服务不同区域的终端节点不同，您可以向企业管理员获取区域和终端节点信息。**默认取值：**终端节点为obs.myhuaweicloud.com且用户未设定区域时，默认为华北-北京一（cn-north-1）。|
|storageClass|StorageClassEnum|**参数解释：**创桶时可指定的桶的存储类别。**取值范围：**可选择的访问策略选项参见StorageClassEnum。**默认取值：**STANDARD，即标准存储类别。|
|acl|AccessControlList|**参数解释：**创桶时可指定桶的ACL访问策略，您可以使用预定义的ACL策略，也可以自定义ACL策略，有关访问控制列表（Access Control List，ACL）功能的详细信息可参见ACL功能介绍。**取值范围：**如果使用预定义ACL策略，则可选策略参见ACL预定义访问策略。如果选择自定义ACL策略，则可以根据AccessControlList参数描述，自行给参数赋值。**默认取值：**AccessControlList.REST_CANNED_PRIVATE|
|bucketTypeEnum|BucketTypeEnum|**参数解释：**创建的桶类型。**取值范围：**详见BucketTypeEnum。**默认取值：**OBJECT，即对象桶。|


## 代码示例<a name="section18911203884710"></a>

本示例用于列举所有桶列表，并查询桶的区域。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ListBucketsRequest;
import com.obs.services.model.ObsBucket;
import java.util.List;
public class ListBucket001 {
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
            // 列举桶
            ListBucketsRequest request = new ListBucketsRequest();
            request.setQueryLocation(true);
            List<ObsBucket> buckets = obsClient.listBuckets(request);
            for (ObsBucket bucket : buckets) {
                System.out.println("ListBuckets successfully");
                System.out.println("BucketName:" + bucket.getBucketName());
                System.out.println("CreationDate:" + bucket.getCreationDate());
                System.out.println("Location:" + bucket.getLocation());
            }
        } catch (ObsException e) {
            System.out.println("ListBuckets failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code: " + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message:" + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
        } catch (Exception e) {
            System.out.println("ListBuckets failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section72611512281"></a>

-   关于列举桶的API说明，请参见[获取桶列表](https://support.huaweicloud.com/api-obs/obs_04_0020.html)。
-   获取桶列表过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

