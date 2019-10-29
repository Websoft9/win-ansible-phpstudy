# SSL/HTTPS

网站完成域名绑定且可以通过HTTP访问之后，方可设置HTTPS。

phpStudy预装包，已安装Web服务器 OpenSSL 模块，并完成预配置。

> 除了虚拟主机配置文件之外，HTTPS设置无需修改 Apache 任何文件

## 设置参考

如果你已经申请了商业证书，只需几步，即可完成HTTPS配置

1. 将申请的证书、秘钥文件上传到 *C:\wwwroot\cert* 目录

2. 打开 [bitnami-apps-vhosts.conf（虚拟主机配置配置文件）](/zh/stack-components.md#apache) 
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-addmorevhostconfig-websoft9.png)

3. 将下面的 HTTPS 配置文件模板（<VirtualHost *:443>...</VirtualHost>），增加到 httpd-vhosts.conf 文件中(不能删除原有内容)

    ```
    <VirtualHost *:443>
    ServerName  www.mydomain.com
    DocumentRoot "C:\wwwroot\mysite2"
    <Directory "C:\wwwroot\mysite2">
    Options Indexes FollowSymlinks
    AllowOverride All
    Require all granted
    </Directory>
    SSLEngine on
    SSLCertificateFile  "C:\wwwroot\cert\cert.pem"
    SSLCertificateKeyFile  "C:\wwwroot\cert\key.pem"
    SSLCertificateChainFile  "C:\wwwroot\cert\chain.pem"
    </VirtualHost>
    ```

7. 修改其中的 ServerName, DocumentRoot, ErrorLog, CusomLog, Directory等项的值（[修改参考](/zh/solution-deployment.html#virtualhost)），修改完成后保存

8. 重启 Apache 服务 
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-bitnami001-websoft9.png)

## 更多指南

若参考上面的**设置参考**仍无法成功设置HTTPS访问，请阅读由Websoft9提供的 [《HTTPS 专题指南》](https://support.websoft9.com/docs/faq/zh/tech-https.html#apache)

HTTPS专题指南方案包括：HTTPS前置条件、HTTPS 配置段模板、注意事项、详细步骤以及故障诊断等具体方案。