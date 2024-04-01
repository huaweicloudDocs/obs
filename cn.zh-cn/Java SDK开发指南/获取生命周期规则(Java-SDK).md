# 获取生命周期规则\(Java SDK\)<a name="obs_21_1103"></a>

## 功能介绍<a name="section60827539"></a>

OBS支持用户配置指定的规则，实现定时删除桶中的对象或者定时转换对象的存储类别，从而节省存储费用，更多生命周期相关信息请参见[生命周期管理](https://support.huaweicloud.com/ugobs-obs/obs_41_0033.html)。

调用获取桶的生命周期配置接口，您可以获取指定桶的生命周期策略。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section326152964516"></a>

-   您必须是桶拥有者或拥有获取桶的生命周期配置的权限，才能获取桶的生命周期配置。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:GetLifecycleConfiguration权限，如果使用桶策略则需授予GetLifecycleConfiguration权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.getBucketLifecycle\(final  [BaseBucketRequest](#table43960571) [request](#table72121329103020)\)

## 请求参数说明<a name="section51426113"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|BaseBucketRequest|必选|**参数解释：**桶的基本信息请求参数列表，详见BaseBucketRequest。|


**表 2**  BaseBucketRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 3**  LifecycleConfiguration

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|rules|List<Rule>|**参数解释：**桶生命周期规则列表，详见Rule。|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


**表 4**  Rule

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|可选|**参数解释：**生命周期规则ID。**取值范围：**长度大于0且不超过255的字符串。**默认取值：**无|
|prefix|String|必选|**参数解释：**对象名前缀，用以标识哪些对象可以匹配到当前这条规则。可为空字符串，代表匹配桶内所有对象。例如，假设您拥有以下对象：logs/day1、logs/day2、logs/day3和ExampleObject.jpg。如果您将ExampleObject.jpg指定为前缀，则规则仅应用于该特定对象。如果您将logs/指定为前缀，规则将应用于密钥名称以字符串“logs/”开头的三个对象。如果您指定空的前缀，规则将应用于桶中的所有对象。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|enabled|boolean|必选|**参数解释：**标识当前规则是否启用。**取值范围：**true：当前规则启用。false：当前规则未启用。**默认取值：**无|
|expiration|Expiration|可选|**参数解释：**对象过期时间配置。详见Expiration。**默认取值：**无|
|noncurrentVersionExpiration|NoncurrentVersionExpiration|可选|**参数解释：**历史版本对象过期时间配置，详见NoncurrentVersionExpiration。**约束限制：**仅针对对象的历史版本。当前桶已启用（或开启后暂停）多版本。**默认取值：**无|
|transitions|List<Transition>|可选|**参数解释：**对象转换策略列表，用于使用生命周期规则转换对象的存储类别，包含生命周期配置的迁移时间和迁移后对象存储级别，详见Transition。**约束限制：**仅针对对象的最新版本。**默认取值：**无|
|noncurrentVersionTransitions|List<NoncurrentVersionTransition>|可选|**参数解释：**历史版本对象转换策略列表，用于使用生命周期规则转换历史版本对象的存储类别，包含生命周期配置的迁移时间和迁移后对象存储级别，详见NoncurrentVersionTransition。**约束限制：**仅针对对象的历史版本。当前桶已启用（或开启后暂停）多版本。**默认取值：**无|


**表 5**  Expiration

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|days|Integer|如果没有设置date则必选|**参数解释：**指定生命周期规则在对象最后更新过后多少天生效，即执行过期删除操作。**约束限制：**仅适用于对象的最新版本。**取值范围：**正整数，单位：天。**默认取值：**无|
|date|Date|如果没有设置days则必选|**参数解释：**指定OBS对该日期之前的对象执行生命周期规则，即执行过期删除操作。**默认取值：**无|


**表 6**  NoncurrentVersionExpiration

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|days|Integer|必选|**参数解释：**表示对象成为历史版本后第几天时过期。**约束限制：**仅针对历史版本。**取值范围：**正整数，单位：天。**默认取值：**无|


**表 7**  Transition

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|days|Integer|如果没有设置date则必选|**参数解释：**表示在对象创建时间后第几天时转换。**约束限制：**仅适用于对象的最新版本。**取值范围：**正整数，单位：天。**默认取值：**无|
|date|Date|如果没有设置days则必选|**参数解释：**表示对象转换的日期。**默认取值：**无|
|storageClass|StorageClassEnum|必选|**参数解释：**对象转换后的存储类别。**约束限制：**对象存储类别转换限制：仅支持将标准存储对象转换为低频访问存储对象，低频访问存储对象转换为标准存储对象需手动转换。仅支持将标准存储或低频访问存储对象转换为归档存储对象。如果要将归档存储对象转换为标准存储或低频访问存储对象，需要手动先恢复对象，然后手动转换存储类别。归档存储不支持多AZ。因此不支持使用生命周期的存储类别转换功能，将多AZ桶或对象的存储类别转化为归档存储。**取值范围：**生命周期转换的目标存储类别取值范围详见StorageClassEnum。**默认取值：**无|


**表 8**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 9**  NoncurrentVersionTransition

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|days|Integer|如果没有设置date则必选|**参数解释：**表示在对象创建时间后第几天时转换。**约束限制：**仅适用于历史版本。**取值范围：**正整数，单位：天。**默认取值：**无|
|storageClass|StorageClassEnum|必选|**参数解释：**对象转换后的存储类别。**约束限制：**对象存储类别转换限制：仅支持将标准存储对象转换为低频访问存储对象，低频访问存储对象转换为标准存储对象需手动转换。仅支持将标准存储或低频访问存储对象转换为归档存储对象。如果要将归档存储对象转换为标准存储或低频访问存储对象，需要手动先恢复对象，然后手动转换存储类别。归档存储不支持多AZ。因此不支持使用生命周期的存储类别转换功能，将多AZ桶或对象的存储类别转化为归档存储。**取值范围：**生命周期转换的目标存储类别取值范围详见StorageClassEnum。**默认取值：**无|


## 代码示例<a name="section1646819448120"></a>

以下代码展示了如何获取examplebucket桶的生命周期规则。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.LifecycleConfiguration;
public class GetBucketLifecycle001 {
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
            // 查看生命周期规则
            LifecycleConfiguration config = obsClient.getBucketLifecycle("examplebucket");
            System.out.println("getBucketLifecycle successfully");
            for (LifecycleConfiguration.Rule rule : config.getRules()) {
                System.out.println(rule.getId());
                System.out.println(rule.getPrefix());
                for (LifecycleConfiguration.Transition transition : rule.getTransitions()) {
                    System.out.println(transition.getDays());
                    System.out.println(transition.getStorageClass());
                }
                System.out.println(rule.getExpiration() != null ? rule.getExpiration().getDays() : "");
                for (LifecycleConfiguration.NoncurrentVersionTransition noncurrentVersionTransition :
                        rule.getNoncurrentVersionTransitions()) {
                    System.out.println(noncurrentVersionTransition.getDays());
                    System.out.println(noncurrentVersionTransition.getStorageClass());
                }
                System.out.println(
                        rule.getNoncurrentVersionExpiration() != null
                                ? rule.getNoncurrentVersionExpiration().getDays()
                                : "");
            }
        } catch (ObsException e) {
            System.out.println("getBucketLifecycle failed");
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
            System.out.println("getBucketLifecycle failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于获取桶的生命周期配置的API说明，请参见[获取桶的生命周期配置](https://support.huaweicloud.com/api-obs/obs_04_0035.html)。
-   更多关于获取桶的生命周期配置的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/PostObjectSample.java)。
-   获取桶的生命周期配置过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   生命周期管理相关问题请参见[生命周期管理相关问题](https://support.huaweicloud.com/obs_faq/obs_faq_0400.html)。

