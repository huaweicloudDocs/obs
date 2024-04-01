# 通过Header鉴权访问OBS\(Java SDK\)<a name="obs_21_0904"></a>

## 代码示例：上传对象<a name="section1246015381154"></a>

通过Header鉴权访问OBS，将“Hello OBS”字符串上传到桶examplebucket里的objectName中。

```
import com.obs.services.internal.Constants;
import com.obs.services.internal.utils.AbstractAuthentication;
import com.obs.services.model.AuthTypeEnum;
import shade.okhttp3.Call;
import shade.okhttp3.MediaType;
import shade.okhttp3.OkHttpClient;
import shade.okhttp3.Request;
import shade.okhttp3.RequestBody;
import shade.okhttp3.Response;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
import java.util.TimeZone;
public class PutObjectTemporaryHeaderToObs {
    // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
    // 您可以登录访问管理控制台获取访问密钥AK/SK
    private static String ak = System.getenv("ACCESS_KEY_ID");
    private static String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
    // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
    private static String securityToken = System.getenv("SECURITY_TOKEN");
    // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
    //private static String endPoint = System.getenv("ENDPOINT");
    // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
    private static String endPoint = "obs.cn-north-4.myhuaweicloud.com";
    private static String bucketName = "examplebucket";
    private static String objectName = "objectName";
    private static String contentType = "application/xml";
    private static Map<String, String> headers = new HashMap<>();
    public static void main(String[] args) throws Exception {
        headers.put("Content-Type", contentType);
        DateFormat dateFormat = new SimpleDateFormat("E, dd MMM yyyy HH:mm:ss z", Locale.ENGLISH);
        dateFormat.setTimeZone(TimeZone.getTimeZone("GMT"));
        Date now = new Date(System.currentTimeMillis());
        headers.put("x-obs-date", dateFormat.format(now));
        sign("PUT", "/" + bucketName + "/" + objectName);
        Request.Builder builder = new Request.Builder();
        for (Map.Entry<String, String> entry : headers.entrySet()) {
            builder.header(entry.getKey(), entry.getValue());
        }
        String url = "https://" + bucketName + "." + endPoint + "/" + objectName;
        //使用PUT请求上传对象
        Request httpRequest = builder.url(url).put(RequestBody.create(MediaType.parse(contentType), "Hello OBS".getBytes("UTF-8"))).build();
        OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
                .cache(null).build();
        Call c = httpClient.newCall(httpRequest);
        Response res = c.execute();
        System.out.println("\tStatus:" + res.code());
        if (res.body() != null) {
            System.out.println("\tContent:" + res.body().string() + "\n");
        }
        res.close();
    }
    public static void sign(String method, String url) throws Exception {
        AbstractAuthentication authentication =
                Constants.AUTHTICATION_MAP.get(AuthTypeEnum.OBS);
        String stringToSign = authentication.makeServiceCanonicalString(method, url, headers, null, Constants.ALLOWED_RESOURCE_PARAMTER_NAMES);
        System.out.println("stringToSign: " + stringToSign);
        String auth = "OBS " + ak + ":" + AbstractAuthentication.calculateSignature(stringToSign, sk);
        headers.put("Authorization", auth);
    }
}
```

## 代码示例：初始化分段上传任务<a name="section18691201810211"></a>

通过Header鉴权访问OBS，初始化多段上传任务，上传的桶名为examplebucket，对象为objectName。

