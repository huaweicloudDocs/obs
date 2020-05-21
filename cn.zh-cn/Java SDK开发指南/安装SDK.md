# 安装SDK<a name="obs_21_0105"></a>

方式一，使用Maven中央仓库下载安装 OBS Java SDK，支持使用maven配置和gradle配置，步骤如下：

-   使用maven配置

    打开maven工程的pom.xml，在“<dependencies\>”节点中加入以下配置：

    ```
           
    <dependency>
       <groupId>com.huaweicloud</groupId>
       <artifactId>esdk-obs-java</artifactId>
       <version>3.19.7</version>
    </dependency>
    ```

-   使用gradle配置

    打开gradle工程的build.gradle，在“dependencies”中加入以下配置：

    ```
    api 'com.huaweicloud:esdk-obs-java:3.19.7'
    ```


方式二，使用镜像库下载安装OBS Java SDK，以Maven为例，步骤如下：

1.  使用浏览器打开华为开源镜像站：[https://mirrors.huaweicloud.com](https://mirrors.huaweicloud.com)。
2.  从打开站点的网页中，找到“HuaweiCloud SDK”面板并单击进入依赖管理工具配置说明页面。
3.  在依赖管理工具配置说明页面，单击右上方的“下载配置文件”，下载并保存Maven配置文件。
4.  使用下载好的Maven配置文件（settings.xml）替换本地Maven的全局配置文件，例如windows系统中该文件通常位于**“C:\\Users\\<administrator\>\\.m2”**下。
5.  打开Maven工程的pom.xml，在“<dependencies\>”节点中加入以下配置：

    ```
    <!-- OBS Java SDK -->
    <dependency>
       <groupId>com.huawei.storage</groupId>
       <artifactId>esdk-obs-java</artifactId>
       <version>3.19.7</version>
    </dependency>
    ```

6.  运行Maven命令（如：mvn package）下载SDK。

方式三，在Eclipse Java项目中导入JAR包，步骤如下：

1.  [下载](SDK下载.md)OBS Java SDK开发包。
2.  解压该开发包。
3.  将解压后的libs文件夹下所有的JAR包拷贝到您的项目中。
4.  在Eclipse中选择您的工程，右击选择 Properties \> Java Build Path \> Add JARs。
5.  选中您在第3步拷贝的所有JAR文件，单击“确定”，完成JAR包的导入。

