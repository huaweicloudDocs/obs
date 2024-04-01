# 问题定位方法\(Java SDK\)<a name="obs_21_0301"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

使用OBS Java SDK对接OBS服务可能会遇到许多问题，您可以通过下面介绍的步骤进行问题分析和定位：

1.  确保使用的是OBS Java SDK的最新版本， 您可以从[这里](https://github.com/huaweicloud/huaweicloud-sdk-java-obs)下载最新版本；
2.  确保开启了OBS Java SDK日志功能，开启方式参见[日志分析](日志分析(Java-SDK).md)章节，通常建议的日志级别为WARN；
3.  确保使用OBS Java SDK的程序代码遵照[OBS客户端通用示例](快速入门(Java-SDK).md#section8686104202916)编写，所有ObsClient的接口调用都进行了异常处理，例如上传对象的示例如下：

    ```
    ObsClient obsClient = null; 
    try
    {
        String endPoint = "https://your-endpoint";
        // 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
        // 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    
        obsClient = new ObsClient(ak, sk, endPoint);
        HeaderResponse response = obsClient.putObject("bucketname", "objectname", new ByteArrayInputStream("Hello OBS".getBytes())); 
        // 可选：调用成功后，记录调用成功的HTTP状态码和服务端请求ID
        System.out.println(response.getStatusCode());
        System.out.println(response.getRequestId());
    }
    catch (ObsException e)
    {
        // 推荐：发生异常后，记录失败的HTTP状态码、服务端错误码、服务端请求ID等
        System.out.println("HTTP Code: " + e.getResponseCode());
        System.out.println("Error Code:" + e.getErrorCode());
        System.out.println("Request ID:" + e.getErrorRequestId());
        // 推荐：发生异常后，记录异常堆栈信息
        e.printStackTrace(System.out);
    }
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >您可以从[这里](SDK自定义异常(Java-SDK).md)查看关于ObsException的详细说明。

4.  当调用ObsClient的接口发生异常时，从ObsException异常或日志文件中获取[HTTP状态码](HTTP状态码(Java-SDK).md)、[OBS服务端错误码](OBS服务端错误码(Java-SDK).md)后进行对照，排查异常原因；
5.  如果通过步骤4未能排查到异常原因，可从ObsException异常或日志文件中获取OBS服务端请求ID后联系OBS服务端运维团队定位异常原因；
6.  如果从ObsException异常或日志文件中无法获取OBS服务端请求ID，请收集ObsException的异常堆栈信息并联系OBS客户端运维团队定位异常原因。

