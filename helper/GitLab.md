**GitLab**

| [Official Site ](https://about.gitlab.com/) | [Officla install Omnibus](https://about.gitlab.com/installation/) | [Optionnal install source](https://kevingoedecke.me/2015/09/17/setup-gitlab-on-debian-7-with-existing-apache-webserver/) |
| :---: | :---: | :---: |

![](../logos/GitLab-v1-128x128.png)  

### Install (ubuntu Omnibus)

+  Install dependencies 
```bash
sudo apt-get install curl openssh-server ca-certificates postfix -y
```

+ Add and install GitLab package
```bash
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo apt-get install gitlab-ce
```

*NOTE* : if you expercienced some issue with interuption during the installation, run
```bash
sudo apt-get install gitlab-ce --fix-missing
```

+ Configure and start GitLab 
```bash
sudo gitlab-ctl reconfigure
```
***

### Optionnal install Sub-domain with apache2 and other hosted app/websites cohabitation 

After you install git lab you may want it as a subdomain of the host so you can use some other hosted app

[source](https://kevingoedecke.me/2015/09/17/setup-gitlab-on-debian-7-with-existing-apache-webserver/)

+ Open gitlab.rb
```bash
sudo nano /etc/gitlab/gitlab.rb
```

+ Set the wanted url and add nginx and web_server instructions
```bash
external_url 'http://gitlab.projectName.fr'
nginx['enable'] = false
web_server['external_users'] = ['www-data']
```
you can optionnaly use the command below as it's made in the source guide, but i didn't and it still worked, need to look deeper if it's related with the slowness issue I expercienced with git
```bash
sudo useradd -G gitlab-www ww-data
```

+ Create the new virtual host
```bash
cd /etc/apache2/sites-available/
sudo nano gitlab.conf
```

+ vHost example
this vHost need to be improve, need to llok deeper at location / instruction 
@need to add the stackoverflow vhost config
```xml
<VirtualHost *:80>
  ServerName gitlab.projectName.fr
  ServerSignature Off
 
  ProxyPreserveHost On
 
  <Location />
    Order deny,allow
    Allow from all
    Require all granted

    ProxyPassReverse http://127.0.0.1:8080
    ProxyPassReverse http://gitlab.projectName.fr/
  </Location>
 
  RewriteEngine on
  RewriteCond %{DOCUMENT_ROOT}/%{REQUEST_FILENAME} !-f
  RewriteRule .* http://127.0.0.1:8080%{REQUEST_URI} [P,QSA]
 
  # needed for downloading attachments
  DocumentRoot /opt/gitlab/embedded/service/gitlab-rails/public
 
</VirtualHost>
```

+ Add the url to your local hosts
```bash
sudo nano /etc/hosts
127.0.1.1	gitlab.projectName.fr
```

+ 
```bash
sudo a2ensite gitlab
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo service apache2 restart
```

+ Finally reconfigure the gitlab
```bash
sudo gitlab-ctl reconfigure
```

+ Test the job
```bash
firefox -new-window http://gitlab.projectName.fr &
```
***