### SSH

isntall ssh service
```
sudo apt install openssh-server
```

verify status
```
sudo systemctl status ssh
```

if down
```
sudo systemctl enable ssh
```

allow ssh port in firewall (22)
```
sudo ufw allow ssh
```

connect to server on other machine
```
ssh username@ipaddress
```




#### shows hardware information extracted from smbois
```
sudo dmidecode -t <hardware>
```

`<hardware>` = processor, memory, bios etc
0 - bios, 4 -processor, 16 - memory

 extract hardware to file
```bash
#!/bin/bash
echo "basic hardware info..."
echo -e "\nenter name of file: "
read the_name
sudo dmidecode -t 1 >> the_name
sudo dmidecode -t 4 >> the_name
sudo dmidecode -t 16 >> the_name
sudo df -h >> the_name
echo "\nexported!"
```

```
sudo bash ./<scriptname.sh>
```



---

### SAMBA
`sudo apt install samba` install samba
create directory you want to share and at end of  `/etc/samba/smb.conf` add:
```
[<directoryname>]
    comment = Samba on Ubuntu
    path = /we/we/<directoryname>
    valid users = 
    read only = no
    browsable = yes
```

then do a 
`sudo service smbd restart`
`sudo ufw allow samba`

set up samba users and passwords
`sudo smbpasswd -a username`

**Linux file permissions override samba permissions!!!**
