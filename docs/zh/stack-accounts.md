# 账号密码

使用phpStudy，可能会用到的几组账号密码如下：

## MySQL

  **管理员用户名**：*root*   
  **密码存储路径**：*C:/credentials/password.txt*     
  **获取方式**： 远程桌面到服务器，打开此文件即可   
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/wamp/wamp-pwfolder-websoft9.png)

  **注意**：若服务器上不存在 password.txt 文件，那么数据库密码是 `123456`。此时务必修改为强密码，类似于：f@N7eUUm25xAjP!$ ，这样有助于提高数据库的安全性，减少数据库密码被破解的风险。

 需要登录MySQL，请参考 [MySQL可视化管理](/zh/admin-mysql.md)

## Windows

* 主机地址：服务公网IP地址
* 连接方式：云控制台在线管理 或 远程桌面工具
* 管理员密码：创建服务器的时候自行设置，若不记得密码需要通过云控制台重置。
* 管理员账号：不同的云平台有一定的差异
   |  云平台   |  管理员账号   |
   | --- | --- |
   |  Azure   |  创建服务器的时候自行设置   |
   |  AWS，阿里云，华为云，腾讯云   |  administrator   |