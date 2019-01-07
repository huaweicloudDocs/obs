# 使用IE9浏览器无法打开OBS管理控制台界面<a name="zh-cn_topic_0045828993"></a>

## 问题<a name="section64363694"></a>

在OBS管理控制台地址能够Ping通的情况下，为什么使用IE9浏览器无法打开OBS管理控制台界面？

## 回答<a name="section42402339"></a>

检查浏览器的“Internet选项”中是否勾选SSL和TLS选项，若没有，则根据以下步骤处理后再重试。

1.  打开IE9浏览器。
2.  单击页面右上角的“设置”按钮，单击“Internet选项 \> 高级”，勾选“使用SSL 2.0”，“使用SSL 3.0”，“使用TLS 1.0”，“使用TLS 1.1”，“使用TLS 1.2”，如[图1](#fig3632690019428)所示。

    **图 1**  Internet选项<a name="fig3632690019428"></a>  
    ![](figures/Internet选项.png "Internet选项")

3.  单击“确定”。

