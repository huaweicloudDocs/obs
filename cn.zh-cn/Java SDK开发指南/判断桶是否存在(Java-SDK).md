# 判断桶是否存在\(Java SDK\)<a name="obs_21_0404"></a>

## 功能说明<a name="section59325057"></a>

判断指定桶名的桶是否存在，返回的结果中HTTP状态码为200表明桶存在，否则返回404表明桶不存在。

## 接口约束<a name="section813083414353"></a>

-   您必须是桶拥有者或拥有判断桶是否存在的权限，才能判断桶是否存在。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:HeadBucket权限，如果使用桶策略则需授予HeadBucket权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.headBucket\(String  [bucketName](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|是|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 2**  返回结果

|**参数类型**|**描述**|
|--|--|
|boolean|**参数解释：**桶是否存在。**取值范围：**true：桶存在false：桶不存在**默认取值：**无|


## 代码示例<a name="section4866240616"></a>

本示例用于判断examplebucket桶是否存在。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
public class HeadBucket001 {
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
            // 判断桶是否存在
            boolean exists = obsClient.headBucket(exampleBucket);
            System.out.println("HeadBucket successfully");
            System.out.println(exists);
        } catch (ObsException e) {
            System.out.println("HeadBucket failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code:" + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code :" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message:" + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
        } catch (Exception e) {
            System.out.println("HeadBucket failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   判断桶是否存在和获取桶元数据是同一个REST API，关于判断桶是否存在的API说明，请参见[获取桶元数据](https://support.huaweicloud.com/api-obs/obs_04_0023.html)。
-   创建桶过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   桶和对象相关常见问题请参见[桶和对象相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1200.html)。

