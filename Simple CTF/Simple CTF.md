**Nmap Scan**

- scanning for ports in general 

![[Pasted image 20250706223739.png]]


EtherNetIP-1 is on port 2222, that's above port 1000, so there are 2 services running below port 1000.
How many services are running under port 1000? - 2

Doing the portscan again, we get
![[Pasted image 20250706231210.png]]

we can answer "What is running on the higher port" with ssh

**ZAP scan**
- first normal spider
- then forced browse site with directory-list-2.3-medium.txt
- found a lot, found http://10.10.129.58/simple/ 
- we also find http://10.10.129.58/simple/admin/login.php

**Website

- Website hat search bar
- we want to test it for sgli by entering ' OR '1'='1
- ![[Pasted image 20250707000421.png]]
- when we click on the link, we see some default templates explained and also a post that has been published by someone named mitch

**Hydra Password Bruteforce with username mitch**

`sudo hydra -l mitch -P /usr/share/wordlists/rockyou.txt 10.10.91.200 http-post-form "/simple/admin/login.php:username=^USER^&password=^PASS^&loginsubmit=Submit:F=incorrect" -V`


![[Pasted image 20250708215042.png]]

**FTP Server**
- you can login to the ftp server without credentials

![[Pasted image 20250708221613.png]]

The file says:
![[Pasted image 20250708221812.png]]
Dammit man... you'te the worst dev i've seen. You set the same pass for the system user, and the password is so weak... i cracked it in seconds. Gosh... what a mess!

**SSH**
- the ssh doesn't react when we try to log in
- with `ssh -vvv mitch@10.10.1.91` we see why: it tries to connect to port 22, but the ssh is running on port 2222
- log in with `ssh -p 2222 mitch@10.10.1.91
- the user.txt file has the flag G00d j0b, keep up!

**privilege escalation**
- see what the user can run with sudo `sudo -l`
- user can run vim with sudo
- ![[Pasted image 20250708224438.png]]
- start vim
	- `sudo vim`
- then escape to shell from vim by typing  `:!sh` in vim 
- ![[Pasted image 20250708224625.png]]
- navigate to folder named root, in root.txt is the flag W3ll d0n3. You made it!