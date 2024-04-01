# 列举桶清单规则\(Java SDK\)<a name="obs_21_0419"></a>

## 功能说明<a name="section13405173072915"></a>

OBS使用不带清单id的GET操作来获取指定桶的所有清单配置，获取到的清单配置一次性返回，不分页。

## 接口约束<a name="section11421530192510"></a>

-   您必须是桶拥有者或者拥有列举桶清单权限，才能列举桶清单。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:GetInventoryConfiguration权限，如果使用桶策略则需授予GetInventoryConfiguration权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。

-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section329121124816"></a>

obsClient.listInventoryConfiguration\([ListInventoryConfigurationRequest](#table2282124793220) [request](#table2282124793220)\)

## 请求参数说明<a name="section1217515331971"></a>

**表 1**  ListInventoryConfigurationRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|是|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|


## 返回结果说明<a name="section127687561478"></a>

**表 2**  ListInventoryConfigurationResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|inventoryConfigurations|List<InventoryConfiguration>|**参数解释：**桶的所有桶清单配置规则，详见InventoryConfiguration|


**表 3**  InventoryConfiguration

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|configurationId|String|必选|**参数解释：**桶清单配置规则的id。**约束限制：**必须由以下字符组成"a-z"、"A-Z"、"0-9"、"-"、"_"和"."。**取值范围：**长度最长为64的字符串。**默认取值：**无|
|isEnabled|boolean|必选|**参数解释：**桶清单配置规则是否启用。**取值范围：**true：生成清单文件。false：不生成清单文件。**默认取值：**true|
|objectPrefix|String|可选|**参数解释：**前缀过滤条件，清单文件中只生成以此前缀开头的对象列表。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|frequency|String|必选|**参数解释：**清单文件的生成周期，只支持按天和按周生成清单，第一次配置完桶清单，任务会在一个小时内启动，之后每隔一个周期启动一次。**取值范围：**Daily：按天生成清单Weekly：按周生成清单**默认取值：**无|
|inventoryFormat|String|必选|**参数解释：**生成的清单文件的格式，现只支持CSV格式。**取值范围：**CSV**默认取值：**无|
|destinationBucket|String|必选|**参数解释：**存放清单文件的目标桶的桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|inventoryPrefix|String|可选|**参数解释：**生成的清单文件对象名会以此前缀开头。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**BucketInventory，即如果不配置前缀，则生成的清单文件对象名默认以"BucketInventory"字符串为前缀开头。|
|includedObjectVersions|String|必选|**参数解释：**清单文件中包含对象的多版本配置。**取值范围：**All：清单会包含对象所有的版本，清单中会增加版本相关的字段：VersionId、IsLatest和DeleteMarker。Current：清单文件中只会列出当前版本信息，不会出现版本相关字段。**默认取值：**无|
|optionalFields|ArrayList<String>|可选|**参数解释：**在此选项中可以添加一些额外的对象元数据字段，生成的清单文件中会包含optionalFields中配置的字段。**取值范围：**Size：对象大小。LastModifiedDate：对象最后修改时间。StorageClass：对象的存储类别。ETag：对象的ETag值。IsMultipartUploaded：对象是否为多段上传。ReplicationStatus：对象的跨区域复制状态。EncryptionStatus：对象的加密状态。**默认取值：**无|


## 代码示例<a name="section770361818820"></a>

本示例用于列举example-bucket桶的所有桶清单文件。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.inventory.InventoryConfiguration;
import com.obs.services.model.inventory.ListInventoryConfigurationRequest;
import com.obs.services.model.inventory.ListInventoryConfigurationResult;
import java.util.List;
public class ListInventoryConfigurations001 {
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
        // String endPoint = System.getenv("ENDPOINT");
        
        // 创建ObsClient实例
        // 使用永久AK/SK初始化客户端
        ObsClient obsClient = new ObsClient(ak, sk,endPoint);
        // 使用临时AK/SK和SecurityToken初始化客户端
        // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

        try {
            // 设置相关示例参数
            String exampleBucketName = "example-bucket";
            ListInventoryConfigurationRequest request = new ListInventoryConfigurationRequest(exampleBucketName);
            // 列举桶清单配置规则
            ListInventoryConfigurationResult result = obsClient.listInventoryConfiguration(request);
            List<InventoryConfiguration> inventoryConfigurations = result.getInventoryConfigurations();
            // 打印inventoryConfigurations的所有规则的所有成员
            for (InventoryConfiguration inventoryConfiguration : inventoryConfigurations) {
                System.out.println("ConfigurationId:" + inventoryConfiguration.getConfigurationId());
                System.out.println("DestinationBucket:" + inventoryConfiguration.getDestinationBucket());
                System.out.println("InventoryFormat:" + inventoryConfiguration.getInventoryFormat());
                System.out.println("Enabled:" + inventoryConfiguration.getEnabled());
                System.out.println("Frequency:" + inventoryConfiguration.getFrequency());
                System.out.println("IncludedObjectVersions:" + inventoryConfiguration.getIncludedObjectVersions());
                System.out.println("InventoryPrefix:" + inventoryConfiguration.getInventoryPrefix());
                System.out.println("ObjectPrefix:" + inventoryConfiguration.getObjectPrefix());
                System.out.println("OptionalFields:" + inventoryConfiguration.getOptionalFields());
                System.out.println("--------------------------------");
            }
            // 打印HTTP状态码
            System.out.println("HTTP Code: " + result.getStatusCode());
            System.out.println("ListInventoryConfiguration succeeded");
        } catch (ObsException e) {
            System.out.println("ListInventoryConfiguration failed");
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
            System.out.println("ListInventoryConfiguration failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section02411903194"></a>

-   关于设置桶清单的API说明，请参见[列举桶清单](https://support.huaweicloud.com/api-obs/obs_04_0057.html)。
-   设置桶清单过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   桶和对象相关常见问题请参见[桶和对象相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1200.html)。

