On RHEL 8.2:

See https://tcexam.org/docs/installation/

```bash

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo rpm -ivh http://www.rpmfind.net/linux/epel/7/x86_64/Packages/z/zbar-0.10-27.el7.x86_64.rpm
sudo dnf -y install libwmf
sudo rpm -ivh https://rpmfind.net/linux/epel/8/Everything/x86_64/Packages/g/GraphicsMagick-1.3.34-1.el8.x86_64.rpm
sudo dnf -y install -y  gd curl ImageMagick   texlive  zbar mysql-server httpd php php-mysqlnd php-pdo php-gd php-mbstring libdbi-dbd-mysql php-curl memcached


```


vim /etc/httpd/conf/httpd.conf
Modify ServerName
ServerName localhost:80


sudo systemctl start mysqld httpd memcached

sudo systemctl enable mysqld httpd memcached

sudo systemctl status mysqld httpd memcached


mysql -u root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
quit;

Check that you can connect as root with the new password
mysql -u root -h localhost -p

cd /var/www/html
sudo git clone https://github.com/tecnickcom/tcexam.git

ls /etc | grep php
php.d
php-fpm.conf
php-fpm.d
php.ini

ls /etc/httpd/modules/ | grep php
libphp7.so

LoadModule php7_module modules/libphp7.so
