**Expect**

| [Linux.die.net Manual ](https://linux.die.net/man/1/expect) |
| :---: |

![](../logos/Bash-v1-128x128.png)

### Install

```bash
sudo apt install expect
```
***

### Script example

+ Auto connect ssh (CLEARLY BAD PRACTICE)

I do not recommand at all to use it if you hardcode the password in the script.
even if i made it because I obviously use it, it was just made as a practice and play on a virtual local environnement
```bash
#!/usr/bin/expect

set host hostName or hostIp
set user userName
set password password

# we spawn the ssh service
spawn ssh "$user@$host"

# "*?assword*" as short regex for any typo of password and in any place in the expected prompted string
expect "*?assword*"
send "$password\n"

# interact no brain copy pasted from another script, didn't work without it, need to look deeper at the doc :s
interact
```
***