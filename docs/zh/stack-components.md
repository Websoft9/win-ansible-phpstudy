# 参数

phpStudy 预装包包含 phpStudy 运行所需一序列支撑软件（简称为“组件”），下面列出主要组件名称、安装路径、配置文件地址、端口、版本等重要的信息。

## 路径

### 网站目录

根目录： *phpStudy 环境中，你的网站代码存放位置是没有限制的，因此没有根目录的说法*  
网站存放目录（建议）： * C:\wwwroot*  
示例网站目录： * C:\wwwroot\www.example.com*  

> 通过 *http://公网IP地址* 访问的就是示例网站 

### Apache

**Apache 虚拟主机配置文件**： *C:\websoft9\wampstack\apache2\conf\bitnami\bitnami-apps-vhosts.conf*  
![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-openvhostconf-websoft9.png)

Apache 主配置文件： *C:\websoft9\wampstack\apache2\conf\httpd.conf*   
Apache 日志文件： *C:\websoft9\wampstack\apache2\logs*  
Apache 模块目录： *C:\websoft9\wampstack\apache2\modules*  

**Apache 虚拟主机配置文件** 默认存在一个 [VirtualHost（虚拟主机）](https://support.websoft9.com/docs/windows/zh/webs-apache.html#虚拟主机) 配置项，对应的就是 **示例网站**
```
<VirtualHost *:80>
    ServerName www.example.com
    ServerAlias example.com
    DocumentRoot "C:\wwwroot\www.example.com"
    ErrorLog "logs\www.example.com-error.log"
    CustomLog "logs\www.example.com-access.log" common

    <Directory "C:\wwwroot\www.example.com">
        Options Indexes FollowSymlinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

> 有多少个网站，就需要在 **虚拟主机配置文件** 中增加同等数量的 **VirtualHost** 配置项，所以说虚拟主机配置文件是这个部署包的核心要点。

### PHP

PHP 配置文件： *C:\websoft9\wampstack\php\php.ini*  
PHP 扩展目录： *C:\websoft9\wampstack\php\ext*   

PHP 扩展启用或关闭，通过修改 PHP 配置文件实现

### MySQL

MySQL 安装路径：*C:\websoft9\wampstack\mysql\*  
MySQL 数据文件：*C:\websoft9\wampstack\mysql\data\mysql*  
MySQL 配置文件：*C:\websoft9\wampstack\mysql\my.ini*    
MySQL 可视化管理地址: *http://服务器公网IP/phpmyadmin*，用户名和密码请见 [账号密码](/zh/stack-accounts.md) 章节。

### phpMyAdmin

phpMyAdmin 安装路径: *C:\websoft9\wampstack\apps\phpmyadmin*  
phpMyAdmin 配置文件: *C:\websoft9\wampstack\apps\phpmyadmin\htdocs\config.inc.php*   
phpMyAdmin 虚拟主机配置文件: *C:\websoft9\wampstack\apps\phpmyadmin\conf\httpd-vhosts.conf*   

## 端口号

在云服务器中，通过 **[安全组设置](https://support.websoft9.com/docs/faq/zh/tech-instance.html)** 来控制（开启或关闭）端口是否可以被外部访问。 

本环境建议开启的端口如下：

| 名称 | 端口号 | 用途 |  必要性 |
| --- | --- | --- | --- |
| HTTP | 80 | 通过 HTTP 访问网站 | 必须 |
| HTTPS | 443 | 通过 HTTP 访问网站 | 可选 |
| MySQL | 3306 | 本地电脑远程连接服务器上的 MySQL | 可选 |

## 版本号

组件版本号可以通过云市场商品页面查看，更精准的版本号请通过下面的方式获取：

- 在服务器 *\websoft9\wampstack\README.txt* 文件中查看  
- 或通过：*http://服务器公网IP/9panel/tz.php* 查看组件的版本