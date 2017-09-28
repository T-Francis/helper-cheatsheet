**Ubuntu extra install**

| [Ubuntu](https://ubuntu-fr.org/) | [Doc ubuntu](https://doc.ubuntu-fr.org/) | 
| :---: | :---: |

![](../logos/Ubuntu-v1-128x128.png)

### Update & Upgrade

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt update
sudo apt upgrade
```
***

### Extra

+ unity launcher to bottom
```bash
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```

+ unity launcher to left
```bash
gsettings set com.canonical.Unity.Launcher launcher-position left
```

+ install Sublime_text(ppa) ajouter le ppa, faire une update, installer git
```bash
  sudo add-apt-repository ppa:webupd8team/sublime-text-3
  sudo apt-get update
  sudo apt-get install sublime-text
```

+ enable minimize
```bash
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window true
```

+ install archive (zip, tar.gz, zip, 7zip rar etc)
```bash
sudo apt-get install unace unrar zip unzip p7zip-full p7zip-rar sharutils rar uudeview mpack arj cabextract file-roller
```

+ install java
```bash
sudo apt-get install openjdk-8-jdk
```

+ install synaptic
```bash
sudo apt-get install synaptic
```

+ install skype
```bash
sudo apt-get install skype
```

+ install qbittorrent
```bash
sudo apt-get install qbittorrent
```

+ install wine
```bash
sudo apt-get install wine winetricks
```

+ install gimp
```bash
sudo apt-get install gimp gimp-data gimp-plugin-registry gimp-data-extras
```

+ install laptop tools
```bash
sudo apt-get install laptop-mode-tools
```
***