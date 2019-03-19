# Header中携带签名<a name="ZH-CN_TOPIC_0100846723"></a>

OBS的所有API接口都可以通过在header中携带签名方式来进行身份认证，也是最常用的身份认证方式。

在Header中携带签名是指将通过HTTP消息中Authorization header头域携带签名信息，消息头域的格式为：

```
Authorization: OBS AccessKeyID:signature
```

签名字符串\(signature\)生成过程如下：

1.  构造请求字符串\(StringToSign\)。

    请求字符串中的参数说明如[表1](#table34479832212511)所示。

    ```
    StringToSign = 
        HTTP-Verb + "\n" + 
        Content-MD5 + "\n" + 
        Content-Type + "\n" + 
        Date + "\n" + 
        CanonicalizedHeaders + CanonicalizedResource
    ```

    **表 1**  构造StringToSign所需参数说明

    <a name="table34479832212511"></a>
    <table><thead align="left"><tr id="row42478738"><th class="cellrowborder" valign="top" width="18%" id="mcps1.2.3.1.1"><p id="p18225769"><a name="p18225769"></a><a name="p18225769"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="82%" id="mcps1.2.3.1.2"><p id="p67001213"><a name="p67001213"></a><a name="p67001213"></a>描述</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row58389173"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p31902586"><a name="p31902586"></a><a name="p31902586"></a>HTTP-Verb</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p33972659"><a name="p33972659"></a><a name="p33972659"></a>指接口操作的方法，对REST接口而言，即为http请求操作的VERB，如："PUT"，"GET"，"DELETE"等字符串。</p>
    </td>
    </tr>
    <tr id="row14909112213405"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p132581298408"><a name="p132581298408"></a><a name="p132581298408"></a>Content-MD5</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p102601629204016"><a name="p102601629204016"></a><a name="p102601629204016"></a>按照RFC 1864标准计算出消息体的MD5摘要字符串，即消息体128-bit MD5值经过base64编码后得到的字符串。</p>
    </td>
    </tr>
    <tr id="row1824493"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p13566274"><a name="p13566274"></a><a name="p13566274"></a>Content-Type</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p25126432"><a name="p25126432"></a><a name="p25126432"></a>内容类型，用于指定 消息类型，例如： text/plain。</p>
    <p id="p24811297"><a name="p24811297"></a><a name="p24811297"></a>当请求中不带该头域时，该参数按照空字符串处理，见<a href="#table14775325212511">表2</a>。</p>
    </td>
    </tr>
    <tr id="row63558046"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p28804613404"><a name="p28804613404"></a><a name="p28804613404"></a>Date</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p10901346204019"><a name="p10901346204019"></a><a name="p10901346204019"></a>生成请求的时间，该时间格式遵循RFC 1123；</p>
    <p id="p792134614016"><a name="p792134614016"></a><a name="p792134614016"></a>当有自定义字段x-obs-date时，该参数按照空字符串处理；见<a href="#table25826370212511">表3</a>。</p>
    <p id="p99420463401"><a name="p99420463401"></a><a name="p99420463401"></a>如果进行临时授权方式操作（如临时授权方式获取对象内容等操作）时，该参数不需要。</p>
    </td>
    </tr>
    <tr id="row42990474"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p59676394"><a name="p59676394"></a><a name="p59676394"></a>CanonicalizedHeaders</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p1949763"><a name="p1949763"></a><a name="p1949763"></a>HTTP请求头字段，以“x-obs-”作为前辍的消息头，如“x-obs-date，x-obs-acl”。</p>
    <a name="ol145715617477"></a><a name="ol145715617477"></a><ol id="ol145715617477"><li>自定义字段中的所有字符要转为小写，需要添加多个字段时，要将所有字段按照字典序进行排序。</li><li>在添加自定义字段时，如果有重名的字段，则需要进行合并。如：x-obs-meta-name:name1和x-obs-meta-name:name2，则需要合并成x-obs-meta-name:name1,name2。</li><li>当自定义字段中，含有非ASCII码或不可识别字符时，需进行Base64编码</li><li>当自定义字段中含有无意义空格或table键时，需要摒弃。例如：x-obs-meta-name: name（name前带有一个无意义空格），需要转换为：x-obs-meta-name:name</li><li>每一个自定义字段最后都需要另起新行，见<a href="#table46456687212511">表4</a></li></ol>
    </td>
    </tr>
    <tr id="row7450793"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.3.1.1 "><p id="p66643399"><a name="p66643399"></a><a name="p66643399"></a>CanonicalizedResource</p>
    </td>
    <td class="cellrowborder" valign="top" width="82%" headers="mcps1.2.3.1.2 "><p id="p29406249"><a name="p29406249"></a><a name="p29406249"></a>表示HTTP请求所指定的OBS资源，构造方式如下：</p>
    <p id="p63329656"><a name="p63329656"></a><a name="p63329656"></a>&lt;桶名+对象名&gt;+[子资源]+[查询字符串]</p>
    <a name="ol135483613475"></a><a name="ol135483613475"></a><ol id="ol135483613475"><li>桶名和对象名，例如：/bucket/object。如果没有对象名，如列举桶，则为"/bucket/"，如桶名也没有，则为“/”。</li><li>如果有子资源，则将子资源添加进来，例如?acl，?logging。子资源包括CDNNotifyConfiguration, acl, encryption, lifecycle, location, logging, metadata, notification, partNumber, policy, uploadId, uploads, versionId, versioning, versions, website, quota, storageClass, storageinfo, delete, restore, tagging, cors, replication。</li><li>如有查询字符串那么将这些查询字符串及其请求值按照字典序从小到大排列。</li></ol>
    </td>
    </tr>
    </tbody>
    </table>

    生成StringToSign的例子如[表2](#table14775325212511)、[表3](#table25826370212511)、[表4](#table46456687212511)和[表5](#table47748300)所示：

    **表 2**  获取对象

    <a name="table14775325212511"></a>
    <table><thead align="left"><tr id="row48189141"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p11006326"><a name="p11006326"></a><a name="p11006326"></a>请求消息头</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p19097245"><a name="p19097245"></a><a name="p19097245"></a>StringToSign</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row3372975"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p4775574"><a name="p4775574"></a><a name="p4775574"></a>GET /object.txt HTTP/1.1</p>
    <p id="p42980173"><a name="p42980173"></a><a name="p42980173"></a>Host: bucket.obs.cn-north-1.myhuaweicloud.com</p>
    <p id="p51277242"><a name="p51277242"></a><a name="p51277242"></a>Date: Sat, 12 Oct 2015 08:12:38 GMT</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p59815938"><a name="p59815938"></a><a name="p59815938"></a>GET \n</p>
    <p id="p164481243202215"><a name="p164481243202215"></a><a name="p164481243202215"></a>\n</p>
    <p id="p1472535"><a name="p1472535"></a><a name="p1472535"></a>\n</p>
    <p id="p13252823"><a name="p13252823"></a><a name="p13252823"></a>Sat, 12 Oct 2015 08:12:38 GMT\n</p>
    <p id="p52166545"><a name="p52166545"></a><a name="p52166545"></a>/bucket/object.txt</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 3**  带自定义字段上传对象1

    <a name="table25826370212511"></a>
    <table><thead align="left"><tr id="row13863750"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p49222002"><a name="p49222002"></a><a name="p49222002"></a>请求消息头</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p27559193"><a name="p27559193"></a><a name="p27559193"></a>StringToSign</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row17702181"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p24590590"><a name="p24590590"></a><a name="p24590590"></a>PUT /object.txt HTTP/1.1</p>
    <p id="p19988723"><a name="p19988723"></a><a name="p19988723"></a>User-Agent: curl/7.15.5</p>
    <p id="p11796122133515"><a name="p11796122133515"></a><a name="p11796122133515"></a>Host: bucket.obs.cn-north-1.myhuaweicloud.com</p>
    <p id="p8473833"><a name="p8473833"></a><a name="p8473833"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT</p>
    <p id="p9155637"><a name="p9155637"></a><a name="p9155637"></a>content-type: text/plain</p>
    <p id="p15291872"><a name="p15291872"></a><a name="p15291872"></a>Content-Length: 5913339</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p30682111"><a name="p30682111"></a><a name="p30682111"></a>PUT\n</p>
    <p id="p7703550"><a name="p7703550"></a><a name="p7703550"></a>\n</p>
    <p id="p2223087"><a name="p2223087"></a><a name="p2223087"></a>text/plain\n</p>
    <p id="p20007789"><a name="p20007789"></a><a name="p20007789"></a>x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\n</p>
    <p id="p45852376"><a name="p45852376"></a><a name="p45852376"></a>/bucket/object.txt</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 4**  带自定义字段上传对象2

    <a name="table46456687212511"></a>
    <table><thead align="left"><tr id="row1033238"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p16583492"><a name="p16583492"></a><a name="p16583492"></a>请求消息头</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p1085622"><a name="p1085622"></a><a name="p1085622"></a>StringToSign</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row20826581"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p9231496"><a name="p9231496"></a><a name="p9231496"></a>PUT /object.txt HTTP/1.1</p>
    <p id="p15974605"><a name="p15974605"></a><a name="p15974605"></a>User-Agent: curl/7.15.5</p>
    <p id="p38071431163517"><a name="p38071431163517"></a><a name="p38071431163517"></a>Host: bucket.obs.cn-north-1.myhuaweicloud.com</p>
    <p id="p18874618"><a name="p18874618"></a><a name="p18874618"></a>Date: Mon, 14 Oct 2015 12:08:34 GMT</p>
    <p id="p35653836"><a name="p35653836"></a><a name="p35653836"></a>x-obs-acl: public-read</p>
    <p id="p52449071"><a name="p52449071"></a><a name="p52449071"></a>content-type: text/plain</p>
    <p id="p2279597"><a name="p2279597"></a><a name="p2279597"></a>Content-Length: 5913339</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p50429634"><a name="p50429634"></a><a name="p50429634"></a>PUT\n</p>
    <p id="p51213523"><a name="p51213523"></a><a name="p51213523"></a>\n</p>
    <p id="p58268531"><a name="p58268531"></a><a name="p58268531"></a>text/plain\n</p>
    <p id="p54654738"><a name="p54654738"></a><a name="p54654738"></a>Mon, 14 Oct 2015 12:08:34 GMT\n</p>
    <p id="p22130602"><a name="p22130602"></a><a name="p22130602"></a>x-obs-acl:public-read\n</p>
    <p id="p64957690"><a name="p64957690"></a><a name="p64957690"></a>/bucket/object.txt</p>
    </td>
    </tr>
    </tbody>
    </table>

    **表 5**  获取对象ACL

    <a name="table47748300"></a>
    <table><thead align="left"><tr id="row66793295"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p41547828"><a name="p41547828"></a><a name="p41547828"></a>请求消息头</p>
    </th>
    <th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p9930893"><a name="p9930893"></a><a name="p9930893"></a>StringToSign</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row66204867"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p60993981"><a name="p60993981"></a><a name="p60993981"></a>GET /object.txt?acl HTTP/1.1</p>
    <p id="p844914343518"><a name="p844914343518"></a><a name="p844914343518"></a>Host: bucket.obs.cn-north-1.myhuaweicloud.com</p>
    <p id="p41565411"><a name="p41565411"></a><a name="p41565411"></a>Date: Sat, 12 Oct 2015 08:12:38 GMT</p>
    </td>
    <td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p11355167"><a name="p11355167"></a><a name="p11355167"></a>GET \n</p>
    <p id="p35087639"><a name="p35087639"></a><a name="p35087639"></a>\n</p>
    <p id="p1478816075319"><a name="p1478816075319"></a><a name="p1478816075319"></a>\n</p>
    <p id="p47353302"><a name="p47353302"></a><a name="p47353302"></a>Sat, 12 Oct 2015 08:12:38 GMT\n</p>
    <p id="p23526540"><a name="p23526540"></a><a name="p23526540"></a>/bucket/object.txt?acl</p>
    </td>
    </tr>
    </tbody>
    </table>

2.  根据请求字符串和用户SK生成signature，生成过程使用HMAC算法\(hash-based authentication code algorithm\)。

    ```
    Signature = Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) )
    ```

    例如在华北区域创建桶名为newbucketname2的私有桶，客户端请求格式为：

    ```
    PUT / HTTP/1.1 
    Host: newbucketname2.obs.cn-north-1.myhuaweicloud.com
    Content-Length: length
    Date: Fri, 06 Jul 2018 03:45:51 GMT
    x-obs-acl:private
    x-obs-storage-class:STANDARD
    Authorization: OBS UDSIAMSTUBTEST000254:ydH8ffpcbS6YpeOMcEZfn0wE90c=
    
    <CreateBucketConfiguration xmlns="http://obs.cn-north-1.myhuaweicloud.com/doc/2015-06-30/"> 
        <Location>cn-north-1</Location>
    </CreateBucketConfiguration>
    ```

    JAVA中，签名的计算方法为：

    ```
    import javax.crypto.Mac;
    import javax.crypto.spec.SecretKeySpec;
    import java.io.UnsupportedEncodingException;
    import java.security.NoSuchAlgorithmException;
    import java.security.InvalidKeyException;
    import java.util.Base64;
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    import java.util.Locale;
    import java.util.TimeZone;
    public class Signature{
    	public static void signWithHmacSha1(String sk, String canonicalString)throws UnsupportedEncodingException{
    	
    		try {
    			SecretKeySpec signingKey = new SecretKeySpec(sk.getBytes("UTF-8"), "HmacSHA1");
    			Mac mac = Mac.getInstance("HmacSHA1");
             		mac.init(signingKey);	
    			System.out.println(Base64.getEncoder().encodeToString(mac.doFinal(canonicalString.getBytes("UTF-8"))));
    		} catch (NoSuchAlgorithmException|InvalidKeyException|UnsupportedEncodingException e) {
    			e.printStackTrace();
    		}
    	}
    	public static void main(String[] str){
                    String yourSecretAccessKeyID = "275hSvB6EEOorBNsMDEfOaICQnilYaPZhXUaSK64";
    		String httpMethod = "PUT";
    		String contentType = "application/xml";
                    // "date" is the time when the request was actually generated
                    Calendar cd = Calendar.getInstance();
                    SimpleDateFormat sdf = new SimpleDateFormat("EEE, d MMM yyyy HH:mm:ss 'GMT'", Locale.US);
                    sdf.setTimeZone(TimeZone.getTimeZone("GMT")); // 设置时区为GMT
                    String date = sdf.format(cd.getTime());
                    String canonicalizedHeaders = "x-obs-acl:private";
    		String CanonicalizedResource = "/newbucketname2";
    	String canonicalString = httpMethod + "\n" + "\n" + contentType + "\n" + date + "\n" + canonicalizedHeaders + CanonicalizedResource;
    		try{
    			signWithHmacSha1(yourSecretAccessKeyID,canonicalString);
    		}catch (UnsupportedEncodingException e){
    			e.printStackTrace();
    		}
    	
    	}
    
    }
    ```

    签名的计算的样例结果为（按照执行时间的不同变化）：ydH8ffpcbS6YpeOMcEZfn0wE90c=


