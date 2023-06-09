# OpenVPN setup
---
## Installing and setting up openvpn

### installation

root (not sudo) required for installation  
```
sudo apt update
```
```
sudo apt install tzdata
```  
  
set up timezone  
```
sudo dpkg-reconfigure tzdata
```  
  
check time  
```
timedatectl show
``` 
  
install packages as root (below for ubuntu 22.04)   
```
apt update && apt -y install ca-certificates wget net-tools gnupg
```  
```
wget https://as-repository.openvpn.net/as-repo-public.asc -qO /etc/apt/trusted.gpg.d/as-repository.asc
```  
```
echo "deb [arch=amd64 signed-by=/etc/apt/trusted.gpg.d/as-repository.asc] http://as-repository.openvpn.net/as/debian jammy main">/etc/apt/sources.list.d/openvpn-as-repo.list
```  
```
apt update && apt -y install openvpn-as
```  
---
#### setup

destroys current config and initiates new one from scratch
```
ovpn-init
```

check username (openvpn default) and password (autogenerated after version ?) all the way down  
then login with it on serverIP:port/admin (192.168.x.x:943/admin) - specified in init.log file
```
sudo cat /usr/local/openvpn_as/init.log
```  

log in as admin and add new user with wanted permissions (TOTO is two factor authentication),
then go to 192.168.x.x:943 - specified in init.log file , and log in as user. download config for your device and run it  
before connecting you need to forward or open ports on both server and router, depending on what you specified in config. default is 1194

---
### connecting
click connect on client app

### issues encountered
note: NetBox [port conflict](#NetBox) 
router incompability with ddns.

---

### Router
Set up ddns then follow  
[https://www.tp-link.com/us/user-guides/Archer-A6&C6_V2/chapter-11-vpn-server#ug-sub-title-1](https://www.tp-link.com/us/user-guides/Archer-A6&C6_V2/chapter-11-vpn-server#ug-sub-title-1)  
Error with version 2.5 and 2.6 CBC ciphers not working, did not try to fix used 2.4  
