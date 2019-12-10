# 创建OBS客户端<a name="ZH-CN_TOPIC_0142815570"></a>

OBS客户端（ObsClient）是访问OBS服务的Java客户端，它为调用者提供一系列与OBS服务进行交互的接口，用于管理、操作桶（Bucket）和对象（Object）等OBS服务上的资源。使用OBS Java SDK向OBS发起请求，您需要初始化一个ObsClient实例，并根据需要修改ObsConfiguration的默认配置项。

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
        >当应用程序部署在ECS服务器上时，使用以上方式创建的OBS客户端会从ECS服务器自动获取临时访问密钥和定期自动刷新。  

        >![](public_sys-resources/icon-notice.gif) **须知：**   
        >请确保服务端和应用程序部署所在环境的UTC时间一致，否则可能会导致临时访问密钥无法及时刷新。  



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
>-   您的工程中可以有多个ObsClient，也可以只有一个ObsClient。  
>-   ObsClient是线程安全的，可在并发场景下使用。  

>![](public_sys-resources/icon-notice.gif) **须知：**   
>ObsClient在调用ObsClient.close方法关闭后不能再次使用。  

