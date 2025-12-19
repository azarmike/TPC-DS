# TPC-DS for Greenplum 6 and GreenGage 7 on Ubuntu 22

--Запускать на мастере, требуется gcc9

sudo apt-get install git make bc g++ -y

sudo apt remove gcc -y

sudo apt-get install gcc-9 g++-9 -y

sudo ln /usr/bin/gcc-9 /usr/bin/gcc

gcc --version

--Запускаем под gpadmin

sudo su - gpadmin

cd /tmp

curl https://raw.githubusercontent.com/azarmike/TPC-DS/master/tpcds.sh > tpcds.sh

chmod 755 tpcds.sh

psql adb

create database gpadmin;

--Запускаем под root

sudo su -

cd /tmp

bash ./tpcds.sh

vi ./tpcds_variables.sh

bash ./tpcds.sh

--Для GreenGage 7 нужно дополнительно выполнить на мастере и сегментах:

sudo mkdir -p /usr/lib/gpdb/

sudo chown gpadmin:gpadmin /usr/lib/gpdb/

sudo ln /usr/lib/ggdb/greengage_path.sh /usr/lib/gpdb/greenplum_path.sh