```
import com.obs.services.internal.Constants;
import com.obs.services.internal.utils.AbstractAuthentication;
import com.obs.services.model.AuthTypeEnum;
import com.obs.services.model.SpecialParamEnum;
import shade.okhttp3.Call;
import shade.okhttp3.MediaType;
import shade.okhttp3.OkHttpClient;
import shade.okhttp3.Request;
import shade.okhttp3.RequestBody;
import shade.okhttp3.Response;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
import java.util.TimeZone;
public class initiateMultipartUpload {
    // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
    //private static String endPoint = System.getenv("ENDPOINT");
    // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
    private static String endPoint = "obs.cn-north-4.myhuaweicloud.com";
    private static String ak = System.getenv("ACCESS_KEY_ID");
    private static String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    private static String bucketName = "examplebucket";
    private static String objectName = "objectName";
    private static String contentType = "application/xml";
    private static Map<String, String> headers = new HashMap<>();
    public static void main(String[] args) throws Exception {
        DateFormat dateFormat = new SimpleDateFormat("E, dd MMM yyyy HH:mm:ss z", Locale.ENGLISH);
        dateFormat.setTimeZone(TimeZone.getTimeZone("GMT"));
        Date now = new Date(System.currentTimeMillis());
        headers.put("x-obs-date", dateFormat.format(now));
        sign("POST", "/" + bucketName + "/" + objectName + "?uploads");
        Request.Builder builder = new Request.Builder();
        for (Map.Entry<String, String> entry : headers.entrySet()) {
            builder.header(entry.getKey(), entry.getValue());
        }
        String url = "https://" + bucketName + "." + endPoint + "/" + objectName + "?uploads";
        //使用POST请求初始化分段上传任务
        Request httpRequest = builder.url(url).post(RequestBody.create(null, "")).build();
        OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
                .cache(null).build();
        Call c = httpClient.newCall(httpRequest);
        Response res = c.execute();
        System.out.println("\tStatus:" + res.code());
        if (res.body() != null) {
            System.out.println("\tContent:" + res.body().string() + "\n");
        }
        res.close();
    }
    public static void sign(String method, String url) throws Exception {
        AbstractAuthentication authentication =
                Constants.AUTHTICATION_MAP.get(AuthTypeEnum.OBS);
        String stringToSign = authentication.makeServiceCanonicalString(method, url, headers, null, Constants.ALLOWED_RESOURCE_PARAMTER_NAMES);
        System.out.println("stringToSign: " + stringToSign);
        String auth = "OBS " + ak + ":" + AbstractAuthentication.calculateSignature(stringToSign, sk);
        headers.put("Authorization", auth);
    }
}
```

## 代码示例：上传段<a name="section11399115119200"></a>

通过Header鉴权访问OBS，将单段上传到桶examplebucket中的对象objectName。

```
import com.obs.services.internal.Constants;
import com.obs.services.internal.utils.AbstractAuthentication;
import com.obs.services.model.AuthTypeEnum;
import shade.okhttp3.Call;
import shade.okhttp3.MediaType;
import shade.okhttp3.OkHttpClient;
import shade.okhttp3.Request;
import shade.okhttp3.RequestBody;
import shade.okhttp3.Response;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
import java.util.TimeZone;
public class UploadPart {
    // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
    //private static String endPoint = System.getenv("ENDPOINT");
    // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
    private static String endPoint = "obs.cn-north-4.myhuaweicloud.com";
    private static String ak = System.getenv("ACCESS_KEY_ID");
    private static String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    private static String bucketName = "examplebucket";
    private static String objectName = "objectName";
    private static String contentType = "application/xml";
    private static Map<String, String> headers = new HashMap<>();
    public static void main(String[] args) throws Exception {
        DateFormat dateFormat = new SimpleDateFormat("E, dd MMM yyyy HH:mm:ss z", Locale.ENGLISH);
        dateFormat.setTimeZone(TimeZone.getTimeZone("GMT"));
        Date now = new Date(System.currentTimeMillis());
        headers.put("x-obs-date", dateFormat.format(now));
        sign("PUT", "/" + bucketName + "/" + objectName + "?partNumber=1&uploadId=0000018A0CA7D2144015626C08A6067A");
        Request.Builder builder = new Request.Builder();
        for (Map.Entry<String, String> entry : headers.entrySet()) {
            builder.header(entry.getKey(), entry.getValue());
        }
        String url = "https://" + bucketName + "." + endPoint + "/" + objectName + "?partNumber=1&uploadId=0000018A0CA7D2144015626C08A6067A";
        //使用PUT请求上传对象
        Request httpRequest = builder.url(url).put(RequestBody.create(null, new byte[6 * 1024 * 1024])).build();
        OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
                .cache(null).build();
        Call c = httpClient.newCall(httpRequest);
        Response res = c.execute();
        System.out.println("\tStatus:" + res.code());
        if (res.body() != null) {
            System.out.println("\tContent:" + res.body().string() + "\n");
        }
        res.close();
    }
    public static void sign(String method, String url) throws Exception {
        AbstractAuthentication authentication =
                Constants.AUTHTICATION_MAP.get(AuthTypeEnum.OBS);
        String stringToSign = authentication.makeServiceCanonicalString(method, url, headers, null, Constants.ALLOWED_RESOURCE_PARAMTER_NAMES);
        System.out.println("stringToSign: " + stringToSign);
        String auth = "OBS " + ak + ":" + AbstractAuthentication.calculateSignature(stringToSign, sk);
        headers.put("Authorization", auth);
    }
}
```

