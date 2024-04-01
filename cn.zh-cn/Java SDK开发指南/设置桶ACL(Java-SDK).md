# 设置桶ACL\(Java SDK\)<a name="obs_21_0406"></a>

## 功能说明<a name="section15575880"></a>

OBS支持对桶操作进行权限控制，您可以为桶设置访问策略，指定某一个用户对某一个桶是否有权行使某一项指定操作。OBS权限控制的方式有IAM、桶策略和ACL三种，ACL按照粒度又分为桶ACL和对象ACL，本节将对桶ACL接口进行详细介绍，更多权限相关内容可参见《对象存储服务权限配置指南》的[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)章节。

桶ACL是跨账号场景的权限，设置授权的对象不是当前账号，也不是当前账号下的IAM用户，而是另一个华为云账号及其账号下的IAM用户；授权的范围是以桶为粒度的，一条ACL策略为一个桶设置策略，因此设置ACL策略时您必须明确指定桶名；桶ACL授予的权限包括桶的访问权限和桶ACL的访问权限两个方面，桶的访问权限包括对桶及桶内对象的查看和编辑权限，桶ACL的访问权限包括对桶ACL策略的查看和编辑权限，详情可参见[ACL权限控制方式介绍](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0005.html)。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

桶访问权限（[ACL](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0005.html)）可以通过三种方式设置， 具体参见[方法定义](#section54232412)。

OBS支持的桶或对象权限包含五类，见[表Permission](#table17475749161815)。

OBS预定义的访问策略包含五类，见下表[ACL预定义访问策略](#table3131153615508)。

## 接口约束<a name="section35171119122414"></a>

-   单个桶最多支持100条ACL策略。
-   您必须是桶拥有者或拥有设置桶ACL的权限，才能设置桶ACL。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:PutBucketAcl权限，如果使用桶策略则需授予PutBucketAcl权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

-   方法1：创建桶时，设置访问权限：

    ```
    obsBucket.setBucketName(exampleBucket);
    // 设置桶访问权限为私有读写
    obsBucket.setAcl(AccessControlList.REST_CANNED_PRIVATE);
    // 创建桶
    obsClient.createBucket(obsBucket);
    ```

-   方法2：通过预定义访问策略设置访问权限：

    ```
    // 设置桶访问权限为私有读写
    obsClient.setBucketAcl(String exampleBucket, AccessControlList.REST_CANNED_PRIVATE);
    ```

-   方法3：调用ObsClient.setBucketAcl直接设置访问权限：

    ```
    // 直接设置桶访问权限
    obsClient.setBucketAcl(String [bucketName](#table14455523),[AccessControlList](#table881141715520) [acl](#table14455523));
    ```

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|acl|AccessControlList|可选|**参数解释：**创桶时可指定桶的ACL访问策略，您可以使用预定义的ACL策略，也可以自定义ACL策略，有关访问控制列表（Access Control List，ACL）功能的详细信息可参见ACL功能介绍。**取值范围：**如果使用预定义ACL策略，则可选策略参见ACL预定义访问策略。如果选择自定义ACL策略，则可以根据AccessControlList参数描述，自行给参数赋值。**默认取值：**AccessControlList.REST_CANNED_PRIVATE|


**表 2**  AccessControlList

|**参数名称**|**参数类型**|**是否必选**|**参数类型**|
|--|--|--|--|
|owner|Owner|可选|**参数解释：**桶所有者的信息，详见Owner。|
|delivered|boolean|可选|**参数解释：**桶的ACL是否向桶内对象传递，作用于桶内所有对象。**取值范围：**true：是，桶ACL向桶内对象传递。false：否，桶ACL不向桶内对象传递，仅作用于桶。**默认取值：**false|
|grants|Set<GrantAndPermission>|可选|**参数解释：**被授权用户相关信息，详见GrantAndPermission。|


**表 3**  预定义的AccessControlList

|**常量名**|**描述**|
|--|--|
|AccessControlList.REST_CANNED_PRIVATE|私有读写。桶或对象的所有者拥有完全控制的权限，其他任何人都没有访问权限。|
|AccessControlList.REST_CANNED_PUBLIC_READ|公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE|公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务。设在对象上，所有人可以获取该对象内容和元数据。|
|AccessControlList.REST_CANNED_PUBLIC_READ_DELIVERED|桶公共读，桶内对象公共读。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据，可以获取该桶内对象的内容和元数据。不能应用于对象。|
|AccessControlList.REST_CANNED_PUBLIC_READ_WRITE_DELIVERED|桶公共读写，桶内对象公共读写。设在桶上，所有人可以获取该桶内对象列表、桶内多段任务、桶的元数据、上传对象、删除对象、初始化段任务、上传段、合并段、拷贝段、取消多段上传任务，可以获取该桶内对象的内容和元数据。不能应用于对象。|


**表 4**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 5**  GrantAndPermission

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantee|GranteeInterface|必选|**参数解释：**被授权用户或用户组，详见GranteeInterface。|
|permission|Permission|必选|**参数解释：**用户或用户组被授予的权限。**取值范围：**详见Permission。**默认取值：**无|
|delivered|boolean|可选|**参数解释：**桶的ACL是否向桶内对象传递，作用于桶内所有对象。**取值范围：**true：是，桶ACL向桶内对象传递。false：否，桶ACL不向桶内对象传递，仅作用于桶。**默认取值：**false|


**表 6**  GranteeInterface

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|CanonicalGrantee|CanonicalGrantee|必选|**参数解释：**被授权用户的用户信息，详见CanonicalGrantee。|
|GroupGrantee|GroupGrantee|必选|**参数解释：**被授权用户组的用户组信息。**取值范围：**详见GroupGrantee。**默认取值：**无|


**表 7**  CanonicalGrantee

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|grantId|String|如果Type为用户类型则必选|**参数解释：**被授权用户的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数描述：**被授权用户的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 8**  GroupGrantee

|**常量名**|**说明**|
|--|--|
|ALL_USERS|所有用户。|
|AUTHENTICATED_USERS|授权用户，已废弃。|
|LOG_DELIVERY|日志投递组，已废弃。|


**表 9**  Permission

|**常量名**|**原始值**|**说明**|
|--|--|--|
|PERMISSION_READ|READ|读权限。如果有桶的读权限，则可以获取该桶内对象列表、桶内多段任务、桶的元数据、桶的多版本。如果有对象的读权限，则可以获取该对象内容和元数据。|
|PERMISSION_WRITE|WRITE|写权限。如果有桶的写权限，则可以上传、覆盖和删除该桶内任何对象和段。此权限在对象上不适用。|
|PERMISSION_READ_ACP|READ_ACP|读取ACL配置的权限。如果有读ACP的权限，则可以获取对应的桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有读对应桶或对象ACP的权限。|
|PERMISSION_WRITE_ACP|WRITE_ACP|修改ACL配置的权限。如果有写ACP的权限，则可以更新对应桶或对象的权限控制列表（ACL）。桶或对象的所有者永远拥有写对应桶或对象的ACP的权限。拥有了写ACP的权限，由于可以更改权限控制策略，实际上意味着拥有了完全访问的权限。|
|PERMISSION_FULL_CONTROL|FULL_CONTROL|完全控制权限，包括对桶或对象的读写权限，以及对桶或对象ACL配置的读写权限。如果有桶的完全控制权限意味着拥有READ、WRITE、READ_ACP和WRITE_ACP的权限。如果有对象的完全控制权限意味着拥有READ、READ_ACP和WRITE_ACP的权限。|


## 返回结果说明<a name="section1155011051819"></a>

**表 10**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例：创建桶时指定预定义访问策略<a name="section53213368210"></a>

本示例用于创建exampleBucket桶时指定预定义访问策略。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.AccessControlList;
import com.obs.services.model.ObsBucket;
public class SetBucketAcl001 {
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
            ObsBucket obsBucket = new ObsBucket();
            //示例桶名
            String exampleBucket = "examplebucket";
            obsBucket.setBucketName(exampleBucket);
            // 设置桶访问权限为私有读写
            obsBucket.setAcl(AccessControlList.REST_CANNED_PRIVATE);
            // 创建桶
            obsClient.createBucket(obsBucket);
            System.out.println("SetBucketAcl successfully");
        } catch (ObsException e) {
            System.out.println("SetBucketAcl failed");
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
            System.out.println("SetBucketAcl failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：为桶设置预定义访问策略<a name="section774752805217"></a>

本示例用于为exampleBucket桶设置预定义访问策略。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.AccessControlList;
public class SetBucketAcl002 {
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
            //示例桶名
            String exampleBucket = "examplebucket";
            // 设置桶访问权限为私有读写
            obsClient.setBucketAcl(exampleBucket, AccessControlList.REST_CANNED_PRIVATE);
            System.out.println("SetBucketAcl successfully");
        } catch (ObsException e) {
            System.out.println("SetBucketAcl failed");
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
            System.out.println("SetBucketAcl failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：设置桶的访问策略<a name="section166239462549"></a>

本示例用于直接设置exampleBucket桶的访问策略。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.AccessControlList;
import com.obs.services.model.CanonicalGrantee;
import com.obs.services.model.GroupGrantee;
import com.obs.services.model.Owner;
import com.obs.services.model.Permission;
public class SetBucketAcl003 {
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
            //示例桶名
            String exampleBucket = "examplebucket";
            //示例userid
            String exampleUserid = "userid";
            //示例userid
            String exampleOwnerId = "ownerid";
            AccessControlList acl = new AccessControlList();
            Owner owner = new Owner();
            owner.setId(exampleOwnerId);
            acl.setOwner(owner);
            // 为指定用户设置完全控制权限
            acl.grantPermission(new CanonicalGrantee(exampleUserid), Permission.PERMISSION_FULL_CONTROL);
            // 为所有用户设置读权限
            acl.grantPermission(GroupGrantee.ALL_USERS, Permission.PERMISSION_READ);
            // 直接设置桶访问权限
            obsClient.setBucketAcl(exampleBucket, acl);
            System.out.println("SetBucketAcl successfully");
        } catch (ObsException e) {
            System.out.println("SetBucketAcl failed");
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
            System.out.println("SetBucketAcl failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于设置桶ACL的API说明，请参见[设置桶ACL](https://support.huaweicloud.com/api-obs/obs_04_0030.html)。
-   更多关于桶ACL的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   获取桶ACL过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   权限相关常见问题请参见[权限相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1100.html)。

