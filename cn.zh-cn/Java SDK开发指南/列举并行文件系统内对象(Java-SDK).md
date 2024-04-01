# 列举并行文件系统内对象\(Java SDK\)<a name="obs_21_0506"></a>

## 功能说明<a name="section179045752013"></a>

您可以通过ObsClient.listObjects列举出指定并行文件系统里的对象。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section1641216192116"></a>

-   您必须是并行文件系统拥有者或拥有列举并行文件系统内对象的权限，才能列举并行文件系统内对象。建议使用IAM或策略进行授权，如果使用IAM则需授予obs:bucket:ListBucket权限，如果使用策略则需授予ListBucket权限。建议使用IAM进行授权，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.listObjects\(final  [ListObjectsRequest](#table14455523) [request](#table16553037152015)\)

## 请求参数说明<a name="section18849343192414"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|ListObjectsRequest|必选|**参数解释：**获取并行文件系统内对象列表请求参数，详见ListObjectsRequest。|


**表 2**  ListObjectsRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|prefix|String|可选|**参数解释：**限定返回的对象名必须带有prefix前缀。**约束限制：**长度大于0且不超过1024的字符串。**默认取值：**无|
|marker|String|可选|**参数解释：**列举桶内对象列表时，指定一个标识符，从该标识符以后按对象名的字典顺序返回对象列表。**约束限制：**仅用于非多版本列举。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|maxKeys|int|可选|**参数解释：**列举对象的最大数目，返回的对象列表将是按照字典顺序的最多前maxKeys个对象。**取值范围：**1~1000，当超出范围时，按照默认的1000进行处理。**默认取值：**1000|
|delimiter|String|可选|**参数解释：**将对象名进行分组的分隔符。如果指定了prefix，从prefix到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes；如果没有指定prefix，从对象名的首字符到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes。例如，桶中有3个对象，分别为abcd、abcde、bbcde。如果指定delimiter为d，prefix为a，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefix；如果只指定delimiter为d，abcd、abcde会被分成一组，形成一条前缀为abcd的commonPrefix，而bbcde会被单独分成一组，形成一条前缀为bbcd的commonPrefix。对于并行文件系统，不携带此参数时默认列举是递归列举此目录下所有内容，会列举子目录。在大数据场景下（目录层级深、目录下文件多）的列举，建议设置[delimiter=/]，只列举当前目录下的内容，不列举子目录，提高列举效率。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|encodingType|String|可选|**参数解释：**对响应中的部分元素进行指定类型的编码。如果 delimiter、marker、prefix、nextMarker 和 objectKey 包含xml 1.0标准不支持的控制字符，可通过设置 encodingType 对响应中的 delimiter、marker、prefix（包括commonPrefixes 中的 prefix）、nextMarker 和 objectKey 进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|


## 返回结果说明<a name="section7526511258"></a>

ObsClient.listObjects返回结果如下：

**表 3**  ObjectListing

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|bucketName|String|**参数解释：**并行文件系统的并行文件系统名。**约束限制：**并行文件系统的名字需全局唯一，不能与已有的任何并行文件系统名称重复，包括其他用户创建的并行文件系统。并行文件系统命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名并行文件系统不会报错，创建的并行文件系统属性以第一次请求为准。**默认取值：**无|
|prefix|String|**参数解释：**对象名的前缀，与请求中的该参数对应。例如，假设您拥有以下对象：logs/day1、logs/day2、logs/day3和ExampleObject.jpg。如果您将logs/指定为前缀，将返回以字符串“logs/”开头的三个对象。如果您指定空的前缀且请求中没有其他过滤条件，将返回并行文件系统中的所有对象。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|objectSummaries|List<ObsObject>|**参数解释：**并行文件系统内对象列表，详见ObsObject。|
|commonPrefixes|List<String>|**参数解释：**当请求中设置了Delimiter分组字符时，返回按Delimiter分组后的对象名称前缀列表。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|truncated|boolean|**参数解释：**表明本次请求是否返回了全部结果。因为每次列举返回对象的数量上限是1000个，如果对象个数大于1000，则无法通过一次请求返回全部结果。**取值范围：**true：表示没有返回全部结果。false：表示已返回了全部结果。**默认取值：**无|
|marker|String|**参数解释：**列举对象的起始位置，与请求中的该参数对应。列举并行文件系统内对象列表时，指定一个标识符，从该标识符以后按对象名的字典顺序返回对象列表。**约束限制：**仅用于非多版本列举。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|maxKeys|int|**参数解释：**列举对象的最大数目，与请求中的该参数对应。返回的对象列表将是按照字典顺序的最多前maxKeys个对象。**取值范围：**1~1000，当超出范围时，按照默认的1000进行处理。**默认取值：**1000|
|delimiter|String|**参数解释：**对象名按照此标识符进行分组。通常与prefix参数搭配使用，如果指定了prefix，从prefix到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes；如果没有指定prefix，从对象名的首字符到第一次出现delimiter间具有相同字符串的对象名会被分成一组，形成一条CommonPrefixes。例如，并行文件系统中有3个对象，分别为abcd、abcde、bbcde。如果指定delimiter为d，prefix为a，abcd、abcde会被分成一组，形成一条前缀为abcd的CommonPrefixes；如果只指定delimiter为d，abcd、abcde会被分成一组，形成一条前缀为abcd的CommonPrefixes，而bbcde会被单独分成一组，形成一条前缀为bbcd的CommonPrefixes。对于并行文件系统，不携带此参数时默认列举是递归列举此目录下所有内容，会列举子目录。在大数据场景下（目录层级深、目录下文件多）的列举，建议设置[delimiter=/]，只列举当前目录下的内容，不列举子目录，提高列举效率。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|nextMarker|String|**参数解释：**下次列举对象请求的起始位置。如果本次没有返回全部结果，响应请求中将包含此字段，用于标明本次请求列举到的最后一个对象。后续请求可以指定Marker参数等于该值来列举剩余的对象。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|location|String|**参数解释：**并行文件系统所在的区域。**约束限制：**该参数定义了并行文件系统将会被创建在哪个区域，如果使用的终端节点是obs.myhuaweicloud.com，可以不携带此参数；如果使用的终端节点不是obs.myhuaweicloud.com，则必须携带此参数。**取值范围：**当前有效的OBS区域和终端节点的更多信息，请参考地区和终端节点。终端节点即调用API的请求地址，不同服务不同区域的终端节点不同，您可以向企业管理员获取区域和终端节点信息。**默认取值：**终端节点为obs.myhuaweicloud.com且用户未设定区域时，默认为华北-北京一（cn-north-1）。|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


**表 4**  ObsObject

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|objectKey|String|**参数解释：**对象名。对象名是对象在存储并行文件系统中的唯一标识。对象名是对象在并行文件系统中的完整路径，路径中不包含并行文件系统名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|bucketName|String|**参数解释：**并行文件系统名。**约束限制：**并行文件系统的名字需全局唯一，不能与已有的任何并行文件系统名称重复，包括其他用户创建的并行文件系统。并行文件系统命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名并行文件系统不会报错，创建的并行文件系统属性以第一次请求为准。**默认取值：**无|
|objectContent|InputStream|**参数解释：**获取对象的数据流。**默认取值：**无|
|owner|Owner|**参数解释：**对象的所有者，包含对象拥有者DomainId和对象拥有者名称，详见Owner。**默认取值：**无。|
|metadata|ObjectMetadata|**参数解释：**对象的元数据信息。**取值范围：**对象的元数据信息，详见ObjectMetadata。**默认取值：**无|


**表 5**  Owner

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|必选|**参数解释**：桶所有者的账号ID，即domain_id。**取值范围：**如何获取账号ID请参见如何获取账号ID和用户ID?。**默认取值：**无|
|displayName|String|可选|**参数解释：**所有者的账号名。**取值范围：**如何获取账号名请参见如何获取账号名?。**默认取值：**无|


**表 6**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 7**  ObjectMetadata

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|contentLength|Long|可选|**参数解释：**对象数据的长度。**约束限制：**单次上传对象大小范围是[0, 5GB]。如果需要上传超过5GB的大文件，需要通过多段操作来分段上传。**默认取值：**如果不设置，则SDK会自动计算对象数据的长度。|
|contentType|String|可选|**参数解释：**对象的文件类型（MIME类型）。contentType（MIME）用于标识发送或接收数据的类型，浏览器根据该参数来决定数据的打开方式。**取值范围：**常见的contentType（MIME）列表参见如何理解Content-Type（MIME）？(Java SDK)。**默认取值：**如果未指定Content-Type，SDK会根据指定Object名称的后缀来判定文件类型并自动填充Content-Type（如.xml判断为application/xml文件；.html判断为text/html文件）。|
|contentEncoding|String|可选|**参数解释：**响应中的Content-Encoding头。指定对象内容编码格式。**默认取值：**无|
|contentDisposition|String|可选|**参数解释：**为请求的对象提供一个默认的文件名赋值给该对象，当下载对象或者访问对象时，以默认文件名命名的文件将直接在浏览器上显示，或在弹出文件下载对话框时显示。**默认取值：**无|
|cacheControl|String|可选|**参数解释：**响应中的Cache-Control头。指定对象被下载时的网页的缓存行为。**默认取值：**无|
|contentLanguage|String|可选|**参数解释：**说明访问者希望采用的语言或语言组合，以根据自己偏好的语言来定制。详情请参见HTTP协议中关于ContentLanguage的定义。**默认取值：**无|
|expires|String|可选|**参数解释：**指对象在网页中的缓存过期时间。**约束限制：**日期格式为GMT的格式。**默认取值：**无|
|contentMd5|String|可选|**参数解释：**对象数据的MD5值（经过Base64编码），提供给OBS服务端，校验数据完整性。OBS服务端会将该MD5值与对象数据计算出的MD5值进行对比，如果不匹配则上传失败，返回HTTP 400错误。**约束限制：**对象数据的MD5值必须经过Base64编码。如果不设置对象的MD5值，OBS服务端会忽略对对象数据的MD5值校验。**取值范围：**按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过Base64编码后得到的字符串。示例：n58IG6hfM7vqI4K0vnWpog==**默认取值：**无|
|storageClass|StorageClassEnum|可选|**参数解释：**对象的存储类别。创建对象时，可以加上此头域设置对象的存储类别。如果未设置此头域，则以并行文件系统的默认存储类别作为对象的存储类别。**取值范围：**可选择的存储类别参见StorageClassEnum。**默认取值：**无|
|webSiteRedirectLocation|String|可选|**参数解释：**当并行文件系统设置了Website配置，可以将获取这个对象的请求重定向到并行文件系统内另一个对象或一个外部的URL，该参数指明对象的重定向地址。例如，重定向请求到并行文件系统内另一对象：WebsiteRedirectLocation:/anotherPage.html或重定向请求到一个外部URL：WebsiteRedirectLocation:http://www.example.com/**约束限制：**必须以“/”、“http://”或“https://”开头，长度不超过2KB。OBS仅支持为并行文件系统根目录下的对象设置重定向，不支持为并行文件系统中文件夹下的对象设置重定向。**默认取值：**无|
|nextPosition|long|可选|**参数解释：**下次追加上传的位置。**取值范围：**0~对象长度，单位：字节。**默认取值：**无|
|appendable|boolean|可选|**参数解释：**对象是否为可追加上传的对象。**取值范围：**true：是，可追加上传。false：否，不可追加上传。**默认取值：**无|
|userMetadata|Map<String, Object>|可选|**参数解释：**对象的自定义元数据，OBS支持用户使用以“x-obs-meta-”开头的消息头来加入自定义的元数据，以便对对象进行自定义管理。Map中的String代表以“x-obs-meta-”开头的自定义元数据名称，Object代表自定义元数据的值。对象的自定义元数据可以通过ObsClient.getObjectMetadata获取，参见获取对象元数据。**约束限制：**一个对象可以有多个元数据，总大小不能超过8KB。使用ObsClient.getObject下载对象时，对象的自定义元数据也会同时下载。**默认取值：**无|


## 代码示例<a name="section177128349211"></a>

本示例用于列举examplebucket并行文件系统目录下的内容。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.*;
import java.io.*;

public class ListPosixObjects{
    // 列举对象返回的最大数量
    private static int maxKey = 1000;
    private static String bucketName = "examplebucket";
    private static ObsClient obsClient;
    public static void main(String[] args) throws IOException, InterruptedException {
        // 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
        // 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
        String ak = System.getenv("OBS_ACCESS_KEY_ID");
        String sk = System.getenv("OBS_SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("OBS_SECURITY_TOKEN");
        // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
        String endPoint = System.getenv("OBS_ENDPOINT");
        // 创建ObsClient实例
        try {
            obsClient = new ObsClient(ak, sk, endPoint);
            // 列举并行文件系统内的对象
            ListObjectsRequest request = new ListObjectsRequest(bucketName);
            // 列举对象返回的最大数量
            request.setMaxKeys(maxKey);
            // 建议设置[delimiter="/"]，只列举当前目录下的内容，不列举子目录
            request.setDelimiter("/");
            listObjects(request);
        } catch (ObsException e) {
            // 请求失败,打印http状态码
            System.out.println("HTTP Code: " + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message: " + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
        } catch (Exception e) {
            // 其他异常信息打印
            e.printStackTrace();
        }
    }

    static void listObjectsByPrefix(ObjectListing result) throws ObsException {
        for (String prefix : result.getCommonPrefixes()) {
            System.out.println("Objects in folder [" + prefix + "]:");
            ListObjectsRequest request = new ListObjectsRequest(bucketName);
            // 列举对象的最大数目，取值范围为1~1000，当超出范围时，按照默认的1000进行处理
            request.setMaxKeys(maxKey);
            // 建议设置[delimiter="/"]，只列举当前目录下的内容，不列举子目录
            request.setDelimiter("/");
           // 按设置的对象前缀返回结果
            request.setPrefix(prefix);
            listObjects(request);
        }
    }

    static void listObjects(ListObjectsRequest request) {
        ObjectListing result;
        do {
            result = obsClient.listObjects(request);
            for (ObsObject obsObject : result.getObjects()) {
                // 打印列举的对象名
                System.out.println("\t" + obsObject.getObjectKey());
                // 打印该对象的所有者
                System.out.println("\t" + obsObject.getOwner());
            }
            // 列举对象的起始位置
            request.setMarker(result.getNextMarker());
            // 递归列举文件夹
            listObjectsByPrefix(result);
        } while (result.isTruncated());
    }
}  
```

## 相关链接<a name="section143419113184"></a>

-   关于并行文件系统的更多说明，请参见[什么是并行文件系统](https://support.huaweicloud.com/pfsfg-obs/obs_13_0007.html)。
-   列举并行文件系统内对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   列举并行文件系统内对象常见问题请参见[并行文件系统常见问题](https://support.huaweicloud.com/pfsfg-obs/obs_13_0015.html)。

