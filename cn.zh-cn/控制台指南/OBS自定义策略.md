# OBS自定义策略<a name="obs_03_0121"></a>

如果系统预置的OBS权限，不满足您的授权要求，可以创建自定义策略。自定义策略中可以添加的授权项（Action）请参考[桶相关授权项](https://support.huaweicloud.com/api-obs/obs_04_0111.html)和[对象相关授权项](https://support.huaweicloud.com/api-obs/obs_04_0112.html)。

目前华为云支持以下两种方式创建自定义策略：

-   可视化视图创建自定义策略：无需了解策略语法，按可视化视图导航栏选择云服务、操作、资源、条件等策略内容，可自动生成策略。
-   JSON视图创建自定义策略：可以在选择策略模板后，根据具体需求编辑策略内容；也可以直接在编辑框内编写JSON格式的策略内容。

具体创建步骤请参见：[创建自定义策略](https://support.huaweicloud.com/usermanual-iam/iam_01_0605.html)。本章为您介绍常用的OBS自定义策略样例。

## OBS自定义策略样例<a name="section10809111016198"></a>

-   示例1：给用户授予OBS的所有权限

    此策略表示用户可以对OBS进行任何操作。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "obs:*:*"
                ]
            }
        ]
    }
    ```

-   示例2：给用户授予OBS控制台的所有权限

    此策略表示用户可以在控制台对OBS进行所有操作。

    由于用户登录OBS控制台时，会访问一些其他服务的资源，如CTS审计信息，CDN加速域名，KMS密钥等。因此除了配置和示例1同样的OBS权限外，还需要配置其他服务的访问权限。其中CDN属于全局服务，CTS、KMS、SMN等属于区域级服务，需要根据您实际使用到的服务和区域分别在全局项目和对应区域项目中配置**Tenant Guest**权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "obs:*:*"
                ]
            }
        ]
    }
    ```

-   示例3：给用户授予桶的只读权限（不限定目录）

    此策略表示用户可以对桶obs-example下的所有对象进行列举和下载。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "obs:object:GetObject",
                    "obs:bucket:ListBucket"
                ],
                "Resource": [
                    "obs:*:*:object:obs-example/*",
                    "obs:*:*:bucket:obs-example"
                ]
            }
        ]
    }
    ```

-   示例4：给用户授予桶的只读权限（限定目录）

    此策略表示用户只能下载桶obs-example中“my-project/“目录下的所有对象，其他目录下的对象虽然可以列举，但无法下载。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "obs:object:GetObject",
                    "obs:bucket:ListBucket"
                ],
                "Resource": [
                    "obs:*:*:object:obs-example/my-project/*",
                    "obs:*:*:bucket:obs-example"
                ]
            }
        ]
    }
    ```

-   示例5：给用户授予桶的读写权限（限定目录）

    此策略表示用户可以对桶obs-example中“my-project“目录下的所有的对象进行列举、下载、上传和删除。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "obs:object:GetObject",
                    "obs:object:ListMultipartUploadParts",
                    "obs:bucket:ListBucket",
                    "obs:object:DeleteObject",
                    "obs:object:PutObject"
                ],
                "Resource": [
                    "obs:*:*:object:obs-example/my-project/*",
                    "obs:*:*:bucket:obs-example"
                ]
            }
        ]
    }
    ```

-   示例6：给用户授予桶的所有权限

    此策略表示用户可以对桶obs-example进行任何操作。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "obs:*:*"
                ],
                "Resource": [
                    "obs:*:*:bucket:obs-example",
                    "obs:*:*:object:obs-example/*"
                ]
            }
        ]
    }
    ```

-   示例7：拒绝用户上传对象

    拒绝策略需要同时配合其他策略使用，否则没有实际作用。用户被授予的策略中，一个授权项的作用如果同时存在Allow和Deny，则遵循**Deny优先原则**。

    如果您给用户授予OBS OperateAccess的系统策略，但不希望用户拥有OBS OperateAccess中定义的上传对象的权限，您可以创建一条拒绝上传对象的自定义策略，然后同时将OBS OperateAccess和拒绝策略授予用户，根据Deny优先原则，则用户可以执行除了上传对象外OBS OperateAccess允许的所有操作。拒绝策略示例如下：

    ```
    { 
             "Version": "1.1", 
             "Statement": [ 
                     {
                             "Effect": "Deny", 
                             "Action": [ 
                                     "obs:object:PutObject" 
                             ],
                     } 
             ] 
     }
    ```


