[ubuntu安装地址sql网站](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-linux-2017)



1. 确保数据库在运行：

   ```bash
   systemctl status mssql-server
   ```

   ​

2. 使用sqlcmd链接本地数据库

   ```cmd
   sqlcmd -S localhost -U SA -P 'sql39+39+21' # 字符串是密码

   # If you later decide to connect remotely, specify the machine name or IP address for the -S parameter, and make sure port 1433 is open on your firewall.
   ```

   ​

3. ​




**安装mysql:** 

[下载网址](https://dev.mysql.com/downloads/mysql/),可以下载Ubuntu Linux版的DEB Bundle,解压后有十一个deb文件：

```
*** libmysqlclient21_8.0.11-1ubuntu16.04_amd64.deb
*** libmysqlclient-dev_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-client_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-common_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-community-client_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-community-client-core_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-community-server_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-community-server-core_8.0.11-1ubuntu16.04_amd64.deb
-rw-r--r-- 1 jj jj 28808966 Apr  8 14:07 mysql-community-test_8.0.11-1ubuntu16.04_amd64.deb
*** mysql-server_8.0.11-1ubuntu16.04_amd64.deb
-rw-r--r-- 1 jj jj    75652 Apr  8 14:07 mysql-testsuite_8.0.11-1ubuntu16.04_amd64.deb
```

 逐个安装，注意顺序：

```
1. sudo dpkg -i mysql-common_8.0.11-1ubuntu16.04_amd64.deb
2. sudo dpkg -i libmysqlclient21_8.0.11-1ubuntu16.04_amd64.deb
3. sudo dpkg -i libmysqlclient-dev_8.0.11-1ubuntu16.04_amd64.deb
4. sudo dpkg -i mysql-community-client-core_8.0.11-1ubuntu16.04_amd64.deb
5. sudo dpkg -i mysql-community-client_8.0.11-1ubuntu16.04_amd64.deb
6. sudo dpkg -i mysql-client_8.0.11-1ubuntu16.04_amd64.deb
7. sudo dpkg -i mysql-community-server-core_8.0.11-1ubuntu16.04_amd64.deb
8. sudo dpkg -i mysql-community-server_8.0.11-1ubuntu16.04_amd64.deb
9. sudo dpkg -i mysql-server_8.0.11-1ubuntu16.04_amd64.deb

```



常用命令：

启动mysql服务：`sudo start mysql` 或者 `sudo service mysql start`  # 命令行工具
停止mysql服务：`sudo stop mysql` 或者 `sudo service mysql stop`
重启mysql服务： `sudo restart mysql` 或者 `sudo service mysql restart`

查看mysql数据库的版本号：`mysql -V`

启动mysqld服务: `sudo /etc/init.d/mysql start`　　＃　mysql服务器
停止mysqld服务: `sudo /etc/init.d/mysql stop`
启动mysqld服务: `sudo /etc/init.d/mysql restart`








