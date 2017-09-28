# **SHH**.

| [Official Site ](https://www.openssh.com/) | [Official Doc](https://www.openssh.com/manual.html) |
| :---: | :---: |

![](../logos/SSH-v1-128x128.png)

### Install

```bash
 sudo apt-get install openssh-server
```

+ check le status
```bash
 sudo service ssh status
```
***

### Helper

+ se connecter en ssh(client)
```bash
 ssh userName@ip.of.the.hosta
```

+ éditer la config(host)(e.g., the listening port, and root login permission)
```bash
 sudo nano /etc/ssh/sshd_config
```

+ redemarrer le service(host)
```bash
 sudo service ssh restart
```
***

### Sécurisation de SSH

+ Création d’un groupe d’utilisateur ssh
```bash
sudo addgroup sshusers
sudo adduser userName sshusers
```

+ Securiser la config
```bash
sudo nano /etc/ssh/sshd_config
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
sudo service ssh restart
```

***
