# 配置SDK验证服务端证书<a name="ZH-CN_TOPIC_0142815523"></a>

OBS Java SDK提供了对服务端证书验证的支持，以确保OBS服务来自于受信服务端。以Windows操作系统为例（Linux操作系统下请将%JAVA\_HOME%修改为$JAVA\_HOME），配置验证服务端证书的步骤如下：

>![](public_sys-resources/icon-note.gif) **说明：**   
>如果访问的OBS服务端的根证书是由权威机构颁发的，可以忽略步骤1、2、3（JDK的证书库中默认已加入了权威机构的根证书）。  

1.  获取OBS服务端的根证书（例如从IE浏览器的“Internet属性 \> 内容 \> 证书”中导出），并保存为文件obs.cer。
2.  运行命令**%JAVA\_HOME%/bin/keytool -import -alias obs -file obs.cer -storepass changeit -keystore %JAVA\_HOME%/jre/lib/security/cacerts**导入证书。
3.  运行命令**%JAVA\_HOME%/bin/keytool -list -v -alias obs -storepass changeit -keystore %JAVA\_HOME%/jre/lib/security/cacerts**查看证书是否导入成功。
4.  配置OBS客户端开启服务端证书验证ObsConfiguration.setValidateCertificate\(true\)。

