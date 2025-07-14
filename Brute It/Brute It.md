## Step 1: Reconnaissance

- do an nmap scan with service/version detection
- `nmap -sV 10.10.65.214`
![Pasted image 20250714151216.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714151216.png)

Now we can answer the following questions:
- **How many ports are open? - 2**
- **What version of SSH is running? - OpenSSH 7.6p1**
- **What version of Apache is running? - 2.4.29**
- **Which Linux distribution is running?  - Ubuntu**

Search for hidden directories with gobuster.
- `gobuster dir -u 10.10.65.214 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
- the medium wordlist was a bit of an overkill for this task
![Pasted image 20250714152537.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714152537.png)
- **What is the hidden directory? - /admin**

## Step 2: Getting a shell

- by just assuming that the login name will be admin, bruteforce the password with hydra
- `sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.65.214 http-post-form "/admin/:user=^USER^&pass=^PASS^:F=invalid" -V`

![Pasted image 20250714153958.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714153958.png)

- **What is the user:password of the admin panel? - admin:xavier**
- login on the webpage to get the web flag
- on the webpage we can also download a key. Safe it to a file and convert it to a format that john can use with `ssh2john key > hash.txt`
- then crack the hash with john `john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt 
`
![Pasted image 20250714161614.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714161614.png)

- **What is John's RSA Private Key passphrase? - rockinroll**
- now use the key to login via ssh, use john as login name, because the website said that it is john's key we downloaded
- first make sure that the key has the correct permissions `chmod 600 /path/to/key`
- specify private key to use with `-i`
- `ssh -i key john@10.10.65.214
- the flag is in the user.txt file

## Step 3: Privilege escalation

- see which programs john can run with root permissions with `sudo -l`
![Pasted image 20250714163126.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714163126.png)

- cat can be run with root privileges without a password
- use cat to read the shadow file that contains the password hashes
- the root password hash is at the top between the first two : `$6$zdk0.jUm$Vya24cGzM1duJkwM5b17Q205xDJ47LOAg/OpZvJ1gKbLF8PJBdKJA4a6M.JYPUTAaWu4infDjI88U9yUXEVgL.`
![Pasted image 20250714163210.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714163210.png)

- save the password hash to a file and crack it with john

![Pasted image 20250714163603.png](https://github.com/gernia/CTF_writeups/blob/main/Brute%20It/imgs/Pasted%20image%2020250714163603.png)

- **What is the root's password? - football**
- now use `su` to switch to root `su root`
- the flag is in the root folder in the root.txt file
