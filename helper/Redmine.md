**Redmine**

| [Official Site ](http://www.redmine.org) | [Official Wiki ](http://www.redmine.org/projects/redmine/wiki) | [Official install unbuntu](http://www.redmine.org/projects/redmine/wiki/HowTo_Install_Redmine_on_Ubuntu_step_by_step) |
| :---: | :---: | :---: |

![](../logos/Redmine-v1-128x128.png)  

### Install

+ Install apache2 and depandancies
```bash
sudo apt-get install apache2 libapache2-mod-passenger
```

+ Install mySql
```bash
sudo apt-get install mysql-server mysql-client
```

+ Install redmine-mysql
```bash
sudo apt-get install redmine redmine-mysql
```

+ Be sure the bundler gem is installed
```bash
sudo gem update
sudo gem install bundler
```

+ Open the passenger.conf
```bash
sudo nano /etc/apache2/mods-available/passenger.conf
```
And add this line in the IfModule mod_pasenger.c instruction
```bash
PassengerDefaultUser www-data
```
***

### hosting STYLE A) in the 000-default.conf

+ create a symlink to connect Redmine
```bash
sudo ln -s /usr/share/redmine/public /var/www/html/redmine
```

+ modify 000-default.conf of apache2 site-available
```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```
And insert following with other directory block instructions
+ 
```bash
<Directory /var/www/html/redmine>
    RailsBaseURI /redmine
    PassengerResolveSymlinksInDocumentRoot on
</Directory>
```

### Hosting STYLE B) in a separated vHost redmine.conf

+ Create and set up a new .conf in apache2 sites-available
```bash
sudo nano /etc/apache2/sites-available/redmine.conf
```

+ Create a path for the logs
```bash
# ugly -m 777, need to look deeper at how create file with good owner/grp
sudo mkdir -m 777  /usr/share/redmine/logs
```

+ vHost example
```xml
<VirtualHost *:80>
	ServerAdmin redmineAdmin@yourMail.com
	ServerName redmine.dev

	DocumentRoot /usr/share/redmine/public

	<Directory /usr/share/redmine/public>
		RailsBaseURI /redmine
		PassengerResolveSymlinksInDocumentRoot on
	</Directory>
	
	ErrorLog /usr/share/redmine/logs/apache2.error.log
	CustomLog /usr/share/redmine/logs/apache2.access.log combined

</VirtualHost>
```
+ Add the url to your local hosts with the vHost serverName you given
```bash
sudo nano /etc/hosts
127.0.1.1	redmine.dev
```
***

### Loading

+ Create and set the ownership of a Gemfile.lock file
```bash
sudo touch /usr/share/redmine/Gemfile.lock
sudo chown www-data:www-data /usr/share/redmine/Gemfile.lock
```

+ Restart apache
```bash
sudo service apache2 restart
```
***