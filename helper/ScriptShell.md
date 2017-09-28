**Script Shell**

| [Ubuntu Script Shell Doc](https://doc.ubuntu-fr.org/tutoriel/script_shell) | [linuxcommand.org](http://linuxcommand.org/) |
| :---: | :---: |

![](../logos/Bash-v1-128x128.png)

### Helper

+ STRING Test
```bash
# si str1 vaut str2
[ $str1 = $str2 ]

# si str1 est différent de str2
[ $str1 != $str2 ]

# si str est vide
[ -z $str ]

# si str est pleine
[ -n $str ]
```

+ NUMBERS Test
```bash
# si deux nombres sont égaux
[ $int1 -eq $int2 ]

# si deux nombres sont différents
[ $int1 -ne $int2 ]

# si int1 est strictement inférieur (<) a int2
[ $int1 -lt $int2 ]
  
# si int1 est inférieur ou égal(<=) a int2
[ $int1 -le $int2 ]
 
# si int1 est strictement supérieur (>) a int2
[ $int1 -gt $int2 ]
 
# si int1 est supérieur ou égal(>=) a int2
[ $int1 -ge $int2 ]
```

+ FILE Test
```bash
# si le fichier existe
[ -e $fileName ]

# si le fichiers EST un repertoire
[ -d $fileName ]

# si le fichier EST un fichier
[ -f $fileName ]

# si le fichier EST un lien symbolique
[ -L $fileName ]

# si le fichier est lisible
[ -r $fileName ]

# si le fichier est modifiable
[ -w $fileName ]

# si le fichier est executable
[ -x $fileName ]

# si le fichier est plus récent
[ $file1 -nt $file2 ]

# si le fichier est plus vieux
[ $file1 -ot $file2 ]
```

+ AND Operator
```bash
# si la str1 vaut str2 et que in1 est egal a 1
[ str1 = str2 ] && [ $int1 -eq 1 ]
```

+ OR Operator
```bash
# si str vaut Yes ou yes ou y
[ str = "Yes" ] || [ $str = "yes" ] || [ $str = "y" ]
```

+ CASE
```bash
# le cas ou str vaut francis, le cas ou str vaut balthazar, le cas par défauts
case $str in
	"francis")
		echo "hello francis"
		;;
	"balthazar")
		echo "hello balthazar"
		;;
	*)
	echo "je ne connais pas ce prénom"
esac
```
```bash
case $str in
	"francis" | "balthazar" | "Quentin")
		echo "Vous êtes stagiaires"
		;;
	"Dominique" | "Jean-Jacques")
		echo "vous êtes formateurs"
		;;
	*)
		echo "vous n'êtes ni stagiaires ni formateur"
		;;
esac
```

+ WHILE
```bash
# tant que la réponse est vide OU n'est pas égal a yes
while [ -z $rep ] || [ $rep != 'yes']
do
	read -p "Enter 'yes' :" rep
done
```

+ UNTIL
```bash
# jusqu'a ce que la réponse soit pleine ET égal a yes
until [ -n $rep ] || [ $rep = 'yes']
do
	read -p "Enter 'yes' :" rep
done
```

+ Make a bash executable
```bash
chmod +x scriptName.sh
```

+ Execute a script (may require sudo if script content need it)
```bash
./scriptName.sh
```
***

### Make a bash globally executable

#### Add an alias that point on your script

+ Open your .bashrc in you user folder
```bash
cd ~
sudo nano .bashrc
```
+ Add an alias with the path/to/yourScript.sh
```plain-text
alias comandName='sh -c /path/to/yourScript.sh'
``̀

#### Add your script to your or the shared bin/ directory

+ If your are the only use on the machine, you can both
```bash
 sudo cp scriptName.sh /usr/bin/scriptName
 sudo cp scriptName.sh /usr/local/bin
```

+ If you want you share you script with other user you MUST need to use
```bash
 sudo cp scriptName.sh /usr/local/bin
```
***