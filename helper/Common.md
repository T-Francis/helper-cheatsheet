# **Common ubuntu / debian**

| [Ubuntu](https://doc.ubuntu-fr.org/) | [Debian](https://www.debian.org/doc/index.fr.html) | [gnu.org](https://www.gnu.org/software/bash/manual/) |
| :---: | :---: | :---: |

![](../logos/Bash-v1-128x128.png)

### Se déplacer, manipuler les fichiers

+ afficher de l'aide sur la commande
```bash
 commandName -help
```

+ se déplacer vers un dossier
```bash
 cd /le/nom/de/mon/dossier
```

+ savoir dans quel dossier on se trouve (Path of current Working Directory)
```bash
 pwd
```

+ afficher le contenu du dossier, les fichiers cachés, les informations sur les fichiers
```bash
 ls
 ls -a
 ls -l
```

+ créer un dossier, supprimer un dossier(vide) supprimer récursivement sans confirmation(attention!)
```bash
 mkdir dirName
 rmdir dirName
sudo  rm -rf dirName
```

+ créer un ficher, supprimer un fichier
```bash
 touch fileName
 rm fileName
```

+ copier un fichier
```bash
 cp fileName fileNameCopy
```

+ déplacer un fichier, des fichiers par extension
```bash
 mv fileName /le/chemin/du/dossier/cible
 mv *.ext /le/chemin/du/dossier/cible
```

+ éteindre la machine (peut nécessiter les droits sudo)
```bash
 sudo shutdown -h now
```

+ couper la connection ou la console/terminal
```bash
 exit
```

+ Connaitre l'espace disque restant
```bash
 df -h
```

+ Localiser la plupart des fichiers de log du system
```bash
 sudo locate *.log*
```

***

### Utilisateur & groupe

+ creer un groupe
```bash
sudo groupadd groupName
```

+ supprimer un groupe
```bash
sudo delgroup groupeName
```

+ creer un utilisateur (creation auto du /home etc...)
```bash
sudo adduser userName
```
+ creer un utilisateur (simplement l'utilisateur)
```bash
sudo useradd userName
```

+ supprimer un utilisateur
```bash
sudo deluser userName
```

+ changer le mot de passe d'un utilisateur
```bash
sudo passwd userName
```

+ lister les groupes
```bash
sudo compgen -g
```

+ lister les utilisateurs
```bash
sudo compgen -u
```

+ lister les utilisateurs d'un group
```bash
getent group groupName
```

+ ajouter un utilisateur au groupe des sudoers
```bash
sudo adduser userName sudo
```

+ ajouter un utilisateur un groupe
```bash
sudo usermod -a -G grouName userName
```

### Permissions

+ changer les droits d'un dossier de facon récursive
```bash
sudo  chmod 770 -R folderName/
```

+ les types
```plain text
u (user, utilisateur) représente la catégorie "propriétaire" ;
g (group, groupe) représente la catégorie "groupe propriétaire" ;
o (others, autres) représente la catégorie "reste du monde" ;
a (all, tous) représente l'ensemble des trois catégories.
```

+ Les modifications
```plain text
+ : ajouter
- : supprimer
= : affectation
```

+ Les droits
```plain text
r : read ⇒ lecture
w : write ⇒ écriture
x : execute ⇒ exécution
```

+ Example
```sh
sudo chmod u+rwx,g+rx-w,o+r-wx fichier
```
On ajoute la permission de lecture, d'écriture et d'exécution sur le fichier fichier pour le propriétaire ;
On ajoute la permission de lecture et d'exécution au groupe propriétaire, on retire la permission d'écriture ;
On ajoute la permission de lecture aux autres, on retire la permission d'écriture et d'exécution.
***

+ Ajouter un groupe en propriétaire de facon récursive
```sh
sudo chgrp -R groupName dirName
```

### Network

##### IP Static
+ connaitre l’adresse IP
```bash
 sudo ifconfig
```

+ éditer le fichier des interfaces réseau
```bash
 sudo nano /etc/network/interfaces
```

+ remplacer les lignes suivantes :
```plain text
 auto eth0
 iface eth0 inet dhcp
```
```sh
 auto eth0
 iface eth0 inet static #IP statique
     address 192.168.1.100 #définit l’adresse
     netmask 255.255.255.0 #définit le masque de réseau avec celui par défaut
     gateway 192.168.1.1 #définit la passerelle
```

+ redémarrer le service
```bash
 sudo /etc/init.d/networking restart #sur ubuntu => service networking restart
```
***


### Install Drivers

+ ajoutez la source
En fonction de la distribution, Ajoutez la source « contrib » et « non-free » à votre fichier /etc/apt/sources.list, par exemple pour Debian 8 "Jessie":
```bash
sudo echo "deb http://httpredir.debian.org/debian/ jessie main contrib non-free" > /etc/apt/sources.list.d/dotdeb.list
```

+ update
```bash
sudo apt-get update
```

##### ATI

+ installez les paquets firmware-linux-nonfree
```bash
sudo apt-get install firmware-linux-nonfree libgl1-mesa-dri xserver-xorg-video-ati
```

##### Broadcom

+ intaller le paquet wireless-tools
DKMS compilera le module wl adapté à votre système
```bash
sudo apt-get install linux-image-$(uname -r|sed 's,[^-]*-[^-]*-,,') linux-headers-$(uname -r|sed 's,[^-]*-[^-]*-,,') broadcom-sta-dkms
```

+ déchargez les modules en conflit
DKMS compilera le module wl adapté à votre système
```bash
modprobe -r b44 b43 b43legacy ssb brcmsmac bcma
```

+ chargez le module wl
DKMS compilera le module wl adapté à votre système
```bash
modprobe wl
```
***

### Auto Mount Drives at System Startup

+ get the UUID (Universally Unique Identifier) of the partition you want to mount
```bash
ls /dev/disk/by-label -g
```
or
install gksu
```bash
sudo apt-get install gksu
sudo blkid
```

+ create a mount point
```bash
sudo mkdir /media/ntfs
```

+ open fstab
```bash
gksu gedit /etc/fstab
```

+ add the following line in the fstab file and replace the above UUID number with the UUID you've got from step 1
```plain text
UUID=1234567890123456 /media/ntfs ntfs rw,nosuid,nodev,noatime,allow_other 0 0
```

+ Restart the system and check if the partition is mounted.
```bash
sudo reboot
```
***
