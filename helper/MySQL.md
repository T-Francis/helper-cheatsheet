#**Mysql**

| [Official Site ](https://www.mysql.com/fr/) | [Official Doc](https://dev.mysql.com/doc/) |
| :---: | :---: |

![](../logos/MySQL-v1-128x128.png)

### Install

```bash
 sudo apt install mysql-server php-mysql
```

+ MySQL secure installation (optional)
```bash
 sudo mysql_secure_installation
```

***

### Optimisation de la config

[source blog idneo](http://blog.idneo.fr/configuration-optimisation-et-securisation-de-mysql/)

+ MySQLTuner
Script perl qui analyse l’activité MySQL
[source](https://github.com/major/MySQLTuner-perl)

```bash
wget http://mysqltuner.pl/ -O mysqltuner.pl
wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/basic_passwords.txt -O basic_passwords.txt
perl mysqltuner.pl
```

+ Mytop
surveillance de MySQL en temps réel
```bash
sudo apt-get install mytop
sudo mytop -u username -p password                 
sudo mytop -u username -p password -d databasename   
```
Regroupe toutes les bases de données
```bash
sudo mytop -u username -p password                 
```
Cible une base de de donnée particulière
```bash              
sudo mytop -u username -p password -d databasename   
```

+ Log des requetes lentes
```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Modifier la config
```bash
log_slow_queries_log = 1
slow_query_log_file = /var/log/mysql/mysql-slow.log
long_query_time = 2
```

***
### Helper

+ create a local user
```sql
CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'myuser@DB2017';
```

+ create a distant user
```sql
CREATE USER 'myuser'@'%' IDENTIFIED BY 'myuser@DB2017';
```

+ create a user datatabase if not exist
```sql
CREATE DATABASE IF NOT EXISTS myuser;
```

+ grant privileges for both user on his datatabase
```sql
GRANT ALL ON myuser.* TO 'myuser'@'localhost';
GRANT ALL ON myuser.* TO 'myuser'@'%';
```

+ privilege on all database
```sql
#GRANT ALL ON *.* TO 'myuser'@'localhost';
#GRANT ALL ON *.* TO 'myuser'@'%';
```

+ change a password as root for any user
```sql
#local user
SET PASSWORD FOR 'myuser'@'localhost' = 's3cr3t';
#distant user
SET PASSWORD FOR 'myuser'@'%' = 's3cr3t';
```

+ change a password as currentuser
```sql
SET PASSWORD = 's3cr3t';
```
