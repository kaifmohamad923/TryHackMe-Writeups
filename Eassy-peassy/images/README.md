# TryHackMe Writeup - Easy Peasy

- TryHackMe Room : <https://tryhackme.com/room/easypeasyctf>


![alt text]( easy-peasy-icon.png "OhSINT room Image")


Write-up and walkthrough of the TryHackMe ‘Easy Peasy’ room, including step-by-step process with screenshots.

# Tools Used
- `Nmap`
- `gobuster`

# Task1

## 1. How many ports are open?

To find this, first we have to run a command - `sudo nmap -sV -p- TARGET` 

![alt text]( q_1_1.png "Step 1 Image")

![alt text]( q_1_2.png "Step 1 Image")

As you can see, I found the 3 open ports


```commandline
3
```

## 2. What is the version of nginx?

you have to check on port 80
![alt text]( q_2_1.png "Step 1 Image")

```commandline
1.16.1
```

## 3. What is running on the highest port?

now lets check on port 65524 you can find answers of 1 to 3 by running only one command and that is -`sudo nmap -sV -p- TARGET` so you don't have to use different commands to find different answers here but i use different commands for every single questions

![alt text]( q_3_1.png "Step 1 Image")
now we can see Apache so thats the answer

```commandline
Apache
```

# Task2

## 4. Using GoBuster, find flag 1.

![alt text]( q_4_1.png "Step 1 Image")

now there is one more hidden directory and that is -`/whatever`  so simply visit there

![alt text]( q_4_2.png "Step 2 Image")

after that we have to check a page source

![alt text]( q_4_3.png "Step 3 Image")

and we can find this so to know what it is i simply ask to gemini 

![alt text]( q_4_4.png "Step 4 Image")

```commandline
flag{f1rs7_fl4g}
```

## 5. Further enumerate the machine, what is flag 2?

so in prevues question we performed -`gobuster` and we found hidden directory -`/roborts.txt` so simply visit there and you can find this

![alt text]( q_5_1.png "Step 1 Image")

no to decode it i use -`md5hashing.net`

![alt text]( q_5_2.png "Step 2 Image")

```commandline
flag{1m_s3c0nd_fl4g}
```

## 6. Crack the hash with easypeasy.txt, What is the flag 3?

so this time we can find direct answer on -`TARGETIP:65524/` so visit there and find carefully you can find answer

![alt text]( q_6_1.png "Step 1 Image")

```commandline
flag{9fdafbd64c47471a8f54cd3fc64cd312}
```

## 7. What is the hidden directory?

while finding a answer of question 6 you also seen this 

![alt text]( q_7_1.png "Step 1 Image")

to decode it you have to use format base62 on -`Cyberchef`

![alt text]( q_7_2.png "Step 2 Image")

```commandline
/n0th1ng3ls3m4tt3r
```

## 8. Using the wordlist that provided to you in this task crack the hash what is the password?

 now to find it you have visit TARGET-IP/n0th1ng3ls3m4tt3r and in that page view page source then you can see a hash 
 then crack it on -`md5hashing.net`

![alt text]( q_8_1.png "Step 1 Image")


```commandline
mypasswordforthatjob
```

## 9. 



```commandline

```

## 10. 



```commandline

```

## 11. 



```commandline

```

## Conclusion


