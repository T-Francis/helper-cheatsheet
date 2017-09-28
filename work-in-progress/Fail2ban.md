**Fail2BAN**

| [Official Site ](https://example.com/) | [config example source](https://blog.nicolargo.com/2012/02/proteger-son-serveur-en-utilisant-fail2ban.html) |
| :---: | :---: |

![](../logos/Fail2ban-v1-128x128.png)

### Installation

+ Install Fail2ban
```bash
apt-get install fail2ban
```

+ Adapter la configuration.
```bash
nano /etc/fail2ban/jail.conf
/etc/init.d/fail2ban restart
```

***

### Config Example

+ SSH Brute Force
```bash
sudo nano /etc/fail2ban/jail.conf
```
```plain text
[ssh]
enabled = true
port = ssh
filter = sshd
action = iptables[name=SSH, port=ssh, protocol=tcp]
logpath = /var/log/auth.log
maxretry = 3
bantime = 900
```

+ Attaque Ddos
```bash
sudo nano /etc/fail2ban/jail.conf
```
```plain text
[http-get-dos]
enabled = true
port = http,https
filter = http-get-dos
logpath = /var/log/apache2/*error.log
maxretry = 360
findtime = 120
action = iptables[name=HTTP, port=http, protocol=tcp]
mail-whois-lines[name=%(__name__)s, dest=%(destemail)s, logpath=%(logpath)s]
bantime = 600
```

Creer e filtre http-get-dos

```bash
sudo nano /etc/fail2ban/filter.d/http-get-dos.conf
```
```plain text
#
# Author: http://www.go2linux.org
#
[Definition]
# Option: failregex
# Note: This regex will match any GET entry in your logs, so basically all valid and not valid entries are a match.
# You should set up in the jail.conf file, the maxretry and findtime carefully in order to avoid false positives.
failregex = ^<HOST>.*\"GET
# Option: ignoreregex
# Notes.: regex to ignore. If this regex matches, the line is ignored.
# Values: TEXT
#
ignoreregex =
```

+ Redemarre le service
```bash
service fail2ban restart
```
***

