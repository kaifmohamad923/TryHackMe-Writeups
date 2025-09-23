# TryHackMe-Writeups

![alt text](TryHackMe-logo.png "Writeup Image")

This repository contains my TryHackMe CTF (Capture The Flag) writeups. Each writeup is organized by room, OS, description, and tools used.

Check out the TryHackMe website: <https://tryhackme.com>

Here's a link to my TryHackMe profile:

[![TryHackMe Profile](your-profile-image.png)](https://tryhackme.com/p/your-username)

> Replace `your-profile-image.png` with your badge image, and `your-username` with your TryHackMe username.

---

## TryHackMe Writeups Table

| Room Name | OS | Description | Tools Used |
|:---:|:---:|---|---|
| [Room 1 Name](room1/README.md) | Linux (Ubuntu) | Brief description of Room 1 | `nmap`, `gobuster` |
| [Room 2 Name](room2/README.md) | Windows 10 | Brief description of Room 2 | `nmap`, `metasploit`, `hydra` |
| [Room 3 Name](room3/README.md) | Linux (CentOS) | Brief description of Room 3 | `nmap`, `wpscan`, `john` |

> You can add more rows as you complete rooms. Make sure each room has its own folder with a `README.md`.

---

## Extra Notes

### My Security Cheat Sheet

I have notes and cheat sheets for pentesting. Could be helpful:

- <https://github.com/your-github-username/security-cheat-sheet/wiki>

### TryHackMe VPN Issues

If your internet doesn’t work with TryHackMe VPN:

```bash
$ nmcli connection   # Note your VPN connection name
$ nmcli connection edit <CONNECTION_NAME>
> set ipv4.never-default true
> set ipv6.never-default true
> save
> quit