## 代码示例：合并段<a name="section46401487217"></a>

通过Header鉴权访问OBS，实现多段上传时段的合并。

```
import com.obs.services.internal.Constants;
import com.obs.services.internal.utils.AbstractAuthentication;
import com.obs.services.model.AuthTypeEnum;
import shade.okhttp3.Call;
import shade.okhttp3.MediaType;
import shade.okhttp3.OkHttpClient;
import shade.okhttp3.Request;
import shade.okhttp3.RequestBody;
import shade.okhttp3.Response;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
import java.util.TimeZone;
public class CompeletePart {
    // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
    //private static String endPoint = System.getenv("ENDPOINT");
    // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
    private static String endPoint = "obs.cn-north-4.myhuaweicloud.com";
    private static String ak = System.getenv("ACCESS_KEY_ID");
    private static String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    private static String bucketName = "examplebucket";
    private static String objectName = "objectName";
    private static String contentType = "application/xml";
    private static Map<String, String> headers = new HashMap<>();
    public static void main(String[] args) throws Exception {
        headers.put("Content-Type", contentType);
        DateFormat dateFormat = new SimpleDateFormat("E, dd MMM yyyy HH:mm:ss z", Locale.ENGLISH);
        dateFormat.setTimeZone(TimeZone.getTimeZone("GMT"));
        Date now = new Date(System.currentTimeMillis());
        headers.put("x-obs-date", dateFormat.format(now));
        sign("POST", "/" + bucketName + "/" + objectName + "?uploadId=0000018A0CA7D2144015626C08A6067A");
        Request.Builder builder = new Request.Builder();
        for (Map.Entry<String, String> entry : headers.entrySet()) {
            builder.header(entry.getKey(), entry.getValue());
        }
        String url = "https://" + bucketName + "." + endPoint + "/" + objectName + "?uploadId=0000018A0CA7D2144015626C08A6067A";
        //使用POST请求初始化分段上传任务
        // 以下content为示例代码，需要通过列举已上传段方法的响应结果，拼装以下内容
        String content = "<CompleteMultipartUpload>";
        content += "<Part>";
        content += "<PartNumber>1</PartNumber>";
        content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
        content += "</Part>";
        content += "</CompleteMultipartUpload>";
        Request httpRequest = builder.url(url).post(RequestBody.create(MediaType.parse(contentType), content.getBytes("UTF-8"))).build();
        OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
                .cache(null).build();
        Call c = httpClient.newCall(httpRequest);
        Response res = c.execute();
        System.out.println("\tStatus:" + res.code());
        if (res.body() != null) {
            System.out.println("\tContent:" + res.body().string() + "\n");
        }
        res.close();
    }
    public static void sign(String method, String url) throws Exception {
        AbstractAuthentication authentication =
                Constants.AUTHTICATION_MAP.get(AuthTypeEnum.OBS);
        String stringToSign = authentication.makeServiceCanonicalString(method, url, headers, null, Constants.ALLOWED_RESOURCE_PARAMTER_NAMES);
        System.out.println("stringToSign: " + stringToSign);
        String auth = "OBS " + ak + ":" + AbstractAuthentication.calculateSignature(stringToSign, sk);
        headers.put("Authorization", auth);
    }
}
```

