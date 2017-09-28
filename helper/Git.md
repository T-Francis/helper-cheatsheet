# **Git**

| [Official Site ](https://git-scm.com/) | [Official Doc](https://git-scm.com/doc) |
| :---: | :---: |

![](../logos/Git-v1-128x128.png)

### Install

+ ajouter le ppa, faire une update, installer git
```bash
  sudo add-apt-repository ppa:git-core/ppa
  sudo apt-get update
  sudo apt-get install git
```

+ check la version
```bash
 git --version
```
***

### helper

+ initialiser git
```bash
  git init
```

+ afficher l'aide
```bash
 git --help
```

+ on afficher l'aide sur config
```bash
 git git help config
```

+ config globale
```bash
 git config --global user.name "Francis Tessier"
 git config --global user.email "francis.contact.mail@gmail.com"
 git config --global color.ui true
```

+ liste des configs
```bash
 git config --list
```

+ créer un fichier
```bash
 touch fileName.ext
```

+ check le status du repository
```bash
 git status
```

+ créer le .gitignore
```bash
 touch .gitignore
```

+ le .git ignore
```bash
 ignore une extension ->  *.tmp
 ignore un dossier et son contenu -> tmp/*
```

+ ajouter par extension
```bash
 git add "*.html"
```

+ ajouter tous les fichiers au tracking
```bash
 git add --all
```

+ ajouter un fichier, dossier au tracking
```bash
 git add readme.md
 git add nomDossier
 git add *.html
 git add --all
```

+ commit avec un commentaire
```bash
 git commit -m "Mon premier commit"
```

+ commit et add avec un commentaire
```bash
 git commit -a -m "Ajout de tout les fichiers"
```

+ affiche les log
```bash
 git log
```

+ affiche les options des logs
```bash
 git help log
```

+ logs sur une ligne
```bash
 git log --oneline
 git log --oneline readme.md
```

+ logs d'un fichier (q pour quitter)
```bash
 git log -p readme.md
```

+ commande pour afficher les differences
```bash
 git diff
 git diff a45Fv54
 git diff a45Fv54..gf4244g
```

+ revenir sur un commit
```bash
 git checkout a45Fv54
```

+ créer une branche
```bash
 git branch nouvelleBranche
```

+ switch sur une branche
```bash
 git checkout dev
 git checkout master
 git checkout nouvelleBranche
```

+ fusionne les modifications d'une branche avec une autre
```bash
 git merge nouvelleBranche
```

+ supprime une branche, -D si pas fusionner
```bash
 git -d nouvelleBranche
 git -D nouvelleBranche
```

+ créer un remote avec l'historique sans dossier de travail
```bash
 git init --bare
```

+ liste les dépôts distants, les chemins associés
```bash
 git remote
 git remote -v
```

+ ajoute, supprime, renomme un nouveau dépôt
```bash
 git remote add aliasName chemin/url #
 git remote rm aliasName
 git remote rename oldName newName
```

+ pousse les modifications sur une ou toutes les branches sur le remote
```bash
 git push remoteName branchName
 git push remoteName --all
```

+ récupere les modifications du remote ou d'une branche du remote
```bash
 git pull remoteName
 git pull remoteName branchName
```

+ push sur un repo initialiser vide sur gitHub
```bash
  git init
  git add --all
  git commit -m "initial commit"
  git remote add origin https://github.com/T-Francis/repoName.git
  git push -u origin master
```

+ push un repo existant
```bash
git remote add origin https://github.com/T-Francis/repoName.git
git push -u origin master
```
***
