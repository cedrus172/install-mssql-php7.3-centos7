curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
yum clean all
yum update -y
ACCEPT_EULA=Y yum install -y msodbcsql mssql-tools unixODBC-devel
cd /tmp
wget https://pecl.php.net/get/sqlsrv-5.8.1.tgz
tar -zxvf sqlsrv-5.8.1.tgz
cd sqlsrv-5.8.1
/www/server/php/73/bin/phpize
./configure --with-php-config=/www/server/php/73/bin/php-config
make
make install

echo "extension=sqlsrv.so" >> /www/server/php/73/etc/php.ini
