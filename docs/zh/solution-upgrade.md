# 更新升级

网站技术日新月异，**更新升级**是维护工作之一，长时间不升级的程序，就如长时间不维护的建筑物一样，会加速老化、功能逐渐缺失直至无法使用。  

这里注意更新与升级这两词的差异（[延伸阅读](https://support.websoft9.com/docs/faq/zh/tech-upgrade.html#更新-vs-升级)），例如：
- 操作系统打个补丁常称之为**更新**，Ubuntu16.04 变更为 Ubuntu18.04，称之为**升级**
- MySQL5.6.25-->MySQL5.6.30 常称之为**更新**，MySQL5.6->MySQL5.7 称之为**升级**

phpStudy 完整的更新升级包括：操作系统更新、PHP 更新、Apache 更新、MySQL 更新

## Windows 更新

Windows服务器的更新与本地电脑类似，手动找到更新管理程序，设置自动下载自动更新即可。

## PHP 更新

以从 PHP7.0.29 升级到 PHP7.0.31 为例：

1. 左击右下角任务栏的 phpStudy 图标，停止所有服务

2. 到 [PHP 官网](https://windows.php.net/download/)下载最新版本的 PHP7.0 
   > 注意：下载的文件为压缩包文件，且必须选择 **Thread Safe** 版本。
   	![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wampserver-phpupdate-1-websoft9.png)

3. 备份原来的 C:\websoft9\wampstack\php 文件夹，再将该文件夹下所有文件删除，将新版 PHP 文件解压到这个文件夹里

4. 将新版 php 文件夹下的 php.ini-production 文件重命名为 php.ini

5. 重新服务


## Apache 更新

待续...

## MySQL 更新
待续...

## 常见问题

#### 是否支持 MySQL 大版本升级，例如：MySQL5.6-> MySQL5.7？
不支持，仅支持小版本升级。例如：5.6.x to 5.6.y 或 5.7.x to 5.7.y

#### 是否支持 PHP 大版本升级，例如：PHP7.0-> PHP7.2？
官方没有提供升级文档

#### 是否支持 PHP 大版本降级，例如：PHP7.2-> PHP7.0？
不支持

#### 升级之前需要做什么准备工作？
做好快照备份