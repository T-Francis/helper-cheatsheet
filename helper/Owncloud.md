**Owncloud Default Install**

| [Official Site ](https://owncloud.org/) | [Official Doc](https://doc.owncloud.org/) |
| :---: | :---: |

![](../logos/Owncloud-v1-128x128.png)

### Install

+ ajoutez la clef
En fonction de la distribution, par exemple pour Debian 8 "Jessie":
```bash
 wget -nv https://download.owncloud.org/download/repositories/stable/Debian_8.0/Release.key -O Release.key
 apt-key add - < Release.key
```

+ ajoutez la source et le repo
En fonction de la distribution, Ajoutez la source « contrib » et « non-free » à votre fichier /etc/apt/sources.list, par exemple pour Debian 8 "Jessie":
```bash
 sh -c "echo 'deb http://download.owncloud.org/download/repositories/stable/Debian_8.0/ /' > /etc/apt/sources.list.d/owncloud.list"
 apt-get update
 apt-get install owncloud
```

+ ajout de www-data en proprietaire
```bash
cd /var/www/
chown www-data:www-data -R owncloud/
```

+ les permissions
```bash
chmod 770 -R owncloud/
```

+ activation des mods apache2
```bash
 a2enmod rewrite
 a2enmod headers
```
***

### Example vhost.conf
```xml
<VirtualHost *:80>
	ServerAdmin francis.contact.mail@gmail.com
	ServerName aliart-dev

	DocumentRoot /var/www/owncloud

	<Directory /var/www/owncloud>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Require all granted

		<IfModule mod_dav.c>
		 Dav off
		</IfModule>

		SetEnv HOME /var/www/owncloud
		SetEnv HTTP_HOME /var/www/owncloud
	</Directory>

	ErrorLog /var/www/owncloud.apache2.error.log
	CustomLog /var/www/owncloud.apache2.access.log combined

</VirtualHost>
```

+ redémarrer les services
```bash
a2ensite owncloud.conf
service apache2 restart
service apache2 reload
```
