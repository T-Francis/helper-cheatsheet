**Inotify**

| [Official Doc](http://) | [Exploiter inotify](http://linuxfr.org/news/exploiter-inotify-c-est-simple) |
| :---: |

![](../logos/Bash-v1-128x128.png)

### Install

```bash
 sudo apt-get install inotify-tools
```
***


### Script

+ Example de serveillance sans traitement
[source example](http://info.figarola.fr/2009/11/06/linux-shell-gerer-les-evenements-inotify/)
```bash
#!/bin/bash

# -r indique de scruter récursivement le répertoire indiqué,
# -m passe la commande en mode monitoring
# -e les évènements à capturer
# –exclude fournit un motif de fichiers pour lequel aucun évènement ne sera transmis
# –format « %e|%w%f »
# output avec le type d’évènement et le nom du fichier concerné, séparés par |
# CREATE|/home/user/tmp/fileName (suite à la création de fileName).
# MODIFY|/home/user/tmp/fileName (suite à la modification de fileName)
# DELETE|/home/user/tmp/fileName (suite à la suppression de fileName)

# scrute récursivement le répertoire /home/user/rep en mode monitoring, capture les création, suppression, deplacement, modification et exclus les .log
# --format output

inotifywait -m -r -e create -e delete -e moved_to -e modify --exclude "*.log" \
            --format "%e|%w%f" /home/user/rep | while read res
do
event=`echo $res | sed s/\|.*$//`
src=`echo $res | sed s/^.*\|//`

case "$event" in
CREATE)
  # Traitement sur création d'un fichier
  ;;
CREATE,ISDIR)
  # Traitement sur création d'un répertoire
  ;;
DELETE)
  # Traitement sur suppression d'un fichier
  ;;
DELETE,ISDIR)
  # Traitement sur suppression d'un fichier
  ;;
MOVED_TO)
  # Traitement sur déplacement d'un fichier
  ;;
MODIFY)
  # Traitement sur modification d'un fichier
  ;;
esac
done
```

+ Homemade script fileLogger
```bash
#!/bin/bash

#le repertoire courant ou est appeler le script
dirPath=`pwd`

#on execute inotify en mode monitoring recursif sur les evenements création,modification,deplacement,suppression.
# --exclude ".md" par exemple aurait ignorer les evenement sur les .md
inotifywait -mrq -e create -e delete -e moved_to -e modify --format "%e %w%f" $dirPath | while read file
do

DATE=`date +%Y-%m-%d`
HOUR=`date +%H:%M`

#si le fichier de log n'existe pas on le creer et on log l'événement
if [ ! -e fileActivity.inotify.log ];then
touch fileActivity.inotify.log
chmod 777 fileActivity.inotify.log
echo -e "le fichier de log etait absent \nIl a été créer et le fichier précédent a correctement été logger" >> fileActivity.inotify.log
echo "[ $DATE $HOUR ] => $file" >> fileActivity.inotify.log

#sinon on log juste l'événement, saud ceux qui concerne la modification du fichier de log
else
case "$file" in
  "MODIFY $dirPath/fileActivity.inotify.log")
    # rien
    ;;
  *)
    # on log
    echo "[ $DATE $HOUR ] => $file" >> fileActivity.inotify.log
    ;;
esac
fi
done

```
***