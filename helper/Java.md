# **Java8**

| [Official Site ](http://www.oracle.com/technetwork/java/index.html) | [Official Doc](https://docs.oracle.com/javase/8/docs/) |
| :---: | :---: |

![](../logos/Java-v1-128x128.png)

### Install

+ ajouter le ppa, faire une update, installer Java8
```bash
 sudo add-apt-repository ppa:webupd8team/java
 sudo apt-get update
 sudo apt-get install oracle-java8-installer
```

+ check la version
```bash
 java -version
```

+ configurer l'environnement
```bash
 sudo apt-get install oracle-java8-set-default
```

+ éditer l'environnement
```bash
 sudo nano /etc/environment
```
```plain text
    JAVA_HOME=/usr/lib/jvm/java-8-oracle
    JRE_HOME=/usr/lib/jvm/java-8-oracle/jre
```
***