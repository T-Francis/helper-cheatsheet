**Helper**

| [Blog idneo (source)](http://blog.idneo.fr/monitoring-serveur-dedie-ubuntu/) |
| :---: |

![](../logos/Bash-v1-128x128.png)

### Munin
[Munin official site](http://munin-monitoring.org/)

Outil de surveillance système et réseau qui génère une série de graphes permettant d’avoir des informations sur Apache2

+ Installation et edition du fichier de config
```bash
 sudo apt-get install munin-node
 sudo nano /etc/munin/munin.conf
```
```plain text
dbdir   /var/lib/munin
htmldir /var/www/util/munin
logdir /var/log/munin
rundir  /var/run/munin
```

+ Création des dossiers, permissions et redémarrage des services
```sh
sudo mkdir -p /var/www/util/munin
sudo chown munin:munin /var/www/util/munin
sudo /etc/init.d/munin-node restart
```

+ Consulter les graphiques
```sh
firefox -new-window http://monserveur/util/munin &
```

***

### PhpSysInfo

propose une interface web affichant clairement toutes les informations systèmes et matériels du serveur

+ Installation et edition du fichier de config
```bash
sudo cd /var/www/util
sudo wget http://downloads.sourceforge.net/project/phpsysinfo/phpsysinfo/3.0.20/phpsysinfo-3.0.20.tar.gz
sudo tar -xf phpsysinfo-3.0.20.tar.gz phpsysinfo
sudo cd phpsysinfo/
sudo mv config.php.new config.php
sudo nano config.php
```
```plain text
define('PSI_DEFAULT_LANG', 'fr');
define('PSI_SENSOR_PROGRAM', 'LMSensors');
define('PSI_HIDE_FS_TYPES', 'tmpfs,devtmpfs'); # On cache les systèmes de fichier inutiles
```

+ Installation de lm sensors
dépendance utile
```bash
sudo apt-get install lm-sensors
```

+ Consulter
```bash
firefox -new-window http://monserveur/util/phpsysyinfo &
```

***

### Monit
[Munin official site](https://mmonit.com/monit/)

Surveille le fonctionnement des services, par mail en cas de défaillance et tente de redémarrer les services arrêtés.
propose une interface web affichant clairement toutes les informations systèmes et matériels du serveur

+ Installation et édition du fichier de config
```bash
sudo apt-get install monit
sudo nano /etc/monit/conf.d/maconfig
```

adapté à la configuration de votre serveur si vous avez modifié les ports par défaut

```plain text
set daemon  60                                 # On vérifie toutes les 60 secondes
set logfile syslog facility log_daemon
set mailserver localhost
set mail-format {
  subject: [Monit] $HOST - $SERVICE $EVENT
}
set alert serveur@idneo.fr                     # Destinataire
set httpd port 8123 and                        # Port pour l'accès à l'interface web
    allow login:passwd                         # login et mot de passe de connexion
```

#### Scripts de surveillance des services

+ Apache2

check process apache with pidfile /var/run/apache2.pid
group apache
start program = &quot;/etc/init.d/apache2 start&quot;
stop program = &quot;/etc/init.d/apache2 stop&quot;
if failed host www.idneo.fr port 80
protocol http then restart
if 5 restarts within 5 cycles then timeout
if cpu &gt; 80% for 2 cycles then alert
if cpu &gt; 90% for 5 cycles then restart
if children &gt; 250 then restart

+ MySQL

check process mysqld with pidfile /var/run/mysqld/mysqld.pid  # a adapter au serveur
group database
start program = &quot;/etc/init.d/mysql start&quot;
stop program = &quot;/etc/init.d/mysql stop&quot;
if failed host 127.0.0.1 port 3306 then restart
if 5 restarts within 5 cycles then timeout

+ SSH

check process sshd with pidfile /var/run/sshd.pid
group ssh
start program &quot;/etc/init.d/ssh start&quot;
stop program &quot;/etc/init.d/ssh stop&quot;
if failed host 127.0.0.1 port 1234 protocol ssh then restart
if 5 restarts within 5 cycles then timeout

+ Postfix

check process postfix with pidfile /var/spool/postfix/pid/master.pid
group mail
start program = &quot;/etc/init.d/postfix start&quot;
stop  program = &quot;/etc/init.d/postfix stop&quot;
if failed port 25 protocol smtp then restart
if 5 restarts within 5 cycles then timeout

+ bind

check process bind9 with pidfile /var/run/named/named.pid
group bind
start program = &quot;/etc/init.d/bind9 start&quot;
stop  program = &quot;/etc/init.d/bind9 stop&quot;
if failed port 53 then restart
if 5 restarts within 5 cycles then timeout

+ Disk

check device sda3 with path /dev/sda3
if space usage &gt; 85% then alert
group system
```

+ Check de la syntax et redemarrage du service
```bash
sudo /etc/init.d/monit syntax
sudo /etc/init.d/monit start
```

l’interface web de gestion de Monit est accessible sur le port défini dans la config avec le login et le mot de passe

***

### Logwatch
Logwatch est un démon qui va se charger d’analyser et résumer les logs générés par les autres services

+ Installation
```bash
sudo apt-get install logwatch
```

+ Edition du mot de passe
```bash
sudo apt-get install logwatch
```
```
sudo nano /usr/share/logwatch/default.conf/logwatch.conf
MailTo = your@yourmail.fr
```
Le mail de rapport vous donnera des informations sur
-Les erreurs httpd, Les connexions FTP et SSH, Les mails envoyés par Postfix

***
