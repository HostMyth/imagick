# imagick
cPanel EasyApache 4 Installing Imagemagick and imagick PHP extension

This is a quick guide on how to install both the imagick PHP extension as well as the application via SSH.
This is fairly simple, just copy and paste the following into SSH.

1. Installing imagemagick:
```
yum -y install ImageMagick-devel ImageMagick-c++-devel ImageMagick-perl
```

2. Installing the imagemagick PHP extensions for PHP versions 5.4, 5.5, 5.6, 7.0 and 7.1
```
for phpver in $(ls -1 /opt/cpanel/ |grep ea-php | sed 's/ea-php//g') ; do
printf "\autodetect" | /opt/cpanel/ea-php$phpver/root/usr/bin/pecl install imagick
echo 'extension=imagick.so' >> /opt/cpanel/ea-php$phpver/root/etc/php.d/imagick.ini
done
/scripts/restartsrv_httpd
/scripts/restartsrv_apache_php_fpm
```
3.  Test to make sure imagemagick is installed:
```
/usr/bin/convert --version
```
4. Test to make sure the PHP extensions loaded:
```
for phpver in $(ls -1 /opt/cpanel/ |grep ea-php | sed 's/ea-php//g') ; do
echo "PHP $phpver" ; /opt/cpanel/ea-php$phpver/root/usr/bin/php -m |grep imagick
done
```
```
PHP 54
imagick
PHP 55
imagick
PHP 56
imagick
PHP 70
imagick
PHP 71
imagick
```
