# 获取下载进度\(Java SDK\)<a name="obs_21_0704"></a>

## 功能说明<a name="section4537105612517"></a>

获取指定对象的下载进度。

您可以通过GetObjectRequest.setProgressInterval设置数据传输接口来获取下载的进度。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section1075231022716"></a>

-   您必须是桶拥有者或拥有下载对象的权限，才能获取获取下载进度。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:GetObject权限，如果使用桶策略则需授予GetObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   支持获取下载进度的接口包括：流式下载、范围下载和断点续传下载。

## 方法定义<a name="section54232412"></a>

GetObjectRequest.setProgressListener\([ProgressListener](#obs_21_0604_table06508445110) [progressListener](#obs_21_0604_table06508445110)\)

## 参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressListener|ProgressListener|必选|**参数解释：**设置数据传输监听器，用于获取下载进度，详见ProgressListener。|


**表 2**  ProgressListener\(传输进度接口\)成员如下

|**方法名称**|**返回值类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressChanged|void|必选|**参数解释：**获取上传进度，详见progressChanged。|


**表 3**  progressChanged参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|status|ProgressStatus|必选|**参数解释：**传输进度数据.，详见ProgressStatus。|


**表 4**  ProgressStatus方法

|**方法名称**|**返回值类型**|**说明**|
|--|--|--|
|getAverageSpeed()|double|上传平均速率。|
|getInstantaneousSpeed()|double|上传瞬时速率。|
|getTransferPercentage()|int|上传进度百分比。|
|getNewlyTransferredBytes()|long|新增的字节数。|
|getTransferredBytes()|long|已传输的字节数。|
|getTotalBytes()|long|待传输的字节数。|


## 代码示例<a name="section583344231112"></a>

本示例用于获取下载examplebucket桶中objectname对象时的进度。示例代码如下：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.GetObjectRequest;
import com.obs.services.model.ObsObject;
import com.obs.services.model.ProgressListener;
import com.obs.services.model.ProgressStatus;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
public class GetObject003 {
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
            // 获取下载进度
            GetObjectRequest request = new GetObjectRequest("examplebucket", "objectname");
            request.setProgressListener(
                    new ProgressListener() {
                        @Override
                        public void progressChanged(ProgressStatus status) {
                            // 获取下载平均速率
                            System.out.println("AverageSpeed:" + status.getAverageSpeed());
                            // 获取下载进度百分比
                            System.out.println("TransferPercentage:" + status.getTransferPercentage());
                        }
                    });
            // 每下载1MB数据反馈下载进度
            request.setProgressInterval(1024 * 1024L);
            ObsObject obsObject = obsClient.getObject(request);
            // 读取对象内容
            System.out.println("Object content:");
            InputStream input = obsObject.getObjectContent();
            byte[] b = new byte[1024];
            ByteArrayOutputStream bos = new ByteArrayOutputStream();
            int len;
            while ((len = input.read(b)) != -1) {
                bos.write(b, 0, len);
            }
            System.out.println("getObjectContent successfully");
            System.out.println(new String(bos.toByteArray()));
            bos.close();
            input.close();
        } catch (ObsException e) {
            System.out.println("getObjectContent failed");
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
            System.out.println("getObjectContent failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于下载对象的API说明，请参见[获取对象内容](https://support.huaweicloud.com/api-obs/obs_04_0083.html)。
-   更多关于下载对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/DownloadFileSample.java)。
-   下载对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   下载对象常见问题请参见[下载对象失败](https://support.huaweicloud.com/obs_faq/obs_faq_0135.html)。

