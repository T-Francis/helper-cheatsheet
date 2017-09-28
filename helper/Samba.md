**Samba**

| [Official Site ](https://www.samba.org/) | [Official Doc](https://www.samba.org/samba/docs/) |
| :---: | :---: |

![](../logos/Samba-v1-128x128.png)

### Install

```bash
 sudo apt install samba
```

+ check status
```bash
 sudo smbstatus
```
***

### Helper

+ ajouter un utilisateur
```sh
 sudo smbpasswd -a username
```

+ supprimer un utilisateur
```sh
 sudo smbpasswd -x username
```

+ restart samba
```sh
 sudo systemctl restart smbd
```

+ monter un dossier de partage (client)
```bash
sudo mount //192.168.1.1/pathTo/sharedFolder /pathTo/sharedFolder/mountFolder/ -o username=userName
```

+  autoriser les connexion via compte (client windows)
```plain text
- Panneau de configuration > Réseaux et Internet > Groupe résidentiel > Modifier les paramètres de partage avancés
- Résidentiel ou professionnel > Connexions de groupe résidentiel > Utiliser les comptes d'utilisateur et les mots de passe
```
***

### Config

+ éditer la config
```sh
 sudo nano /etc/samba/smb.conf
```

+ example de config global
```sh
[global]
## Browsing/Identification ###
# Change this to the workgroup/NT-domain name your Samba server will part of
	workgroup = WORKGROUP
	netbios name = sambaHostMachineName
	public = yes
	security = user
```

+ example de partage
```sh
[folderNameOnNetwork]
path = /pathTo/folderToShare/
read only = no
writeable = yes
valid users = sambaUserName
comment = description of the share
```
***