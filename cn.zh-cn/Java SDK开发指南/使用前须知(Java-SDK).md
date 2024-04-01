# 使用前须知\(Java SDK\)<a name="obs_21_0101"></a>

本文介绍Java SDK的版本变更，并提供版本兼容性说明，以及其他使用前须知。

## 变更说明<a name="section869171493118"></a>

如[表1](#table384mcpsimp)所示，本节将为您展示Java SDK的版本变更情况和兼容性说明。

**表 1**  Java SDK版本变更及兼容性说明

|**版本**|**变更类型**|**说明**|**是否兼容**|
|--|--|--|--|
|v3.23.9.1|新功能适配第三方组件|新功能：支持设置自定义dns解析器适配第三方组件：移除 java-xmlbuilder，使用默认的javax.xml库|-|
|v3.23.9|新功能适配第三方组件|新功能：新增配置桶清单接口新增客户端加密支持在生命周期规则中配置碎片过期时间适配第三方组件：使用 okio 3.5.0 替代 okio 2.10.0使用 okhttp 4.11.0 替代 okhttp 4.10.0|是|
|v3.23.5|新功能|新功能：新增双写桶功能支持标准存储、低频存储、归档存储三种桶容量的统计|是|
|v3.23.3|新功能适配第三方组件|新功能：支持crr进度查询新增对象标签接口（设置、获取、删除 对象标签）适配第三方组件：使用 powermock-module-junit4 2.0.9 替代 powermock-module-junit4 1.6.5使用 powermock-api-mockito2 2.0.9 替代 powermock-api-mockito 1.6.5使用 mockito-core 4.11.0 替代 mockito-core 1.10.19|是|
|v3.22.12|新功能适配第三方组件|新功能：Java SDK 实现 posix accesslable相关接口适配第三方组件：使用 log4j2 2.18.0 替代 log4j2 2.17.1使用 okhttp 4.10.0 替代 okhttp 4.9.3使用 jackson-core 2.13.3 替代 jackson-core 2.13.0使用 jackson-databind 2.13.4.1 替代 jackson-databind 2.13.0使用 jackson-annotations 2.13.3 替代 jackson-annotations 2.13.0|是|
|v3.22.3|适配第三方组件|使用 log4j2 2.17.1 替代 log4j2 2.17.0使用 okhttp 4.9.3 替代 okhttp 4.9.1使用 okio 2.10.0 替代 okio 2.7.0使用 jackson-core 2.13.0 替代 jackson-core 2.12.5使用 jackson-databind 2.13.0 替代 jackson-databind 2.12.5使用 jackson-annotations 2.13.0 替代 jackson-annotations 2.12.5|是|
|v3.21.12|适配第三方组件|使用 log4j2 2.17.0 替代 log4j2 2.16.0|是|


完整的版本变更情况请参见：[ChangeLog](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/README_CN.MD)。

## 兼容性说明<a name="section87011823142810"></a>

-   推荐使用的JDK版本：JDK 8及以上版本。
-   旧版本（2.x）已不再维护，建议尽快升级至最新版。

## 其他使用前须知<a name="section1799812136145"></a>

-   请确认您已经熟悉OBS的基本概念，如[桶（Bucket）](http://support.huaweicloud.com/productdesc-obs/obs_03_0207.html)、[对象（Object）](http://support.huaweicloud.com/productdesc-obs/obs_03_0206.html)、[访问密钥（AK和SK）](http://support.huaweicloud.com/productdesc-obs/obs_03_0208.html)、[终端节点（Endpoint）和访问域名](https://support.huaweicloud.com/productdesc-obs/obs_03_0152.html)等。
-   您可以先参考[OBS客户端通用示例](快速入门(Java-SDK).md#section8686104202916)，了解OBS Java SDK接口调用的通用方式。
-   使用OBS客户端进行接口调用操作完成后，没有异常抛出，则表明返回值有效；如果抛出异常，则说明操作失败，此时可从[SDK自定义异常](SDK自定义异常(Java-SDK).md)实例中获取错误信息。
-   使用OBS客户端进行接口调用成功后，均会返回包含响应头信息的[SDK公共响应头](SDK公共响应头(Java-SDK).md)实例（或其子类实例）。
-   当前各区域特性开放不一致，部分特性只在部分区域开放，使用过程中如果接口HTTP状态码为405，请确认该区域是否支持该功能特性。您可以查看[功能总览](https://support.huaweicloud.com/function-obs/index.html)确认区域是否支持该功能特性，或者[提交工单](https://console.huaweicloud.com/ticket/#/ticketindex/createIndex)寻求技术支持。

## 技术支持渠道<a name="section944718413617"></a>

开发者社区提供的技术支持渠道如下：

-   开发过程中，您有任何问题可以在Github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

