# TPC-DS for GreenGage 6 and 7 on Ubuntu22 and AltLinux10

########## Запуск на Ubuntu22. Запускать на мастере, требуется gcc9:

sudo apt-get install git make bc g++ -y

sudo apt remove gcc -y

sudo apt-get install gcc-9 g++-9 -y

sudo ln /usr/bin/gcc-9 /usr/bin/gcc

gcc --version

########## Запуск на AltLinux10. Запускать на мастере, требуется gcc9:

sudo su -

vi /etc/apt/sources.list.d/altsp.list

rpm [cert8] https://mirror.yandex.ru/altlinux c10f2/branch/x86_64 classic gostcrypto

rpm [cert8] https://mirror.yandex.ru/altlinux c10f2/branch/x86_64-i586 classic

rpm [cert8] https://mirror.yandex.ru/altlinux c10f2/branch/noarch classic

apt-get update

apt-get install gcc9 git bc make -y 

ln /usr/bin/gcc-9 /usr/bin/x86_64-alt-linux-gcc

gcc --version

########## Далее независимо от OS, запускаем под gpadmin:

sudo su - gpadmin

cd /tmp

curl https://raw.githubusercontent.com/azarmike/TPC-DS/master/tpcds.sh > tpcds.sh

chmod 755 tpcds.sh

psql adb

create database gpadmin;

########## Запускаем под root:

sudo su -

cd /tmp

bash ./tpcds.sh

vi ./tpcds_variables.sh

bash ./tpcds.sh

########## Для GreenGage 7 нужно дополнительно выполнить на мастере и сегментах:

sudo mkdir -p /usr/lib/gpdb/

sudo chown gpadmin:gpadmin /usr/lib/gpdb/

sudo ln /usr/lib/ggdb/greengage_path.sh /usr/lib/gpdb/greenplum_path.sh

sudo mkdir -p /usr/lib/gpdb/bin

sudo chown gpadmin:gpadmin /usr/lib/gpdb/bin

sudo ln /usr/lib/ggdb/bin/gpfdist /usr/lib/gpdb/bin/gpfdist
