# **Install & Secure a virtual private server(Ubuntu)**

| [Official Site ]() | [Official Doc]() |
| :---: | :---: |

![](../logos/Vps-v1-128x128.png)

### Connect & update

source : [doc ovh](https://docs.ovh.com/pages/releaseview.action?pageId=18121869)

source : [blog idneo](http://blog.idneo.fr/prise-en-main-serveur-dedie-kimsufi-ubuntu/)

+ Se connecter et changer le mdp root
```bash
ssh root@server
passwd
```

+ Update and upgrade
```bash
apt-get update
apt-get upgrade
```

+ Création d’un utilisateur
```bash
adduser userName
usermod -a -G root,adm,sudo userName #adm : Permet à l’utilisateur de consulter les fichiers de log dans /var/log
```

***

### Sécurisation de SSH

+ Création d’un groupe d’utilisateur ssh
```bash
addgroup sshusers
adduser userName sshusers
```

+ Securiser la config
```bash
nano /etc/ssh/sshd_config
```

+ Editer la config
```bash
# What ports, IPs and protocols we listen for /!\ Be carefull about what port you choose to listen to
Port 22
# Authentication:
LoginGraceTime 30          # Une connexion de 30 secondes en SSH sans authentification entraîne la déconnexion
PermitRootLogin no         # root login denied
StrictModes yes
MaxStartups 10:30:60       # 10 connexions sans authentification, sinon 30% de rejet jusqu'à 100% en 60 connexions
AllowGroups sshusers
# pour un seul utilisateur
# AllowUsers userName
```

+ Restart shh
```bash
service ssh restart
```

+ Se connecter
```bash
ssh userName@host.Ip.Adresses -p newPort
```

***

### Configurer le firewall network OVH

OVH propose gratuitement un firewall network pour votre serveur.
onglet IP de votre manager OVH puis cliquez sur l'engrenage en fin de ligne pour sélectionner "Activer le Firewall" :
Il est alors possible d'ajouter différentes règles pour sécuriser le VPS en choisissant différents critères :

La priorité de la règle (de 0 à 19) :
Cette dernière est important car elle permet d'indiquer les règles à remplir dans un certain ordre. La priorité 19 pouvant être une règle de rejet par défaut.
L'action : Accepter ou Refuser
Le protocole : TCP, UDP, AH, ESP, GRE, ICMP, IPv4

Selon certaines configurations peuvent s'ajouter :
IP Source
Port Source
Port Destination

***

### Configuration du réseau

+ Personnalisation du hostname:
```bash
sudo nano /etc/hostname
serveur.userName.fr
```
```bash
sudo nano /etc/hosts
127.0.0.1       localhost.localdomain localhost
176.31.120.208  serveur.userName.fr serveur
```

+ Synchronisation de l’heure du serveur avec NTP
```bash
apt-get update                
apt-get install ntp ntpdate   
```

+ Ajout du serveur horaire français
```bash
/etc/init.d/ntp stop
ntpdate fr.pool.ntp.org
/etc/init.d/ntp start
```

+ Update et reboot
```bash
apt-get upgrade
reboot
```

### Sécurité

+ Smurf Attack / Source routing / Syn Flood / Bad error messages / Redirects
```bash
sudo nano /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
```
```plain text
1
```
```bash
sudo nano /proc/sys/net/ipv4/conf/all/accept_source_route
```
```plain text
0
```
```bash
sudo nano /proc/sys/net/ipv4/tcp_syncookies
```
```plain text
1
```
```bash
sudo nano /proc/sys/net/ipv4/tcp_max_syn_backlog
```
```plain text
1024
```
```bash
sudo nano /proc/sys/net/ipv4/conf/all/rp_filter
```
```plain text
1
```
```bash
sudo nano /proc/sys/net/ipv4/icmp_ignore_bogus_error_responses
```
```plain text
1
```
```bash
sudo nano /proc/sys/net/ipv4/conf/all/accept_redirects
```
```plain text
0
```
```bash
sudo nano /proc/sys/net/ipv4/conf/all/secure_redirects
```
```plain text
0
```

***
