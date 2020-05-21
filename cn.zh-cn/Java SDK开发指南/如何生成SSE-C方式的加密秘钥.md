# 如何生成SSE-C方式的加密秘钥<a name="obs_21_2119"></a>

以下代码展示了如何生成SSE-C方式的加密秘钥，以及秘钥的MD5值如何生成：

```
import java.nio.charset.Charset;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class SseCTool {
    public static void main(String[] args) {
        // 加密秘钥示例：长度32的字符串，用于生成256 bit的密钥；该秘钥可根据业务需要自行修改，但长度必须为32个字符，及256 bit的字符串
        String keyString = "12345678901234567890123456789012";

        // 计算x-obs-server-side-encryption-customer-key头域
        String customerKey = toBase64String(keyString.getBytes(Charset.forName("UTF-8")));
        System.out.println("customer key is : " + customerKey);

        // 计算x-obs-server-side-encryption-customer-key-MD5头域
        String customerKeyMD5 = computeMD5(fromBase64(customerKey));
        System.out.println("md5 for customer key is : " + customerKeyMD5);
    }

    // 计算Base64字符串
    public static String toBase64String(byte[] data) {
        java.util.Base64.Encoder encoder = java.util.Base64.getEncoder();
        return new String(encoder.encode(data), Charset.forName("UTF-8"));
    }

    // 计算MD5字符串
    public static String computeMD5(byte[] b64Data) {
        try {
            MessageDigest md5 = MessageDigest.getInstance("MD5");
            md5.update(b64Data);

            byte[] byteArray = md5.digest();

            return toBase64String(byteArray);
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
            return "";
        }

    }

    public static byte[] fromBase64(String b64Data) {
        java.util.Base64.Decoder decoder = java.util.Base64.getDecoder();
        return decoder.decode(b64Data.getBytes(Charset.forName("UTF-8")));
    }
}
```

