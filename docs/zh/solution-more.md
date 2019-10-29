# 更多...

下面每一个方案，都经过实践证明行之有效，希望能够对你有帮助

## 域名绑定

当服务器上只有一个网站时，不做域名绑定也可以访问网站。但从安全和维护考量，**域名绑定**不可省却。

以示例网站为例，域名绑定操作步骤如下：

1. 确保域名解析已经生效  
2. 使用 **远程桌面工具** 登录云服务器
2. 修改 [Apache虚拟机主机配置文件](/zh/stack-components.md#apache)，将其中的 **ServerName** 项的值修改为你的域名
   ```text
   <VirtualHost *:80>
   ServerName www.mydomain.com # 此处修改为你的域名
   DocumentRoot "C:\wwwroot\mysite2"
   ...
   ```
3. 保存配置文件，重启 [Apache 服务](/zh/admin-services.md)


## 使用 Apache 伪静态

使用 Apache 伪静态有三个步骤：

1.  打开 [Apache 主配置文件](/zh/stack-components.md#apache)，检查 Rewrite 模块是否启用（phpStudy 环境默认已经开启 Rewirte）
```
 LoadModule rewrite_module modules/mod_rewrite.so #若前面有"#"号则需要将其去掉，使之支持 mod_rewrite 模块；
```
2.  保证 [Apache 虚拟主机配置文件](/zh/stack-components.md#apache)中 VirtualHost 配置段中增加 AllowOverride All
3.  给需要使用伪静态的网站的根目录中增加 `.htaccess` 文件，并在其中配置伪静态规则

## 重置 MySQL 密码

重置 MySQL 密码的原理主要分为三个部分

1. 将 MySQL 更改为临时免密模式
2. 修改密码
3. 将 MySQL 恢复为正常模式

### 将 MySQL 更改为临时免密模式

1. 远程连接到服务器，打开 [MySQL 配置文件](/zh/stack-components.html#mysql)，在 [mysqld] 配置项中增加一行 `skip-grant-tables`，保存
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-addconfigtomysqld-websoft9.png)

2. 重启 MySQL 服务
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-managerservice-websoft9.png)

### 修改密码 

- 进入到 MySQL 下的 bin 目录，按住键盘 `Shift`键的同时点击鼠标右键，
  ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-opencmdinbin-websoft9.png)

- 进入命令窗口，依次运行下列命令：
   ```
    mysql -uroot
    use mysql;
    update user set authentication_string=password("12345678") where user="root";
    flush privileges;
    exit
   ```

### 将 MySQL 恢复为正常模式

1. 打开 [MySQL 配置文件](/zh/stack-components.html#mysql)，在 [mysqld] 配置项中删除 `skip-grant-tables` 这一行
2. 再次重启 MySQL 服务，此时密码已被重置为 `12345678`

## 修改 PHP 配置文件（php.ini）

在使用PHP网站的时候，你可能会碰到需要修改：上传文件大小、内存限制等参数。这个时候，就需要通过修改 `php.ini` 来实现

1. 远程桌面登录到服务器，打开 [`php.ini`](/zh/stack-components.html#php) 文件 
```
# File upload limit
post_max_size = 16M
upload_max_filesize = 16M

# Max Execution Time
max_execution_time = 90

# Memory Limit
memory_limit – Minimum: 256M
```
2. 修改所需的参数，保存并重启 [Apache 服务](/zh/admin-services.md)


## PHP 扩展

在 phpStudy 上安装和管理 PHP 扩展的通用步骤如下：

1. 下载正确的 PHP 扩展文件（[注意事项](https://www.php.net/manual/zh/install.pecl.windows.php)），上传到服务器的 [PHP 扩展目录](/zh/stack-components.md#php)

2. 通过修改 PHP 配置文件设置，开启或关闭扩展
   ```
   extension=php_bz2.dll
   ;extension=php_com_dotnet.dll
   ```

不同的 PHP 扩展安装有一定的差异，具体以扩展提供的文档为准

## 安装 Composer

phpStudy 镜像中安装 composer 的方法步骤如下：

1. 进入到 PHP 目录，按住 shift + 鼠标右键，选择“在此处打开命令行窗口”；
2. 输入 php -r "readfile('https://getcomposer.org/installer');" | php 安装 composer；
3. 在该目录下新建 composer.bat 文件，并编辑输入：```@php "%~dp0composer.phar" %*```；
4. 将 PHP 所在目录路径添加到环境变量中，添加方法参考：[Windows系统如何设置添加环境变量？](https://support.websoft9.com/docs/windows/solution-environmentvar.html)
5. 至此，composer 安装完毕。

## 修改网站根目录

将网站根目录设置到D盘或不喜欢现在根目录的位置，就需要修改网站默认根目录。  

phpStudy 环境的根目录是可以被修改的，具体只需2个步骤：

1. 修改[虚拟主机配置文件](/zh/stack-components.html#apache)，将网站对应的`<VirtualHost *:80>...</VirtualHost>` 中 DocumentRoot 和 Directory 的值修改成你网站的路径
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-mddfvhost-websoft9.png)
   
2. 保存后，重启 Apache 服务 