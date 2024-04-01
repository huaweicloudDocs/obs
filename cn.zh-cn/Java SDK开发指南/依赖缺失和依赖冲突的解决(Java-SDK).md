# 依赖缺失和依赖冲突的解决\(Java SDK\)<a name="obs_21_0303"></a>

依赖缺失和依赖冲突是 Java 开发中的常见问题，在集成 SDK 的过程中也会遇到，在应用编译和运行时报错 ClassNotFoundException 与  NoClassDefFoundError 时可怀疑是否是依赖问题而导致，针对不同情况参照下述步骤进行排查和解决。

## 依赖缺失<a name="section1168245414421"></a>

通过 maven 等包管理插件引入 OBS SDK 时，包管理工具会自动下载相关依赖，其他情况下需要您自行下载依赖包并添加至工程，最新版 SDK 依赖的三方组件与版本如下：

|依赖库名称|版本号|作用|
|--|--|--|
|okhttp|4.9.1|发送HTTP请求的组件|
|okio|2.7.0|okhttp的配套组件|
|java-xmlbuilder|1.3|构建和解析XML的组件|
|jackson-core|2.12.5|构建和解析JSON的组件|
|jackson-databind|2.12.5|jackson-core的配套组件|
|jackson-annotations|2.12.5|jackson-core的配套组件|


其他版本的依赖三方库可参考 Maven 中心仓库中 SDK 的 Compile Dependencies 说明。

## 依赖冲突<a name="section09819387016"></a>

当您项目中存在多个版本的 OBS Java SDK 软件包，或多个版本的第三方依赖库时，有可能会产生依赖冲突问题。当存在旧版本 SDK 时，建议您删除旧版本软件包，升级至新版；当存在多个版本的第三方依赖库时，请将产生冲突的三方依赖替换为 SDK 的指定版本。

## 使用 Bundle 包<a name="section193511829420"></a>

当您的工程存在多种三方依赖包，或多个版本的三方依赖包而又无法删除时，可使用 Bundle 版 SDK。该 Bundle 包中打包了除了 log4j 以外的所有三方依赖，可以不依赖其他三方软件包直接使用，相应的，Bundle 包大小也比普通 SDK 更大，在空间敏感的场景下请评估后使用。Bundle 包的 maven 配置如下：

```
<dependency>
    <groupId>com.huaweicloud</groupId>
    <artifactId>esdk-obs-java-bundle</artifactId>
    <version>[3.21.11,)</version>
</dependency>
```

