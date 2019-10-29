# 迁移网站

迁移网站就是将**网站数据**移动到新的位置，然后通过配置，保证移动后可正常访问。

迁移是需要谨慎对待的操作，迁移之前需要清楚的明白如下要点：

- 被移动的网站数据对象：网站源码文件和数据库数据文件  
- 目的地位置：服务器目录之间转移（本地）和转移到外部服务器（外部）

被迁移对象和目的地位置的组合，形成了多种多样的迁移场景。下面详细说明最常见的迁移场景：

## 迁移网站源码（本地）

以将原目录 *c:\wwwroot* 下的 **mysite1** 迁移到 *d:\www* 目录下为例，具体步骤如下：

1. 使用 **远程桌面** 连接服务器，停止 [Apache 服务](/zh/admin-services.md#apache)
2. 将 ***mysite1*** 文件夹整体拷贝到目标位置 *d:\www*
3. 修改 [虚拟主机配置文件](/zh/stack-components.html#apache) 中 mysite1 这个网站对应的 VirtualHost 配置段 DocumentRoot, Directory 项的值，并保存它

   原地址：c:\wwwroot\mysite1  
   目标地址：d:\www\mysite1

4. 重启 [Apache 服务](/zh/admin-services.md#apache)
5. 测试迁移后的结果，成功后可以删除原来的 *mysite1* 文件夹

## 迁移数据库文件（本地）

没有特殊情况，我们不建议迁移数据库文件到服务器上另外一个目录，毕竟主流的云厂商磁盘均可扩容。

1. 停止 MySQL 服务
2. 将 *C:/websoft9/wampstack/mysql/data* 下所有文件拷贝到新目录，例如：D:\data
3. 修改 [数据库配置文件](/zh/stack-components.md#mysql) 文件中数据存放的路径，范例参考：
	~~~
    datadir="C:/websoft9/wampstack/mysql/data"
    log-error="C:/websoft9/wampstack/mysql/data/mysqld.log"
        
    修改为：
    
    datadir="D:\data"
    log-error="D:\data\mysqld.log"
    ~~~
 4. 重启 MySQL 服务

## 迁移到外部服务器

网站从一台服务器（原服务器）迁移到另外一台服务器（目的服务器）是一个系统工程，基本步骤如下：

1. 通过云控制台，在目的服务器上[部署](/zh/stack-deployment.md)参数一致的 phpStudy 镜像。
2. 将原服务器上的网站源文件**转移到**目的服务器。
3. 通过 phpMyAdmin **导出**原服务器上的数据库，然后在目的服务器上**导入**数据库。
4. 把原服务器上的 [虚拟主机配置文件](/zh/stack-components.html#apache) 配置文件内容，完整拷贝到目的服务器的 [虚拟主机配置文件](/zh/stack-components.html#apache) 中，保存之。
5. 重启 Apache 服务。
5. 解析域名到目的服务器，等待域名解析生效。
5. 通过域名访问网站，测试可用性。
6. 正式发布。

如果一台服务器上有多个网站需要迁移，建议逐个迁移