# 创建OBS客户端<a name="obs_21_0202"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。[接口参考文档](https://obssdk.obs.cn-north-1.myhuaweicloud.com/apidoc/cn/java/index.html)详细介绍了每个接口的参数和使用方法。

OBS客户端（ObsClient）是访问OBS服务的Java客户端，它为调用者提供一系列与OBS服务进行交互的接口，用于管理、操作桶（Bucket）和对象（Object）等OBS服务上的资源。使用OBS Java SDK向OBS发起请求，您需要初始化一个ObsClient实例，并根据需要修改ObsConfiguration的默认配置项。您可以参考[终端节点（Endpoint）](https://support.huaweicloud.com/productdesc-obs/obs_03_0152.html)，了解Endpoint的获取方式。

-   直接使用服务地址创建OBS客户端（ObsClient），所有配置均为默认值，且后续不支持修改。
    -   永久访问密钥（AK/SK）创建OBS客户端的代码如下:

        ```
        String endPoint = "https://your-endpoint";
        String ak = "*** Provide your Access Key ***";
        String sk = "*** Provide your Secret Key ***";
        // 创建ObsClient实例
        ObsClient obsClient = new ObsClient(ak, sk, endPoint);
         
        // 使用访问OBS
                
        // 关闭obsClient
        obsClient.close();
        ```

    -   临时访问密钥（AK/SK/SecurityToken）创建OBS客户端的代码如下：

        ```
        String endPoint = "https://your-endpoint";
        String ak = "*** Provide your Access Key ***";
        String sk = "*** Provide your Secret Key ***";
        String securityToken = "*** Provide your Security Token ***"; 
        // 创建ObsClient实例
        ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);
         
        // 使用访问OBS
                
        // 关闭obsClient
        obsClient.close();
        ```

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >您可以参考[示例程序](示例程序.md)，进一步了解临时AK/SK/SecurityToken的获取方式和使用方式。


    -   使用BasicCredentialsProvider创建OBS客户端的代码如下：

        ```
        String endPoint = "https://your-endpoint";
        String ak = "*** Provide your Access Key ***";
        String sk = "*** Provide your Secret Key ***";
        // 创建ObsClient实例
        ObsClient obsClient = new ObsClient(new BasicObsCredentialsProvider(ak, sk), endPoint);
         
        // 使用访问OBS
                
        // 关闭obsClient
        obsClient.close();
        ```

    -   使用EnvironmentVariableObsCredentialsProvider创建OBS客户端的代码如下：

        ```
        String endPoint = "https://your-endpoint";
        // 创建ObsClient实例
        ObsClient obsClient = new ObsClient(new EnvironmentVariableObsCredentialsProvider(), endPoint);
         
        // 使用访问OBS
                
        // 关闭obsClient
        obsClient.close();
        ```

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >以上方式会在环境变量里寻找访问密钥，需要在环境变量中定义OBS\_ACCESS\_KEY\_ID和OBS\_SECRET\_ACCESS\_KEY分别代表永久的AK和SK。

    -   使用EcsObsCredentialsProvider创建OBS客户端的代码如下：

        ```
        String endPoint = "https://your-endpoint";
        // 创建ObsClient实例
        ObsClient obsClient = new ObsClient(new EcsObsCredentialsProvider(), endPoint);
         
        // 使用访问OBS
                
        // 关闭obsClient
        obsClient.close();
        ```

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >当应用程序部署在ECS服务器上时，并且ECS绑定了IAM对ECS的云服务委托，并给委托配置OBS权限，使用以上方式ObsClient会从ECS服务器自动获取临时访问密钥和定期自动刷新。

        >![](public_sys-resources/icon-notice.gif) **须知：** 
        >1.  请确保服务端和应用程序部署所在环境的UTC时间一致，否则可能会导致临时访问密钥无法及时刷新。
        >2.  使用该方式创建客户端时，SDK会请求固定IP（169.254.169.254）的API获取临时AKSK，具体请参见[在ECS上获取Security Key](https://support.huaweicloud.com/usermanual-ecs/ecs_03_0166.html#section7)。



-   除了上述指定一种方式获取访问密钥外，您还可以以链式的形式从环境变量及ECS服务器上进行搜索以获取对应的访问密钥。
    -   使用链式方式创建OBS客户端的代码如下：

        ```
        String endPoint = "https://your-endpoint";
        // 创建ObsClient实例
        ObsClient obsClient = new ObsClient(new OBSCredentialsProviderChain(), endPoint);
         
        // 使用访问OBS
                
        // 关闭obsClient
        obsClient.close();
        ```

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >以上方式指定以链式的方式从预定义方式列表中搜索访问密钥。当前默认提供从环境变量中以及从ECS服务器上获取访问密钥两种预定义搜索方式，并按照先从环境变量，再从ECS服务器的顺序进行搜索。链式搜索方式会以第一组成功获取到的访问密钥创建OBS客户端。


-   使用可定制各参数的配置类（ObsConfiguration）创建OBS客户端（ObsClient），创建完成后不支持再次修改参数，具体可配置的参数参见[配置OBS客户端](配置OBS客户端.md)。以上创建OBS客户端方式均支持使用配置类进行创建，示例代码如下：

```
String endPoint = "https://your-endpoint";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";

// 创建ObsConfiguration配置类实例
ObsConfiguration config = new ObsConfiguration();
config.setEndPoint(endPoint);
config.setSocketTimeout(30000);
config.setMaxErrorRetry(1);

// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, config);

// 使用Provider创建ObsClient实例
// ObsClient obsClient = new ObsClient(new EnvironmentVariableObsCredentialsProvider(), config);
// ObsClient obsClient = new ObsClient(new EcsObsCredentialsProvider(), config);

// 使用访问OBS

// 关闭obsClient
obsClient.close();
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   建议整个代码工程全局使用一个ObsClient客户端，只在程序初始化时创建一次，因为创建多个ObsClient客户端在高并发场景下会影响性能。
>-   在使用临时aksk时，aksk会有过期时间，可调用ObsClient.refresh\("yourAccessKey", "yourSecretKey", "yourSecurityToken"\)刷新ObsClient的aksk，不必重新创建ObsClient。
>-   ObsClient是线程安全的，可在并发场景下使用。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>ObsClient在调用ObsClient.close方法关闭后不能再次使用，保证全局使用一个ObsClient客户端的情况下，不建议主动关闭ObsClient客户端。

