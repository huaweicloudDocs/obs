# 通过URL访问对象失败<a name="obs_03_0033"></a>

## 问题<a name="section891211016486"></a>

通过对象URL访问对象时，出现错误。

## 回答<a name="section24937835142144"></a>

-   若通过对象URL访问对象时，出现类似于如下的错误提示，则需先为该对象开启“匿名用户”的“读取权限”。权限开启方法请参见[应用举例：为匿名用户设置对象的访问权限](应用举例-为匿名用户设置对象的访问权限.md)。权限开启后，请按照上述步骤重试。

    ```
    <Error> 
      <Code>AccessDenied</Code>  
      <Message>Access Denied</Message>  
      <RequestId>000173811E0000015B18BC86A3FBD65I</RequestId>  
      <HostId>bcmaSevE9j9tY/Mg646E5xkF5D2jTbHcmxXt6TEfICxLLgbauVuxjJ3hL8zfH+B2</HostId> 
    </Error>
    ```


-   若通过对象URL访问对象时，出现类似于如下的错误提示，则表示该对象为已加密对象，已加密的对象不支持通过对象URL访问。

    ```
    <Error> 
      <Code>InvalidArgument</Code>  
      <Message>Requests specifying Server Side Encryption with KMS managed keys require Signature Version 4.</Message>  
      <RequestId>000173811E0000015B18C601893BBEFQ</RequestId>  
      <HostId>B8OwldJm/6tRwVx1ONJ/ilTioZnndywWyWPgs3jF/zCyOARICV+dfn0XkXTh8vjW</HostId>  
      <ArgumentName>Authorization</ArgumentName>  
      <ArgumentValue>null</ArgumentValue> 
    </Error>
    ```


