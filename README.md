# ZABBIX_INSTALL_5.4
INSTALAÇÃO DO ZABBIX 5.4 LTS



sudo apt install wget
sudo su

wget https://repo.zabbix.com/zabbix/5.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.0-1+focal_all.deb
dpkg -i zabbix-release_5.0-1+focal_all.deb

apt update
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-agent
apt install mariadb-server
mysql -uroot -p 
Digite uma senha para seu BD
mysql> create database zabbix character set utf8 collate utf8_bin;
mysql> create user zabbix@localhost identified by 'senha que você digitou acima';
mysql> grant all privileges on zabbix.* to zabbix@localhost;
mysql> quit;
zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix
nano /etc/zabbix/zabbix_server.conf
Localize a linha:
DBPassword=password
Descomente e insira a senha do BD criada no passo anterior e salve.
nano /etc/zabbix/apache.conf
Localize a linha:
# php_value date.timezone Europe/Riga
Altere para America/Sao_Paulo salve e feche o arquivo.
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
