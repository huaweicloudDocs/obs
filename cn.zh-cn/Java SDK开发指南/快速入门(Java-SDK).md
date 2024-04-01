# 快速入门\(Java SDK\)<a name="obs_21_0100"></a>

本节介绍在完成SDK的下载和安装后，如何快速上手使用OBS的基础功能，完成创建桶、上传下载对象、列举对象和删除对象。

## 入门准备<a name="section16220111719211"></a>

使用SDK管理OBS资源，您需要先完成以下几项准备工作：

1.  [使用前须知\(Java SDK\)](使用前须知(Java-SDK).md)：了解并选择合适的SDK版本。
2.  [使用前准备\(Java SDK\)](使用前准备(Java-SDK).md)：完成服务环境和开发环境准备。
3.  [下载与安装SDK\(Java SDK\)](下载与安装SDK(Java-SDK).md)：下载SDK并完成安装。

## 创建桶<a name="section11761013151619"></a>

以下代码展示了创建一个名为examplebucket的桶，设置桶所在区域为华北-北京四，设置桶权限为私有，存储类别为标准存储，存储冗余类别为单AZ。了解更多请参见[创建桶\(Java SDK\)](创建桶(Java-SDK).md)。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.AccessControlList;
import com.obs.services.model.AvailableZoneEnum;
import com.obs.services.model.CreateBucketRequest;
import com.obs.services.model.ObsBucket;
import com.obs.services.model.StorageClassEnum;

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
            CreateBucketRequest request = new CreateBucketRequest();
            //示例桶名
            String exampleBucket = "examplebucket";
            //示例桶区域位置
            String exampleLocation = "cn-north-4";
            request.setBucketName(exampleBucket);
            // 设置桶访问权限为私有读写，默认也是私有读写
            request.setAcl(AccessControlList.REST_CANNED_PRIVATE);
            // 设置桶的存储类别为标准存储
            request.setBucketStorageClass(StorageClassEnum.STANDARD);
            // 设置桶区域位置(以区域为华北-北京四为例)，location 需要与 endpoint的位置信息一致
            request.setLocation(exampleLocation);
            // 指定创建多AZ桶，如果不设置，默认创建单AZ桶
            request.setAvailableZone(AvailableZoneEnum.MULTI_AZ);
            // 创建桶
            ObsBucket bucket = obsClient.createBucket(request);
            // 创建桶成功
            System.out.println("CreateBucket successfully");
            System.out.println("RequestId:"+bucket.getRequestId());


        } catch (ObsException e) {
            System.out.println("CreateBucket failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code: " + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message: " + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
        } catch (Exception e) {
            System.out.println("CreateBucket failed");
            // 其他异常信息打印
            e.printStackTrace();

        }
    }
}

```

## 上传对象<a name="section6561717181613"></a>

以下代码展示了向名为examplebucket的桶中上传2个对象，一个对象本地文件名为localfile，上传到桶中是名为objectkey，另一个对象本地文件名为localfile2，上传到桶中是名为objectkey2。了解更多请参见[上传对象\(Java SDK\)](上传对象(Java-SDK).md)。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.PutObjectRequest;
import java.io.File;
public class PutObject004 {
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
            // localfile为待上传的本地文件路径，需要指定到具体的文件名
            obsClient.putObject("examplebucket", "objectkey", new File("localfile"));
            // localfile2 为待上传的本地文件路径，需要指定到具体的文件名
            PutObjectRequest request = new PutObjectRequest();
            request.setBucketName("examplebucket");
            request.setObjectKey("objectkey2");
            request.setFile(new File("localfile2"));
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

## 下载对象<a name="section1322111219168"></a>

以下代码展示了下载examplebucket桶中名为objectname的对象。了解更多请参见[下载对象\(Java SDK\)](下载对象(Java-SDK).md)。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ObsObject;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
public class GetObject001 {
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
            // 流式下载
            ObsObject obsObject = obsClient.getObject("examplebucket", "objectname");
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

## 列举对象<a name="section112431224121610"></a>

以下代码展示了列举名为examplebucket桶中的对象。了解更多请参见[列举对象\(Java SDK\)](列举对象(Java-SDK).md)。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ObjectListing;
import com.obs.services.model.ObsObject;
public class ListObjects001 {
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
            // 简单列举
            ObjectListing result = obsClient.listObjects("examplebucket");
            for (ObsObject obsObject : result.getObjects()) {
                System.out.println("listObjects successfully");
                System.out.println("ObjectKey:" + obsObject.getObjectKey());
                System.out.println("Owner:" + obsObject.getOwner());
            }
        } catch (ObsException e) {
            System.out.println("listObjects failed");
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
            System.out.println("listObjects failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 删除对象<a name="section4530132715162"></a>

以下代码展示了删除examplebucket桶中名为objectname的对象。了解更多请参见[删除对象\(Java SDK\)](删除对象(Java-SDK).md)。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
public class DeleteObject001 {
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
            // 删除单个对象
            obsClient.deleteObject("examplebucket", "objectname");
            System.out.println("deleteObject successfully");
        } catch (ObsException e) {
            System.out.println("deleteObject failed");
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
            System.out.println("deleteObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## OBS客户端通用示例<a name="section8686104202916"></a>

以下代码展示了使用OBS客户端的通用方式：

```
// 您的工程中可以只保留一个全局的ObsClient实例
// ObsClient是线程安全的，可在并发场景下使用
ObsClient obsClient = null; 
try
{
    String endPoint = "https://your-endpoint";
    // 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
    // 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
    String ak = System.getenv("ACCESS_KEY_ID");
    String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    // 创建ObsClient实例
    obsClient = new ObsClient(ak, sk, endPoint);
    // 调用接口进行操作，例如上传对象
    HeaderResponse response = obsClient.putObject("bucketname", "objectname", new File("localfile"));  // localfile为待上传的本地文件路径，需要指定到具体的文件名
    System.out.println(response);
}
catch (ObsException e)
{
    System.out.println("HTTP Code: " + e.getResponseCode());
    System.out.println("Error Code:" + e.getErrorCode());
    System.out.println("Error Message: " + e.getErrorMessage());
    
    System.out.println("Request ID:" + e.getErrorRequestId());
    System.out.println("Host ID:" + e.getErrorHostId());
    Map<String, String> headers = e.getResponseHeaders();// 遍历Map的entry,打印所有报错相关头域
    if(headers != null){
        for (Map.Entry<String, String> header : headers.entrySet()) {    
            if(header.getKey().contains("error")){        
                System.out.println(header.getKey()+":"+header.getValue());    
            }
        }
    }
    e.printStackTrace();
}finally{
    // 关闭ObsClient实例，如果是全局ObsClient实例，可以不在每个方法调用完成后关闭
    // ObsClient在调用ObsClient.close方法关闭后不能再次使用
    if(obsClient != null){
        try
        {
            // obsClient.close();
        }
        catch (IOException e)
        {
        } 
    }
}
```

