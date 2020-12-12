On RHEL 8.2:

```bash
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo rpm -ivh http://www.rpmfind.net/linux/epel/7/x86_64/Packages/z/zbar-0.10-27.el7.x86_64.rpm
sudo dnf -y install libwmf
sudo rpm -ivh https://rpmfind.net/linux/epel/8/Everything/x86_64/Packages/g/GraphicsMagick-1.3.34-1.el8.x86_64.rpm
sudo dnf -y install -y  gd curl ImageMagick   texlive  zbar mysql-server php httpd php-mysql libdbi-dbd-mysql php-gd php-curl memcached
```
