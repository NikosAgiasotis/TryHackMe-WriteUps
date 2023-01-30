# TryHackMe-Easy Peasy (CTF)


## 📌 TASK 1 : Enumeration through Nmap
<br>
First of all we have to scan our machine for open ports. <br>
📜 Command : sudo nmap -sV -A -p- -sC IP
<br>

Output : 
<br>

```html
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-30 20:35 EET
Nmap scan report for 10.10.129.58
Host is up (0.071s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
80/tcp    open  http    nginx 1.16.1
|_http-title: Welcome to nginx!
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: nginx/1.16.1
6498/tcp  open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 304a2b22acd95609f2da122057f46cd4 (RSA)
|   256 bf86c9c7b7ef8c8bb994ae0188c0854d (ECDSA)
|_  256 a172ef6c812913ef5a6c24034cfe3d0b (ED25519)
65524/tcp open  http    Apache httpd 2.4.43 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/
|_http-title: Apache2 Debian Default Page: It works
|_http-server-header: Apache/2.4.43 (Ubuntu)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=1/30%OT=80%CT=1%CU=44246%PV=Y%DS=2%DC=T%G=Y%TM=63D80E5
OS:D%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=10F%TI=Z%CI=Z%II=I%TS=A)OPS
OS:(O1=M506ST11NW7%O2=M506ST11NW7%O3=M506NNT11NW7%O4=M506ST11NW7%O5=M506ST1
OS:1NW7%O6=M506ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN
OS:(R=Y%DF=Y%T=40%W=F507%O=M506NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 21/tcp)
HOP RTT      ADDRESS
1   72.92 ms 10.18.0.1
2   72.97 ms 10.10.129.58

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 95.61 seconds
```
<br><br>
We found out 3 open ports : 

1. 80/tcp    open  http    nginx 1.16.1
2. 6498/tcp  open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
3. 65524/tcp open  http    Apache httpd 2.4.43 ((Ubuntu))
<br><br>

### ❓ Question 1  : How many ports are open? 
✅ A : 3

### ❓ Question 2 : What is the version of nginx?
✅ A : 1.16.1

### ❓ Question 3 : What is running on the highest port 
✅ A : Apache

<br>

-----------
-----------
<br>

## 📌 TASK 2 : Compromising the machine
<br>

Let's try to compromise the machine ...

### ❓ Question 1 : Using GoBuster, find flag 1. ?

We will use GuBuster to scan for  directories in this machine . We will use the following <br>
📜 Command : gobuster dir -u IP -w /usr/share/dirb/wordlists/big.txt

```html

===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.129.58
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2023/01/30 20:38:15 Starting gobuster in directory enumeration mode
===============================================================

/hidden               (Status: 301) [Size: 169] [--> http://10.10.129.58/hidden/]

/robots.txt           (Status: 200) [Size: 43]

===============================================================
2023/01/30 20:40:48 Finished
===============================================================
```

we can see an intesting directory which is /hidden .
IF we try to explore it 

Let's try again a scan to the our new /hidden directory . <br>
📜 Command : gobuster dir -u 10.10.129.58/hidden  -w /usr/share/dirb/wordlists/big.txt   >  gobuster_scan2.txt
















