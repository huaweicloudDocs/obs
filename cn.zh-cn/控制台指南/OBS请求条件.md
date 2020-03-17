# OBS请求条件<a name="obs_03_0155"></a>

您可以在创建自定义策略时，通过添加“请求条件”（Condition元素）来控制策略何时生效。请求条件包括条件键和运算符，条件键表示策略语句的Condition元素，分为全局级条件键和服务级条件键。[全局级条件键](https://support.huaweicloud.com/usermanual-iam/iam_01_0017.html)（前缀为g:）适用于所有操作，服务级条件键（前缀为服务缩写，如obs:）仅适用于对应服务的操作。运算符与条件键一起使用，构成完整的条件判断语句。

OBS通过IAM预置了一组条件键，例如，您可以先使用obs:SourceIp条件键检查请求者的IP地址，然后再允许执行操作。

OBS支持的条件键和运算符与桶策略的Condition一致，在IAM配置时需要在前面加上“obs:”。详细的Condition介绍请参见[Policy格式](https://support.huaweicloud.com/devg-obs/obs_06_0048.html)。

