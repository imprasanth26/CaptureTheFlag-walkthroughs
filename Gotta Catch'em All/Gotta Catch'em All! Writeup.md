# Gotta Catch'em All!  Writeup

# Scanning:

```python
nmap -Pn -sCV -A -T4 10.10.138.238
```

```python
nmap -Pn -sCV -A -T4 10.10.138.238

Starting Nmap 7.95 ( https://nmap.org ) at 2025-06-17 14:28 IST
Nmap scan report for 10.10.138.238
Host is up (0.18s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 58:14:75:69:1e:a9:59:5f:b2:3a:69:1c:6c:78:5c:27 (RSA)
|   256 23:f5:fb:e7:57:c2:a5:3e:c2:26:29:0e:74:db:37:c2 (ECDSA)
|_  256 f1:9b:b5:8a:b9:29:aa:b6:aa:a2:52:4a:6e:65:95:c5 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Can You Find Them All?
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
Network Distance: 5 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 3306/tcp)
HOP RTT       ADDRESS
1   38.90 ms  10.17.0.1
2   ... 4
5   192.09 ms 10.10.138.238

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.53 seconds
                                                              
```

# Enumeration:

```python
gobuster dir -u http://10.10.138.238:80 -w /usr/share/dirb/wordlists/common.txt
```

```python
 gobuster dir -u http://10.10.138.238:80 -w /usr/share/dirb/wordlists/common.txt                                  
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.138.238:80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 278]
/.hta                 (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/index.html           (Status: 200) [Size: 11217]
/server-status        (Status: 403) [Size: 278]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================

```

### We can’t find that much details with Gobuster, Let’s check on the website!

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image.png)

### On the Apace page-source we find a username and password

### 

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%201.png)

### Since we already know that the target machine running a secure shell(ssh). So let’s try these credentials there.

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%202.png)

### So the credentials that provided on page-source is correct. We connected to the ssh

### While exploring the shell we obtained, we found a ZIP file in the Desktop directory. After unzipping the file, we were provided with a hex-encoded string

### 

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%203.png)

### After converting the hex-encoded data to text, we retrieved the first flag.

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%204.png)

# Second flag:

## The given hint is “Maybe the website has an answer?”

## While locate the flag but it’s name on terminal we get,

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%205.png)

### The flag we found in the text file appeared to be encrypted using the Caesar Cipher algorithm. By using an online tool, we were able to retrieve our second flag.

# Third flag:

### While locating the third flag by its name in the terminal, we found the flag encoded in Base64. After decoding it, we obtained our flag.

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%206.png)

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%207.png)

# Privilege Escalation:

# Final flag:

### After searching a bit, we found the credentials of the user 'Ash'.

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%208.png)

### With those credentials, we successfully logged in as the user 'Ash'.

### Then we found the final root flag!

![image.png](Gotta%20Catch'em%20All!%20Writeup%20215aae3b76d0801c9727f7e67c3e0fad/image%209.png)

## Conclusion:

### Finally, we found all the flags! This room was created especially for beginners. I hope you enjoyed exploring this room with me.