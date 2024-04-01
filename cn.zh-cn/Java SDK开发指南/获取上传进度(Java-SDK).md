# 获取上传进度\(Java SDK\)<a name="obs_21_0604"></a>

## 功能说明<a name="section4537105612517"></a>

获取指定对象的上传进度。

您可以通过PutObjectRequest.setProgressListener设置数据传输接口来获取上传的进度。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section1075231022716"></a>

-   您必须拥有obs:object:PutObject权限，才能获取获取上传进度。相关授权操作可参见[典型权限场景配置案例](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0011.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   支持获取上传进度的接口包括：流式上传、文件上传、上传段、追加上传和断点续传上传。
-   如果ProgressStatus.getTransferPercentage\(\)返回-1，表明是流式上传，此时必须设置对象属性中的对象长度（Content-Length）。

## 方法定义<a name="section54232412"></a>

PutObjectRequest.setProgressListener\([ProgressListener](获取上传进度(Java-SDK).md#table134092034114420) [progressListener](#table06508445110)\)

## 参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressListener|ProgressListener|必选|**参数解释：**设置数据传输监听器，用于获取上传进度，详见ProgressListener。|


**表 2**  ProgressListener\(传输进度接口\)成员如下

|**方法名称**|**返回值类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressChanged|void|必选|**参数解释：**获取上传进度，详见progressChanged。|


**表 3**  progressChanged参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|status|ProgressStatus|必选|**参数解释：**传输进度数据，详见ProgressStatus。|


**表 4**  ProgressStatus方法

|**方法名称**|**返回值类型**|**说明**|
|--|--|--|
|getAverageSpeed()|double|上传平均速率。|
|getInstantaneousSpeed()|double|上传瞬时速率。|
|getTransferPercentage()|int|上传进度百分比。|
|getNewlyTransferredBytes()|long|新增的字节数。|
|getTransferredBytes()|long|已传输的字节数。|
|getTotalBytes()|long|待传输的字节数。|


## 代码示例<a name="section13446329260"></a>

本示例用于获取将exampleLocalFilePath本地文件上传到examplebucket桶中objectname对象的进度。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ProgressListener;
import com.obs.services.model.ProgressStatus;
import com.obs.services.model.PutObjectRequest;
import java.io.File;
public class PutObject005 {
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
            // 文件上传
            PutObjectRequest request = new PutObjectRequest("examplebucket", "exampleobject");
            request.setFile(new File("exampleLocalFilePath"));
            request.setProgressListener(
                    new ProgressListener() {
                        @Override
                        public void progressChanged(ProgressStatus status) {
                            // 获取上传平均速率
                            System.out.println("AverageSpeed:" + status.getAverageSpeed());
                            // 获取上传进度百分比
                            System.out.println("TransferPercentage:" + status.getTransferPercentage());
                        }
                    });
            // 每上传1MB数据反馈上传进度
            request.setProgressInterval(1024 * 1024L);
            obsClient.putObject(request);
            System.out.println("putObject successfully");
        } catch (ObsException e) {
            System.out.println("putObject failed");
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
            System.out.println("putObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   更多关于上传对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ObjectOperationsSample.java)。
-   上传对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   上传对象常见问题请参见[上传对象失败](https://support.huaweicloud.com/obs_faq/obs_faq_0134.html)。

