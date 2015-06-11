# Mysql 导入大 SQL 文件的设置

在往 Mysql 数据库导入非常大的 `.sql` 文件的时候经常会遇到两个错误: `MySql server has gone away` 和 `Server dropped an incorrect or too large packet.`

更改两处 Mysql 的配置即可顺利完成导入:


> ####Server timed out and closed the connection. 
> How to fix:
> 
> check that wait_timeout variable in your mysqld’s my.cnf configuration file is large enough. 
  
> On Debian: `sudo vim 
>  /etc/mysql/my.cnf`, set `wait_timeout = 600` seconds (you can tweak/decrease this value when error 2006 is gone), then `sudo
  /etc/init.d/mysql restart`. I didn't check, but the default value for `wait_timeout` might be around 28800 seconds (8 hours).
  
> ####Server dropped an incorrect or too large packet. 
> 
> How to fix:
> 
> If mysqld gets a packet that is too large or incorrect, it assumes that something has gone wrong with the client and closes the connection. You can increase the maximal packet size limit by increasing the value of `max_allowed_packet` in `my.cnf` file. 
> 
> On Debian: sudo vim
  `/etc/mysql/my.cnf`, set `max_allowed_packet = 64M` (you can tweak/decrease this value when error 2006 is gone), then `sudo
  /etc/init.d/mysql restart`.