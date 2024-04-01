# 设置桶清单规则\(Java SDK\)<a name="obs_21_0417"></a>

## 功能说明<a name="section1811932082310"></a>

桶清单功能可以定期生成桶内对象的相关信息，保存在CSV格式的文件中，并上传到您指定的桶中，方便您管理桶内对象。目标桶和源桶可以是同一个桶。指定的对象内容包括对象版本、大小、上次修改时间、存储类别、标签、加密状态等。

支持对桶清单加密，加密方式为SSE-KMS方式。

## 接口约束<a name="section11421530192510"></a>

-   您必须是桶拥有者或者拥有设置桶清单权限，才能设置桶清单。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:PutBucketInventoryConfiguration权限，如果使用桶策略则需授予PutBucketInventoryConfiguration权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   **桶版本限制：**
    -   只有OBS 3.0的桶支持配置清单，目标桶无OBS版本限制。

-   **清单数量限制：**
    -   一个桶最多支持10条桶清单。

-   **源桶和目标桶限制：**
    -   桶清单配置的源桶和目标桶必须归属同一个账号。
    -   桶清单配置的源桶和目标桶必须归属同一个区域。
    -   桶清单中配置的目标桶不能开启桶默认加密。

-   **功能限制：**
    -   只支持生成CSV格式的清单文件。
    -   桶清单筛选条件目前仅支持设置为所有对象或指定前缀的对象。
    -   同一个桶中多条清单规则的筛选条件不能彼此包含：
        -   如果已经存在针对桶中所有对象的规则，则无法再创建按对象名前缀筛选的规则。如需创建，要先删除针对所有对象的规则。
        -   如果已经存在按对象名前缀筛选的规则，则无法再创建针对桶中所有对象的规则。如需创建，要先删除所有按对象名前缀筛选的规则。
        -   如果已经存在某个按对象名前缀筛选的规则（如前缀ab），则无法再创建与其存在包含或被包含关系的规则（如前缀a或前缀abc）。如需创建，要先删除存在包含或被包含关系的规则。

    -   桶清单加密方式目前只支持SSE-KMS。

-   **权限限制：**
    -   清单文件使用OBS系统用户上传到目标桶，目标桶必须给OBS系统用户写权限。

-   **其他：**
    -   暂不对桶清单功能收费，桶清单生成后只按照存量计费。

## 方法定义<a name="section329121124816"></a>

obsClient.setInventoryConfiguration\([SetInventoryConfigurationRequest](#table649204716910) [request](#table649204716910)\)

## 请求参数说明<a name="section1217515331971"></a>

**表 1**  SetInventoryConfigurationRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|是|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|inventoryConfiguration|InventoryConfiguration|是|**参数解释：**桶清单配置规则，详见InventoryConfiguration。|


**表 2**  InventoryConfiguration

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


## 返回结果说明<a name="section127687561478"></a>

**表 3**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section770361818820"></a>

本示例将为example-bucket桶设置桶清单，桶清单会统计前缀为exampleObjectPrefix的对象的信息。清单文件将存储在example-target-bucket桶中，清单文件的前缀为exampleInventoryPrefix。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HeaderResponse;
import com.obs.services.model.inventory.InventoryConfiguration;
import com.obs.services.model.inventory.SetInventoryConfigurationRequest;
public class SetInventoryConfiguration001
{
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
            String exampleTargetBucketName = "example-target-bucket";
            String exampleConfigurationId = "exampleConfigId001";
            String exampleInventoryPrefix = "exampleInventoryPrefix";
            String exampleObjectPrefix = "exampleObjectPrefix";
            // 设置桶清单配置规则详细参数
            InventoryConfiguration exampleConfiguration = new InventoryConfiguration();
            exampleConfiguration.setDestinationBucket(exampleTargetBucketName);
            exampleConfiguration.setConfigurationId(exampleConfigurationId);
            exampleConfiguration.setInventoryFormat(InventoryConfiguration.InventoryFormatOptions.CSV);
            exampleConfiguration.setFrequency(InventoryConfiguration.FrequencyOptions.DAILY);
            exampleConfiguration.setEnabled(true);
            exampleConfiguration.setIncludedObjectVersions(
                    InventoryConfiguration.IncludedObjectVersionsOptions.CURRENT);
            exampleConfiguration.setInventoryPrefix(exampleInventoryPrefix);
            exampleConfiguration.setObjectPrefix(exampleObjectPrefix);
            // 设置清单文件中会包含的额外的对象元数据字段
            exampleConfiguration
                    .getOptionalFields()
                    .add(InventoryConfiguration.OptionalFieldOptions.IS_MULTIPART_UPLOADED);
            exampleConfiguration.getOptionalFields().add(InventoryConfiguration.OptionalFieldOptions.ETAG);
            exampleConfiguration
                    .getOptionalFields()
                    .add(InventoryConfiguration.OptionalFieldOptions.REPLICATION_STATUS);
            SetInventoryConfigurationRequest request =
                    new SetInventoryConfigurationRequest(exampleBucketName, exampleConfiguration);
            // 设置桶清单配置规则
            HeaderResponse response = obsClient.setInventoryConfiguration(request);
            System.out.println("SetInventoryConfiguration succeeded");
            System.out.println("HTTP Code: " + response.getStatusCode());
        } catch (ObsException e) {
            System.out.println("SetInventoryConfiguration failed");
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
            System.out.println("SetInventoryConfiguration failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于设置桶清单的API说明，请参见[设置桶清单](https://support.huaweicloud.com/api-obs/obs_04_0055.html)。
-   设置桶清单过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   桶和对象相关常见问题请参见[桶和对象相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1200.html)。

