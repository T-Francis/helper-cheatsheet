# **Tomcat**

| [Official Site ](http://tomcat.apache.org/) | [Official Doc](https://wiki.apache.org/tomcat/FrontPage) |
| :---: | :---: |

![](../logos/Tomcat-v1-128x128.png)

### Prérequis

+ update, install java jdk (si nécessaires)
```bash
 sudo apt-get update
 sudo apt-get install default-jdk
```

+ create Tomcat User

Par sécurité, il est préférable de créer des privilèges différents pour Tomcat
```bash
 sudo groupadd tomcat
 sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat
```
***

### Install

+ install Tomcat dans `/opt/tomcat`

Chercher la dernière version de Tomcat sur la [page de téléchargement](http://tomcat.apache.org/whichversion.html) et a `Core List`, copier le lien "tar.gz"
(e.g: http://www-us.apache.org/dist/tomcat/)
```bash
 cd /tmp
 curl -O http://www-us.apache.org/dist/tomcat/tomcat-9/link-of-version-of-you-found
 sudo mkdir /opt/tomcat
 sudo tar xzvf apache-tomcat-9*tar.gz -C /opt/tomcat --strip-components=1
```

+ update des permissions

Donner au group Tomcat les droits propriétaire
Donner au group Tomcat les droits d'Accès a la conf et son contenu
Faire de Tomcat le propriétaire des dossier approprié
```bash
 cd /opt/tomcat
 sudo chgrp -R tomcat /opt/tomcat
 sudo chmod -R g+r conf
 sudo chmod g+x conf
 sudo chown -R tomcat webapps/ work/ temp/ logs/

# give write permissions for the group on webapps
# sudo chmod -R g+w /opt/tomcat/webapps
```
***

### Tomcat Service File

Pour activer Tomcat en tant que service
```bash
 sudo update-java-alternatives -l
    #Output
    #java-1.8.0-openjdk-amd64       1081       /usr/lib/jvm/java-1.8.0-openjdk-amd64
```

On peut construire la variable d'environement JAVA en recopiant la colonne de droite de l'output generer et en ajoutant /jre
Par exemple, pour cet output, la variable JAVA serait :
```sh
    JAVA_HOME
    /usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
    # votre JAVA_HOME peut etre différent.
```

+ Tomcat.service file
```bash
 sudo nano /etc/systemd/system/tomcat.service
```

+ service file config example
```sh
    [Unit]
    Description=Apache Tomcat Web Application Container
    After=network.target

    [Service]
    Type=forking

    Environment=JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
    Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
    Environment=CATALINA_HOME=/opt/tomcat
    Environment=CATALINA_BASE=/opt/tomcat
    Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
    Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

    ExecStart=/opt/tomcat/bin/startup.sh
    ExecStop=/opt/tomcat/bin/shutdown.sh

    User=tomcat
    Group=tomcat
    UMask=0007
    RestartSec=10
    Restart=always

    [Install]
    WantedBy=multi-user.target
```

+ recharger le systemd daemon, démarrer Tomcat
```bash
  sudo systemctl daemon-reload
  sudo systemctl start tomcat
```

+ check status
```bash
 sudo systemctl status tomcat
```

+ autoriser le port 8080 pour le firewall
```bash
 sudo ufw allow 8080
```

+ tester de se connecter(dans navigateur)
```plain text
 http://localhost:8080
```

+ activer Tomcat en service
```plain text
 sudo systemctl enable tomcat
```
***

### Helper
~ none
***

### Config

+ configurer les utilisateurs de Tomcat
```sh
 sudo nano /opt/tomcat/conf/tomcat-users.xml
```
```xml
<tomcat-users . . .>
    <user username="admin" password="password" roles="manager-gui,admin-gui"/>
</tomcat-users>
```

+ configurer app manager interface

Par défaut, Tomcat restreint l'access au interfaces de gestion

APP
```sh
sudo nano /opt/tomcat/webapps/manager/META-INF/context.xml
```
Commenter la restriction d'IP et autoriser ce que l'on souhaite
```xml
<Context antiResourceLocking="false" privileged="true" >
  <!--<Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />-->
</Context>
```

HOST
```sh
sudo nano /opt/tomcat/webapps/host-manager/META-INF/context.xml
```
Commenter la restriction d'IP et autoriser ce que l'on souhaite
```xml
<Context antiResourceLocking="false" privileged="true" >
  <!--<Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />-->
</Context>
```

+ accès interface web(dans navigateur)

APP
```plain text
 http://server_domain_or_IP:8080/manager/html
```
HOST
```plain text
http://server_domain_or_IP:8080/host-manager/html/
```
***

TODO=> tester la procédure
### Coupler apache avec tomcat

+ Activez le mode proxy
```sh
sudo a2enmod proxy_http
```

+ Créer et éditer le fichier de config du vHost
```sh
sudo touch /etc/apache2/site-available/siteName.conf
sudo nano siteName.conf
```

+ Ajoutez la configuration
```plain text
<VirtualHost *:80>
    ServerName siteName
    ProxyPreserveHost On
    ProxyRequests On
    ProxyPass / 127.0.0.1 #ou adresse du site/appli sur tomcat
    ProxyPassReserve / 127.0.0.1 #ou adresse du site/appli sur tomcat
</VirtualHost>
```

+ Active la configuration, reload apache2
```sh
sudo a2ensite siteName.conf
sudo service apache2 reload
```
