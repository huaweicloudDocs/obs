# 无法在浏览器中打开对象URL<a name="zh-cn_topic_0045828985"></a>

## 问题<a name="s66d8cfd6480c42f7b4ec7ece2c9336ab"></a>

为什么无法在浏览器中打开对象URL？

## 回答<a name="s6d21c5d0d89f47149100d6f837e85244"></a>

-   若通过对象URL访问对象时，出现类似于如下的错误提示，则需先在OBS管理控制台为该对象开启“匿名用户”的“读取权限”。权限开启后，请按照[通过对象URL访问对象](通过对象URL访问对象.md)中步骤3重试。

    ```
    <Error>
        <Code>AccessDenied</Code>
        <Message>Access Denied</Message>
        <RequestId>000173811E0000015B18BC86A3FBD65I</RequestId>
        <HostId>
         bcmaSevE9j9tY/Mg646E5xkF5D2jTbHcmxXt6TEfICxLLgbauVuxjJ3hL8zfH+B2
        </HostId>
        </Error>
    ```


-   若通过对象URL访问对象时，出现类似于如下的错误提示，则表示该对象为已加密对象，已加密的对象不支持通过对象URL访问。

    ```
    <Error>
        <Code>InvalidRequest</Code>
        <Message>
        The object was stored using a form of Server Side Encryption. The correct parameters must be provided to retrieve the object.
        </Message>
        <RequestId>000173811E0000015B282B2D4D98C59P</RequestId>
        <HostId>
        heAWAu3VYmy64mS9biPT6mT37aGWb3sIFx6WJuxzyUW9+VRAcLOu4gPRquZOp+St
        </HostId>
        </Error>
    ```


