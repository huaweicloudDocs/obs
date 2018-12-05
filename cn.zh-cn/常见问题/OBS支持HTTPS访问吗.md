# OBS支持HTTPS访问吗？<a name="obs_03_0071"></a>

OBS支持HTTPS访问。

-   使用OBS分配的域名进行访问时，只要在浏览器中将桶或对象的URL的http:// 替换成https:// 即可。
-   OBS使用自定义域名绑定功能，未启用CDN加速时，由于OBS自定义域名绑定不支持HTTPS访问自定义域名，只支持HTTP方式访问自定义域名，客户自定义域名绑定成功后，若想使用https方式进行访问，需先在浏览器上导入SSL证书，再使用HTTPS方式访问。
-   配合CDN同时使用时，通过CDN管理控制台进行HTTPS证书管理，即可使用HTTPS访问。CDN管理控制台HTTPS证书管理方式，详见[配置HTTPS安全加速](https://support.huaweicloud.com/usermanual-cdn/zh-cn_topic_0064907771.html)。

