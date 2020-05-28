# 创建IAM用户并授权使用OBS<a name="obs_03_0122"></a>

如果您需要对您所拥有的OBS资源进行精细的权限管理，您可以使用[统一身份认证服务](https://support.huaweicloud.com/usermanual-iam/iam_01_0001.html)（Identity and Access Management，简称IAM），通过IAM，您可以：

-   根据企业的业务组织，在您的华为云账号中，给企业中不同职能部门的员工创建IAM用户，让员工拥有唯一安全凭证，并使用OBS资源。
-   根据企业用户的职能，设置不同的访问权限，以达到用户之间的权限隔离。
-   将OBS资源委托给更专业、高效的其他华为云账号或者云服务，这些账号或者云服务可以根据权限进行代运维。

如果华为云账号已经能满足您的要求，不需要创建独立的IAM用户，您可以跳过本章节，不影响您使用OBS服务的其它功能。

本章节为您介绍对用户授权的方法，操作流程如[图1](#fig292324264713)所示。

## 前提条件<a name="section15304115717917"></a>

给用户组授权之前，请您了解用户组可以添加的OBS权限，并结合实际需求进行选择，OBS支持的系统权限，请参见：[OBS系统权限](https://support.huaweicloud.com/productdesc-obs/obs_03_0045.html)。若您需要对除OBS之外的其它服务授权，IAM支持服务的所有权限请参见[系统权限](https://support.huaweicloud.com/permissions/policy_list.html?product=obs)。

## 示例流程<a name="section35143124418"></a>

**图 1**  为IAM用户授权OBS资源权限<a name="fig292324264713"></a>  
![](figures/为IAM用户授权OBS资源权限.png "为IAM用户授权OBS资源权限")

1.  <a name="li64462106181"></a>[创建用户组并授权](https://support.huaweicloud.com/usermanual-iam/iam_03_0001.html)

    在IAM控制台创建用户组，并授予对象存储服务“OBS ReadOnlyAccess”权限。

2.  [创建用户并加入用户组](https://support.huaweicloud.com/usermanual-iam/iam_02_0001.html)

    在IAM控制台创建用户，并将其加入[1](#li64462106181)中创建的用户组。

3.  [用户登录](https://support.huaweicloud.com/usermanual-iam/iam_01_0552.html)并验证权限

    新创建的用户登录控制台，验证权限：

    -   在服务列表中选择“对象存储服务 OBS”，进入OBS主界面，若能显示账号下的桶列表，单击任意桶名称，在对象列表能显示桶中对象，但无法执行上传下载等其他操作，表示“OBS ReadOnlyAccess”已生效。
    -   在OBS桶列表页面左侧导航栏，选择“CDN”，若提示权限不足，表示“OBS ReadOnlyAccess”已生效。


