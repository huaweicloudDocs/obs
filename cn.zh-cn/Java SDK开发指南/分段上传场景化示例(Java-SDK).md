# 分段上传场景化示例\(Java SDK\)<a name="obs_21_0618"></a>

分段上传的主要目的是解决大文件上传或网络条件较差的情况。通过使用UploadPartRequest.setOffset和UploadPartRequest.setPartSize来设置每段的起始结束位置。下面的示例代码展示了如何使用分段上传并发上传大文件。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.CompleteMultipartUploadRequest;
import com.obs.services.model.InitiateMultipartUploadRequest;
import com.obs.services.model.InitiateMultipartUploadResult;
import com.obs.services.model.PartEtag;
import com.obs.services.model.UploadPartRequest;
import com.obs.services.model.UploadPartResult;
import java.io.File;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
public class ConcurrentUploadPart001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("SECURITY_TOKEN");
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
            final String bucketName = "examplebucket";
            final String objectKey = "objectname";
            // 初始化线程池
            ExecutorService executorService = Executors.newFixedThreadPool(20);
            final File largeFile = new File("localfile");
            // 初始化分段上传任务
            InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, objectKey);
            InitiateMultipartUploadResult result = obsClient.initiateMultipartUpload(request);
            final String uploadId = result.getUploadId();
            System.out.println("\t" + uploadId + "\n");
            // 每段上传100MB
            long partSize = 100 * 1024 * 1024L;
            long fileSize = largeFile.length();
            // 计算需要上传的段数
            long partCount = fileSize % partSize == 0 ? fileSize / partSize : fileSize / partSize + 1;
            final List<PartEtag> partEtags = Collections.synchronizedList(new ArrayList<PartEtag>());
            // 执行并发上传段
            for (int i = 0; i < partCount; i++) {
                // 分段在文件中的起始位置
                final long offset = i * partSize;
                // 分段大小
                final long currPartSize = (i + 1 == partCount) ? fileSize - offset : partSize;
                // 分段号
                final int partNumber = i + 1;
                executorService.execute(
                        new Runnable() {
                            @Override
                            public void run() {
                                UploadPartRequest uploadPartRequest = new UploadPartRequest();
                                uploadPartRequest.setBucketName(bucketName);
                                uploadPartRequest.setObjectKey(objectKey);
                                uploadPartRequest.setUploadId(uploadId);
                                uploadPartRequest.setFile(largeFile);
                                uploadPartRequest.setPartSize(currPartSize);
                                uploadPartRequest.setOffset(offset);
                                uploadPartRequest.setPartNumber(partNumber);
                                UploadPartResult uploadPartResult;
                                try {
                                    uploadPartResult = obsClient.uploadPart(uploadPartRequest);
                                    System.out.println("Part#" + partNumber + " done\n");
                                    partEtags.add(
                                            new PartEtag(uploadPartResult.getEtag(), uploadPartResult.getPartNumber()));
                                } catch (ObsException e) {
                                    e.printStackTrace();
                                }
                            }
                        });
            }
            // 等待上传完成
            executorService.shutdown();
            while (!executorService.isTerminated()) {
                try {
                    executorService.awaitTermination(5, TimeUnit.SECONDS);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            // 合并段
            CompleteMultipartUploadRequest completeMultipartUploadRequest =
                    new CompleteMultipartUploadRequest(bucketName, objectKey, uploadId, partEtags);
            obsClient.completeMultipartUpload(completeMultipartUploadRequest);
            System.out.println("completeMultipartUpload successfully");
        } catch (ObsException e) {
            System.out.println("CompleteMultipartUpload failed");
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
            System.out.println("completeMultipartUpload failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

