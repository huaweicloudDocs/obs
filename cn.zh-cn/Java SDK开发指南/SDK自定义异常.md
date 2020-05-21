# SDK自定义异常<a name="obs_21_2005"></a>

SDK自定义异常（ObsException）是由ObsClient统一抛出的异常，继承自java.lang.RuntimeException类。通常是OBS服务端错误，包含[OBS错误码](OBS服务端错误码.md)、错误信息等，便于用户定位问题，并做出适当的处理。

ObsException通常包含以下错误信息：

-   ObsException.getResponseCode：HTTP状态码。
-   ObsException.getErrorCode：OBS服务端错误码。
-   ObsException.getErrorMessage：OBS服务端错误描述。
-   ObsException.getErrorRequestId：OBS服务端返回的请求ID。
-   ObsException.getErrorHostId：请求的服务端ID。
-   ObsException.getResponseHeaders：HTTP响应头信息。

