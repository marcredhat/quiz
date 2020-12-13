## Install TCExam (Open Source system for electronic exams) on RHEL 8.2:

See 

https://tcexam.org/docs/installation/

https://access.redhat.com/solutions/2662201

https://computingforgeeks.com/how-to-install-php-7-2-7-1-on-rhel-8/


```bash
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo rpm -ivh http://www.rpmfind.net/linux/epel/7/x86_64/Packages/z/zbar-0.10-27.el7.x86_64.rpm
sudo dnf -y install libwmf
sudo rpm -ivh https://rpmfind.net/linux/epel/8/Everything/x86_64/Packages/g/GraphicsMagick-1.3.34-1.el8.x86_64.rpm
sudo dnf -y install -y  gd curl ImageMagick   texlive  zbar mysql-server httpd php php-posix php-mysqlnd php-pdo php-gd php-mbstring libdbi-dbd-mysql php-curl memcached
```

```text
In /etc/httpd/conf/httpd.conf, modify ServerName as follows:
ServerName localhost:80
```


```bash
sudo systemctl start mysqld httpd memcached

sudo systemctl enable mysqld httpd memcached

sudo systemctl status mysqld httpd memcached
```


```bash
mysql -u root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
quit;
```

```text
Check that you can connect as root with the new password
mysql -u root -h localhost -p
```

```bash
cd /var/www/html
sudo git clone https://github.com/tecnickcom/tcexam.git
```

```bash
semanage fcontext -R -a -t httpd_sys_rw_content_t '/var/www/html/tcexam/'
restorecon -R -v '/var/www/html/tcexam/'
```

```bash
ls /etc | grep php
php.d
php-fpm.conf
php-fpm.d
php.ini
```

```text
In /etc/php.ini, comment all lines referring to magic quotes
```

See my php.ini at https://github.com/marcredhat/quiz/blob/main/php.ini


```bash
sudo yum module install php:7.2
sudo systemctl enable --now php-fpm
```

```bash
ls /etc/httpd/modules/ | grep php
libphp7.so
```

```text
In /etc/httpd/conf/httpd.conf:
LoadModule php7_module modules/libphp7.so
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
```

```text
In /etc/httpd/conf.modules.d/00-mpm.conf,
comment 
#LoadModule mpm_event_module modules/mod_mpm_event.so
```

See my /etc/httpd/conf/httpd.conf and /etc/httpd/conf.modules.d/00-mpm.conf at
https://github.com/marcredhat/quiz/blob/main/httpd.conf
https://github.com/marcredhat/quiz/blob/main/00-mpm.conf


```bash
From laptop:
sudo ssh marc@127.0.0.1 -p 2222 -L 80:localhost:80
```


Browse to
http://127.0.0.1/tcexam/admin/code/index.php

Connect as admin/1234
