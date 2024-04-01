# 客户端加密接口\(Java SDK\)<a name="obs_21_2303"></a>

## 初始化CryptoCipher<a name="section61436018442"></a>

OBS Java SDK提供两种加密套件。您可根据使用场景自行选择。

[CtrRSACipherGenerator](#table38241617131212)继承于[CTRCipherGenerator](#table58575812)，不需要提供数据密钥或初始值，只需要提供RSA公钥或RSA私钥，用以加密和解密随机生成的数据密钥。

[CTRCipherGenerator](#table58575812)仅需提供一个数据密钥，所有对象均使用该数据密钥进行加密。

**表 1**  CtrRSACipherGenerator类型参数

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|privateKey|PrivateKey|解密文件时必选（例如getObject）|**参数解释：**RSA私钥。**默认取值：**无|
|publicKey|PublicKey|加密文件时必选（例如putObject）|**参数解释：**RSA公钥。**默认取值：**无|
|masterKeyInfo|String|可选|**参数解释：**密钥信息，该信息会存至对象的自定义元数据中， 帮助您区分不同密钥，需您自行维护 masterKeyInfo与 密钥的映射关系。**默认取值：**无|
|secureRandom|SecureRandom|必选|**参数解释：**安全随机数生成器，用于随机生成cryptoKeyBytes和cryptoIvBytes，请您根据业务需求选择设置。**默认取值：**无|
|needSha256|boolean|可选|**参数解释：**是否校验加密后数据的sha256，并设置加密前后的sha256作为自定义元数据。为了节省内存开销，SDK 采用了流式计算的方法，这也就意味着，普通上传时需要读取并加密文件两次；在另外由于断点续传上传接口为分段上传接口的封装，在断点续传下，则需要读取并加密文件三次。**取值范围：**true：设置need_sha256为true时，SDK会自动计算待上传对象的加密前sha256值与加密后的sha256值，并存至对象自定义元数据，同时也会在发送请求时将加密后的文件的sha256值置于请求头，服务端收到请求后会计算收到对象的sha256，如果sha256不一致会返回错误信息。false：不计算校验加密后数据的sha256。**默认取值：**false|


**表 2**  CTRCipherGenerator类型参数

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|masterKeyInfo|String|可选|**参数解释：**密钥信息，该信息会存至对象的自定义元数据中，帮助您区分不同cryptoKeyBytes，需您自行维护 masterKeyInfo与 cryptoKeyBytes的映射关系。**默认取值：**无|
|cryptoKeyBytes|byte[]|必选|**参数解释：**加密数据所使用的数据密钥。**约束限制：**长度必须为32 bytes。**默认取值：**无|
|cryptoIvBytes|byte[]|可选|**参数解释：**加密数据时所使用的初始值。**约束限制：**长度必须为16 bytes。指定时，所有对象均使用该初始值加密；未指定时，SDK会为每个对象随机生成不同初始值。**默认取值：**无|
|secureRandom|SecureRandom|必选|**参数解释：**安全随机数生成器，用于在未设置cryptoKeyBytes或cryptoIvBytes时随机生成缺失的对应参数，请您根据业务需求设置。**默认取值：**无|
|needSha256|boolean|可选|**参数解释：**是否校验加密后数据的sha256，并设置加密前后的sha256作为自定义元数据。为了节省内存开销，SDK 采用了流式计算的方法，这也就意味着，普通上传时需要读取并加密文件两次；在另外由于断点续传上传接口为分段上传接口的封装，在断点续传下，则需要读取并加密文件三次。**取值范围：**true：设置need_sha256为true时，SDK会自动计算待上传对象的加密前sha256值与加密后的sha256值，并存至对象自定义元数据，同时也会在发送请求时将加密后的文件的sha256值置于请求头，服务端收到请求后会计算收到对象的sha256，如果sha256不一致会返回错误信息。false：不计算校验加密后数据的sha256。**默认取值：**false|


## 初始化CryptoObsClient<a name="section821514563446"></a>

初始化[CryptoObsClient](#table10831182114445)继承自普通ObsClient，详细配置可参考[创建并配置客户端\(Java SDK\)](创建并配置客户端(Java-SDK).md)。

**方法定义**

CryptoObsClient\(String accessKey, String secretKey, String endPoint, CTRCipherGenerator ctrCipherGenerator\)

**表 3**  CryptoObsClient初始化参数

|**参数名称**|**描述**|**建议值**|
|--|--|--|
|accessKey|**参数解释：**访问密钥中的AK。**默认取值：**空字符串，表示匿名用户|N/A|
|secretKey|**参数解释：**访问密钥中的SK。**默认取值：**空字符串，表示匿名用户|N/A|
|endPoint|**参数解释：**连接OBS的服务地址。可包含协议类型、域名、端口号。示例：https://your-endpoint:443。（出于安全性考虑，建议使用https协议）。**默认取值：**无|N/A|
|ctrCipherGenerator|**参数解释：**该加密客户端所使用的 加密套件。**取值范围：**CtrRSACipherGeneratorCTRCipherGenerator**默认取值：**无|N/A|


## 支持加密的接口<a name="section753815711219"></a>

**表 4**  目前支持加密的接口列表

|**方法名称**|**说明**|
|--|--|
|putObject|上传对象|
|getObject|下载对象|


## 示例代码<a name="section1680016487146"></a>

这是CtrRSACipherGenerator的示例代码：

```
import com.obs.services.ObsConfiguration;
import com.obs.services.crypto.CTRCipherGenerator;
import com.obs.services.crypto.CryptoObsClient;
import com.obs.services.crypto.CtrRSACipherGenerator;
import com.obs.services.exception.ObsException;
import com.obs.services.model.GetObjectRequest;
import com.obs.services.model.ObsObject;
import com.obs.services.model.PutObjectResult;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.security.NoSuchAlgorithmException;
import java.security.PrivateKey;
import java.security.PublicKey;
import java.security.spec.InvalidKeySpecException;

public class CtrRSACipherGeneratorDemo001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        // String securityToken = System.getenv("SECURITY_TOKEN");
        // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
        String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
        // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
        //String endPoint = System.getenv("ENDPOINT");
        CtrRSACipherGenerator ctrRSACipherGenerator = null;
        try {
            String examplePrivateKeyPath = "yourRSAPrivateKeyPath";
            String examplePublicKeyPath = "yourRSAPublicKeyPath";
            ObsConfiguration config = new ObsConfiguration();
            PrivateKey privateKeyObj = CtrRSACipherGenerator.importPKCS8PrivateKey(examplePrivateKeyPath);
            PublicKey publicKeyObj = CtrRSACipherGenerator.importPublicKey(examplePublicKeyPath);
            ctrRSACipherGenerator =
                    new CtrRSACipherGenerator(
                            "example_master_key_info", true, config.getSecureRandom(), privateKeyObj, publicKeyObj);

        } catch (IllegalArgumentException | IOException | NoSuchAlgorithmException | InvalidKeySpecException e) {
            e.printStackTrace();
        }
        assert ctrRSACipherGenerator != null;
        // 创建ObsClient实例
        try (CryptoObsClient cryptoObsClient = new CryptoObsClient(ak, sk, securityToken, endPoint, ctrRSACipherGenerator)) {
            String exampleBucketName = "example-bucket";
            String exampleObjectKey = "exampleObjectKey";
            String examplePlainTextFilePath = "examplePlainTextFilePath";
            String exampleDecryptedFilePath = "exampleDecryptedFilePath";
            PutObjectResult putObjectResult =
                    cryptoObsClient.putObject(exampleBucketName, exampleObjectKey, new File(examplePlainTextFilePath));
            System.out.println("HTTP Code: " + putObjectResult.getStatusCode());
            System.out.println("Etag: " + putObjectResult.getEtag());
            // 客户端加密上传成功
            System.out.println("CtrRSACipherGeneratorDemo001 putObject successfully");

            GetObjectRequest getObjectRequest = new GetObjectRequest(exampleBucketName, exampleObjectKey);
            ObsObject obsObject = cryptoObsClient.getObject(getObjectRequest);
            InputStream input = obsObject.getObjectContent();
            byte[] b = new byte[1024];
            FileOutputStream fileOutputStream = new FileOutputStream(exampleDecryptedFilePath);
            int len;
            while ((len = input.read(b)) != -1) {
                fileOutputStream.write(b, 0, len);
            }
            fileOutputStream.close();
            input.close();

            System.out.println("HTTP Code: " + obsObject.getMetadata().getStatusCode());
            // 客户端解密下载成功
            System.out.println("CtrRSACipherGeneratorDemo001 getObject successfully");

            // 验证加密之前的文件和解密之后的文件是否一致
            byte[] plainTextFileSha256 = CTRCipherGenerator.getFileSha256Bytes(examplePlainTextFilePath);
            byte[] decryptedFileSha256 = CTRCipherGenerator.getFileSha256Bytes(exampleDecryptedFilePath);
            String plainTextFileSha256Base64Encoded = CTRCipherGenerator.getBase64Info(plainTextFileSha256);
            String decryptedFileSha256Base64Encoded = CTRCipherGenerator.getBase64Info(decryptedFileSha256);
            System.out.println("plainTextFileSha256 base64 encoded: " + plainTextFileSha256Base64Encoded);
            System.out.println("decryptedFileSha256 base64 encoded: " + decryptedFileSha256Base64Encoded);
            System.out.println(
                    "plainTextFileSha256 equals decryptedFileSha256 ? "
                            + decryptedFileSha256Base64Encoded.equals(plainTextFileSha256Base64Encoded));
            System.out.println("CtrRSACipherGeneratorDemo001 successfully");
        } catch (ObsException e) {
            System.out.println("CtrRSACipherGeneratorDemo001 failed");
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
            System.out.println("CtrRSACipherGeneratorDemo001 putObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}


```

这是CTRCipherGenerator的示例代码：

```
import com.obs.services.crypto.CTRCipherGenerator;
import com.obs.services.crypto.CryptoObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.GetObjectRequest;
import com.obs.services.model.ObsObject;
import com.obs.services.model.PutObjectResult;

import java.io.File;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.security.NoSuchAlgorithmException;
import java.security.SecureRandom;

public class CTRCipherGeneratorDemo001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        // String securityToken = System.getenv("SECURITY_TOKEN");
        // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
        String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
        // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
        //String endPoint = System.getenv("ENDPOINT");
          CTRCipherGenerator ctrCipherGenerator = null;
        try {
            SecureRandom secureRandom = SecureRandom.getInstanceStrong();
            // 注意 Linux 下SecureRandom.getInstanceStrong()在熵不够的情况下可能阻塞，建议同时增加相关的补熵机制，或者以其他方式设置SecureRandom
            byte[] exampleMasterKey = new byte[CTRCipherGenerator.CRYPTO_KEY_BYTES_LEN];
            secureRandom.nextBytes(exampleMasterKey);
            // 这里的exampleMasterKey用随机生成的主密钥演示，使用时请您保证密钥长度为32,并妥善保管密钥。
            ctrCipherGenerator =
                    new CTRCipherGenerator("example_master_key_info", exampleMasterKey, true, secureRandom);
        } catch (IllegalArgumentException | NoSuchAlgorithmException e) {
            e.printStackTrace();
        }
        assert ctrCipherGenerator != null;
        // 创建ObsClient实例
        try (CryptoObsClient cryptoObsClient =
                new CryptoObsClient(ak, sk, securityToken, endPoint, ctrCipherGenerator)) {
            String exampleBucketName = "example-bucket";
            String exampleObjectKey = "exampleObjectKey";
            String examplePlainTextFilePath = "examplePlainTextFilePath";
            String exampleDecryptedFilePath = "exampleDecryptedFilePath";
            PutObjectResult putObjectResult =
                    cryptoObsClient.putObject(exampleBucketName, exampleObjectKey, new File(examplePlainTextFilePath));
            System.out.println("HTTP Code: " + putObjectResult.getStatusCode());
            System.out.println("Etag: " + putObjectResult.getEtag());
            // 客户端加密上传成功
            System.out.println("CTRCipherGeneratorDemo001 putObject successfully");

            GetObjectRequest getObjectRequest = new GetObjectRequest(exampleBucketName, exampleObjectKey);
            ObsObject obsObject = cryptoObsClient.getObject(getObjectRequest);
            InputStream input = obsObject.getObjectContent();
            byte[] b = new byte[1024];
            FileOutputStream fileOutputStream = new FileOutputStream(exampleDecryptedFilePath);
            int len;
            while ((len = input.read(b)) != -1) {
                fileOutputStream.write(b, 0, len);
            }
            fileOutputStream.close();
            input.close();

            System.out.println("HTTP Code: " + obsObject.getMetadata().getStatusCode());
            // 客户端解密下载成功
            System.out.println("CTRCipherGeneratorDemo001 getObject successfully");
            
            // 验证加密之前的文件和解密之后的文件是否一致
            byte[] plainTextFileSha256 = CTRCipherGenerator.getFileSha256Bytes(examplePlainTextFilePath);
            byte[] decryptedFileSha256 = CTRCipherGenerator.getFileSha256Bytes(exampleDecryptedFilePath);
            String plainTextFileSha256Base64Encoded = CTRCipherGenerator.getBase64Info(plainTextFileSha256);
            String decryptedFileSha256Base64Encoded = CTRCipherGenerator.getBase64Info(decryptedFileSha256);
            System.out.println("plainTextFileSha256 base64 encoded: " + plainTextFileSha256Base64Encoded);
            System.out.println("decryptedFileSha256 base64 encoded: " + decryptedFileSha256Base64Encoded);
            System.out.println(
                    "plainTextFileSha256 equals decryptedFileSha256 ? "
                            + decryptedFileSha256Base64Encoded.equals(plainTextFileSha256Base64Encoded));
            System.out.println("CTRCipherGeneratorDemo001 successfully");
        } catch (ObsException e) {
            System.out.println("CTRCipherGeneratorDemo001 failed");
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
            System.out.println("CTRCipherGeneratorDemo001 putObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

