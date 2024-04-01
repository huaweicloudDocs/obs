# 使用前准备\(Java SDK\)<a name="obs_21_0102"></a>

在使用Java SDK访问华为云对象存储服务OBS之前，您需要先完成服务环境的准备和开发环境的准备。服务环境准备包括准备华为账号和访问密钥，是使用SDK与OBS云服务交互的必要条件。开发环境准备是指为了您能顺利完成SDK的安装、完成基于SDK的代码开发与运行，需要提前在本地完成开发环境的搭建，比如下载安装依赖软件、安装开发工具等。

## 准备华为账号<a name="section11551158392"></a>

使用OBS之前您必须要有一个华为账号。申请华为账号步骤详见：[注册华为账号并开通华为云](https://support.huaweicloud.com/usermanual-account/account_id_001.html)。

## 准备访问密钥<a name="section458414452394"></a>

OBS通过用户账号中的AK和SK进行签名验证，确保通过授权的账号才能访问指定的OBS资源。获取访问密钥前，请确保访问OBS的IAM子用户已开启编程访问，开启方式详见[修改或查看IAM用户信息](https://support.huaweicloud.com/usermanual-iam/iam_02_0002.html#section0)。以下是对AK和SK的解释说明：

-   AK：Access Key ID，接入键标识，用户在对象存储服务系统中的接入键标识，一个接入键标识唯一对应一个用户，一个用户可以同时拥有多个接入键标识。对象存储服务系统通过接入键标识识别访问系统的用户。
-   SK：Secret Access Key，安全接入键，用户在对象存储服务系统中的安全接入键，是用户访问对象存储服务系统的密钥，用户根据安全接入键和请求头域生成鉴权信息。安全接入键和接入键标识一一对应。

访问密钥分永久访问密钥（AK/SK）和临时访问密钥（AK/SK和SecurityToken）两种。每个用户最多可创建两个有效的永久访问密钥。临时访问密钥只在设置的有效期内能够访问OBS，过期后需要重新获取。出于安全性考虑，建议您使用临时访问密钥访问OBS，或使用永久访问密钥访问OBS时，定期更新您的访问密钥（AK/SK）。两种密钥的获取方式如下。

-   永久访问密钥：
    1.  登录OBS控制台。
    2.  单击页面右上角的用户名，并选择“我的凭证”。
    3.  在“我的凭证”页面，单击左侧导航栏的“访问密钥”。
    4.  在“访问密钥”页面，单击“新增访问密钥”。
    5.  在弹出的“新增访问密钥”对话框中，输入登录密码和对应验证码。

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >-   用户如果未绑定邮箱和手机，则只需输入登录密码。
        >-   用户如果同时绑定了邮箱和手机，可以选择其中一种方式进行验证。

    6.  单击“确定”。
    7.  在弹出的“下载确认”提示框中，单击“确定”后，密钥会直接保存到浏览器默认的下载文件夹中。
    8.  打开下载下来的“credentials.csv”文件既可获取到访问密钥（AK和SK）。

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >-   每个用户最多可创建两个有效的访问密钥。
        >-   为防止访问密钥泄露，建议您将其保存到安全的位置。如果用户在此提示框中单击“取消”，则不会下载密钥，后续也将无法重新下载。如果需要使用访问密钥，可以重新创建新的访问密钥。

-   临时访问密钥：

    临时AK/SK和SecurityToken是系统颁发给用户的临时访问令牌，通过接口设置有效期，范围为15分钟至24小时，过期后需要重新获取。临时AK/SK和SecurityToken遵循权限最小化原则。使用临时AK/SK鉴权时，临时AK/SK和SecurityToken必须同时使用。

    获取临时访问密钥的接口请参考[获取临时AK/SK和securitytoken](https://support.huaweicloud.com/api-iam/iam_04_0002.html)。

    >![](public_sys-resources/icon-notice.gif) **须知：** 
    >OBS属于全局级服务，所以在获取临时访问密钥时，需要设置Token的使用范围取值为domain，表示获取的Token可以作用于全局服务，全局服务不区分项目或者区域。

## 准备开发环境<a name="section19499111413511"></a>

-   从[Oracle官网](http://www.oracle.com/technetwork/java/archive-139210.html)下载并安装推荐使用的JDK版本。推荐使用的JDK版本：JDK 8及以上版本。
-   从[Eclipse官网](http://www.eclipse.org/downloads/eclipse-packages/)下载并安装Eclipse IDE for Java Developers最新版本。

