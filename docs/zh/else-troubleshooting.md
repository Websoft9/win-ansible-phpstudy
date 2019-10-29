# 故障处理

此处收集使用 phpStudy 过程中最常见的故障，供您参考

> 大部分故障与云平台密切相关，如果你可以确认故障的原因是云平台造成的，请参考[云平台文档](https://support.websoft9.com/docs/faq/zh/tech-instance.html)

#### 网站重定向错误？

网站重定向错误比较常见。  

处理办法：分析网站根目录下的 `.htaccess` 文件，看看有没有死循环规则

#### 新增站点报错：You don't have permission to access/on this server

解决办法：

1.  检查网站目录的权限
2.  配置虚拟主机配置文件是否有 "AllowOverride All   Require all granted" 相关内容

#### 如何解决 http-proxy 漏洞？
升级 PHP 的小版本即可解决 ttp-proxy 漏洞

#### Apache httpd 服务无法启动？

请通过分析日志文件定位原因

#### 数据库服务无法启动

数据库服务无法启动最常见的问题包括：磁盘空间不足，内存不足，配置文件错误。  
建议先通过命令进行排查  

```shell
# 查看磁盘空间
df -lh

# 查看内存使用
free -lh
```

#### 数据库日志文件太大，导致磁盘空间不足？

默认安装，mysql会自动开启binlog，binlog是一个二进制格式的文件，用于记录用户对数据库**更新的****SQL语句****信息**，例如更改数据库表和更改内容的SQL语句都会记录到binlog里。

binlog主要用于出现没有备份的情况下，恢复数据库。但binlog会占用较大空间，长期不清理会让剩余磁盘空间为0，从而影响数据库或服务器无法启动

如果对自己的备份有信心，不需要binlog功能，参考如下步骤关闭之：

1. 编辑 [MySQL 配置文件](/zh/stack-components.md#mysql)，注释掉 binlog 日志
  ~~~
  #log-bin=mysql-bin  
  ~~~
2. 重启 MySQL 服务

#### 如何根据 Windows 系统日志查看故障原因？

按照下列图中所示，进入到 Windows 系统的**事件查看器**，选择 Windows 日志下的应用程序，然后在右侧的事件列表查看出现错误的应用程序，单击即可在下方弹出详细的错误信息，最后就可以根据错误原因来纠正错误。

![event](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wampserver/wampserver-eventerror-websoft9-1.png)
![event](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wampserver/wampserver-eventerror-websoft9-2.png)

#### 如何解决端口冲突？

默认下，Apache默认端口为80，MySQL默认端口为3306；可以通过cmd控制台输入指令：netstat -ano，查看服务器端口的使用情况。  

如果发送端口冲突故障，具体解决方法如下：

1. 找到 Apache 的配置文件（包括 httpd.conf 和站点配置文件），将端口 80 改为其他端口，如：81，然后重启 Apache。
**注意：更改端口后，需要将安全组的对应端口开放出来，否则服务正常启动，但外网依然无法访问网站。**
2. 找到 MySQL 的配置文件 my.ini ，将其中的 port = 3306 改为其他端口，然后重启MySQL服务。
3. 通过 netstat -ano 命令查看是哪个程序或服务占用了 80 或 3306 端口，可根据 PID 到任务管理器或服务列表将其关闭，再重新启动 Apache 和 MySQL。