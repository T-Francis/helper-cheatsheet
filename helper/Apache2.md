# **Apache2**

| [Official Site ](https://httpd.apache.org/) | [Official Doc](https://httpd.apache.org/docs/2.4/) |
| :---: | :---: |

![](../logos/Apache2-v1-128x128.png)

### Install
```bash
sudo apt install apache2 libapache2-mod-php
```
***

### Helper

+ éditer un fichier de configuration d'un virtualhost avec sudo et nano (requiert des droits sudo)
```bash
sudo nano /ect/apache2/sites-available/siteName.conf
```

+ activer ou desactiver une configuration du dossier site-available et reload apache
```bash
sudo a2ensite siteName.conf
ou
sudo a2dissite siteName.conf
sudo service apache2 reload
```

+ éditer le fichiers hosts avec sudo et nano (requiert des droits sudo)
```bash
sudo nano /ect/hosts
```

+ demarrer, arreter, redemarrer apache
```bash
sudo service apache2 start
sudo service apache2 stop
sudo service apache2 restart
```

+ passer ww-data dans le groupe propriétaire
```bash
sudo chown www-data:www-data -R folderName/
```

+ activer le mode rewrite, headers d'apache
```bash
sudo a2enmod rewrite
sudo a2enmod headers
```
***

### Vhost Example

+ example de ficher vhost.conf
```xml
<VirtualHost *:80>
	ServerAdmin francis.contact.mail@gmail.com
	ServerName siteExample.com

	DocumentRoot /pathTo/projectFolder/siteExampleFolder/publicFolder

	<Directory /pathTo/projectFolder/siteExampleFolder/publicFolder>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Require all granted
	</Directory>

	ErrorLog /pathTo/projectFolder/siteExampleFolder/logs/apache2.error.log
	CustomLog /pathTo/projectFolder/siteExampleFolder/logs/apache2.access.log combined

</VirtualHost>
```
***
+ faire un lien symbolique dans le var/www/html/
```bash
sudo ln -s /path/of/your/project/folder/ /var/www/html/
```

