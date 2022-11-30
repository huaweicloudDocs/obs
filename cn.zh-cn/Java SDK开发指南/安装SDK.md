# 安装SDK<a name="obs_21_0105"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。[接口参考文档](https://obssdk.obs.cn-north-1.myhuaweicloud.com/apidoc/cn/java/index.html)详细介绍了每个接口的参数和使用方法。

方式一，使用Maven中央仓库下载安装OBS Java SDK，支持使用maven配置和gradle配置，步骤如下：

-   使用maven配置

    打开maven工程的pom.xml，在“<dependencies\>”节点中加入以下配置：

    ```
    <dependency>
       <groupId>com.huaweicloud</groupId>
       <artifactId>esdk-obs-java-bundle</artifactId>
       <version>[3.21.11,)</version>
    </dependency>
    <!--若您的项目对三方依赖占用空间大小较为敏感，可使用下方代码引用非 bundle 版 SDK。具体差别见说明-->
    <!--<dependency>-->
    <!--	<groupId>com.huaweicloud</groupId>-->
    <!--	<artifactId>esdk-obs-java</artifactId>-->
    <!--	<version>[3.21.8,)</version>-->
    <!--</dependency>-->
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   esdk-obs-java-bundle 与 esdk-obs-java 的源代码相同，区别在于 Bundle 版将所有三方依赖打包并重定向至包内，不再依赖外部三方包，可避免因依赖冲突导致的问题，相应的 Bundle 版 SDK 占用的空间也更大（7M+）。在使用 esdk-obs-java 的过程中遇到依赖冲突问题时，可参考  [依赖缺失和依赖冲突的解决](依赖缺失和依赖冲突的解决.md)  解决。
    >-   由于 Spring-boot 的依赖管理机制，会自动将 OBS SDK 所指定的依赖 okhttp 4.8.0 降级至 okhttp 3.x 版本，导致 SDK 不可用，当您的项目同时包含 Spring-boot 与非 bundle 版 SDK 时，请在您的 pom 文件中显式的引用 okhttp4.8.0 版本，点[这里](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/pom.xml)获取okhttp的maven坐标。

-   使用gradle配置

    打开gradle工程的build.gradle，在“dependencies”中加入以下配置：

    ```
    api 'com.huaweicloud:esdk-obs-java-bundle:3.21.8'
    // 若您的项目对三方依赖占用空间大小较为敏感，可使用下方代码引用非 bundle 版 SDK。具体差别见说明
    // api 'com.huaweicloud:esdk-obs-java:3.21.8'
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >esdk-obs-java-bundle 与 esdk-obs-java 的源代码相同，区别在于 Bundle 版将所有三方依赖打包并重定向至包内，不再依赖外部三方包，可避免因依赖冲突导致的问题，相应的 Bundle 版 SDK 占用的空间也更大（7M+）。在使用 esdk-obs-java 的过程中遇到依赖冲突问题时，可参考  [依赖缺失和依赖冲突的解决](依赖缺失和依赖冲突的解决.md)  解决。


方式二，使用镜像库下载安装OBS Java SDK，以Maven为例，步骤如下：

1.  使用浏览器打开华为开源镜像站：[https://mirrors.huaweicloud.com](https://mirrors.huaweicloud.com)。
2.  从打开站点的网页中，找到“HuaweiCloud SDK”面板并单击进入依赖管理工具配置说明页面。
3.  在依赖管理工具配置说明页面，单击右上方的“下载配置文件”，下载并保存Maven配置文件。
4.  使用下载好的Maven配置文件（settings.xml）替换本地Maven的全局配置文件，例如windows系统中该文件通常位于**“C:\\Users\\<administrator\>\\.m2”**下。
5.  打开Maven工程的pom.xml，在“<dependencies\>”节点中加入以下配置：

    ```
    <dependency>
       <groupId>com.huaweicloud</groupId>
       <artifactId>esdk-obs-java-bundle</artifactId>
       <version>[3.21.11,)</version>
    </dependency>
    <!--若您的项目对三方依赖占用空间大小较为敏感，可使用下方代码引用非 bundle 版 SDK。具体差别见说明-->
    <!--<dependency>-->
    <!--	<groupId>com.huaweicloud</groupId>-->
    <!--	<artifactId>esdk-obs-java</artifactId>-->
    <!--	<version>[3.21.11,)</version>-->
    <!--</dependency>-->
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >esdk-obs-java-bundle 与 esdk-obs-java 的源代码相同，区别在于 Bundle 版将所有三方依赖打包并重定向至包内，不再依赖外部三方包，可避免因依赖冲突导致的问题，相应的 Bundle 版 SDK 占用的空间也更大（7M+）。在使用 esdk-obs-java 的过程中遇到依赖冲突问题时，可参考  [依赖缺失和依赖冲突的解决](依赖缺失和依赖冲突的解决.md)  解决。

6.  运行Maven命令（如：mvn package）下载SDK。

1.  下载OBS Java SDK开发包。
2.  解压该开发包。
3.  将解压后的libs文件夹下所有的JAR包拷贝到您的项目中。
4.  在Eclipse中选择您的工程，右击选择Properties \> Java Build Path \> Add JARs。
5.  选中您在第3步拷贝的所有JAR文件，单击“确定”，完成JAR包的导入。

方式三，自行编译 Jar 包，步骤如下：

1.  由  [SDK下载](SDK下载.md)  下载源码并解压。
2.  配置本地  Java 环境与 Maven 环境。
3.  通过命令行进入源码解压目录。
4.  运行如下命令

    ```
    mvn clean package -Dmaven.test.skip=true -f pom-java.xml
    ```

5.  构建产物位于解压目录中 target 目录下。

方式四，由  [SDK下载](SDK下载.md)  直接下载 Jar 包，并放置于本地工程的依赖路径。