## 示例代码：下载对象<a name="section11608537312"></a>

通过Header鉴权访问OBS，下载examplebucket里的objectName对象。

```
import com.obs.services.internal.Constants;
import com.obs.services.internal.utils.AbstractAuthentication;
import com.obs.services.model.AuthTypeEnum;
import shade.okhttp3.Call;
import shade.okhttp3.OkHttpClient;
import shade.okhttp3.Request;
import shade.okhttp3.Response;
import java.io.*;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.time.ZoneId;
import java.time.ZoneOffset;
import java.util.*;

public class Header_Get_Object_test {
    private static String ak = System.getenv("ACCESS_KEY_ID");
    private static String sk = System.getenv("SECRET_ACCESS_KEY_ID");
    // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
    // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
    private static String securityToken = System.getenv("SECURITY_TOKEN");
    // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
    //private static String endPoint = System.getenv("ENDPOINT");
    // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
    private static String endPoint = "obs.cn-north-4.myhuaweicloud.com";
    private static String bucketName = "examplebucket" ;
    private static String objectName = "objectkname";
    private static String contentType = "application/xml";
    private static String method = "GET";
    private static Map<String, String> headers = new HashMap<>();

    public static void main(String[] args) throws Exception { 
        headers.put("Content-Type", contentType);
        DateFormat dateFormat = new SimpleDateFormat("E, dd MMM yyyy HH:mm:ss z", Locale.ENGLISH);
        ZoneId zoneId = ZoneId.ofOffset("UTC", ZoneOffset.ofHours(8));
        TimeZone timeZone = TimeZone.getTimeZone(zoneId);
        dateFormat.setTimeZone(timeZone);
        String now = dateFormat.format(new Date(System.currentTimeMillis()));
        headers.put("x-obs-date", now);
        sign(method, "/" + bucketName + "/" + objectName);
        Request.Builder builder = new Request.Builder();
        for (Map.Entry<String, String> entry : headers.entrySet()) {
            builder.header(entry.getKey(), entry.getValue());
        }
        String url = "https://" + bucketName + "." + endPoint + "/" + objectName ;
        //使用get请求下载对象
        Request httpRequest = builder.url(url).get().build();
        OkHttpClient httpClient =
                new OkHttpClient.Builder()
                        .followRedirects(false)
                        .retryOnConnectionFailure(false)
                        .cache(null)
                        .build();
        Call c = httpClient.newCall(httpRequest);
        Response res = c.execute();
        if (res.code() < 300)
            System.out.println("Status:" + res.code());
            System.out.println("getObject successfully");
        InputStream objectContent = null;
        if (res.body() != null) {
            objectContent = res.body().byteStream();
            System.out.println("Content:" + res.body().string() + "\n");
        }
        if(objectContent != null) {
            // objectContent 就是获取的要下载的文件的文件流
            // 在这里可以读取 objectContent，长时间不读取这个流会被服务端断开连接
        }
        res.close();

    }
    public static void sign(String method, String url) throws Exception {
        AbstractAuthentication authentication =
                Constants.AUTHTICATION_MAP.get(AuthTypeEnum.OBS);
        String stringToSign = authentication.makeServiceCanonicalString(method, url, headers, null, Constants.ALLOWED_RESOURCE_PARAMTER_NAMES);
        System.out.println("stringToSign: " + stringToSign);
        String auth = "OBS " + ak + ":" + AbstractAuthentication.calculateSignature(stringToSign, sk);
        headers.put("Authorization", auth);

    }
}
```

