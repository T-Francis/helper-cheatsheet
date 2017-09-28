**PhP**

| [Official Site ](https://secure.php.net/) | [Official Doc](http://php.net/docs.php) |
| :---: | :---: |

![](../logos/PhP-v1-128x128.png)

### Install

```bash
 sudo apt install -y php
```
***

### Helper

+ suppression de PHP 5
```bash
systemctl stop php5-fpm
apt-get autoremove --purge php5*
```

+ install de PHP 7(debian / apache2), ajout du depot, update, upgrade et install
```bash
sudo echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list
sudo wget -O- https://www.dotdeb.org/dotdeb.gpg | apt-key add -
sudo apt update
sudo apt upgrade
sudo apt install php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-json php7.0-gd php7.0-mcrypt php7.0-msgpack php7.0-memcached php7.0-intl php7.0-sqlite3 php7.0-gmp php7.0-geoip php7.0-mbstring php7.0-xml php7.0-zip
```
***