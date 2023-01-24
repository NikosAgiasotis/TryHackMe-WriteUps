<h1>⭕ TryHackMe RootMe CTF </h1>

<h3> 📃 Task 1 :  Deploy the machine </h3>

Just start the machine 

<h3> 📃 Task 2 :  Reconnaissance </h3>

Let's scan the machine with nmap and check out for open ports. <br>

![Scan output](https://i.imgur.com/FiK2Igf.png)

> Command : nmap -sV IP

*-sV: Probe open ports to determine service/version info* <br> 

🏷️ Q1 : Scan the machine, how many ports are open? <br>
A  : 2

🏷️ Q2 : What version of Apache is running ? <br>
A  : 2.4.29

🏷️ Q3 : What service is running on port 22 ? <br>
A  : ssh

----------

🔖 Q4 : Find directories on the web server using the GoBuster tool. <br>
A  : -

🔭 At this point we should use Gobuster to find all directories for this web application . 
> Command : gobuster dir -u 10.10.242.72 -w /usr/share/dirb/wordlists/common.txt

![Scan output](https://i.imgur.com/sohUnEq.png)

As we can see we have 2 intersting directories in our web app which is :
/panel
/uploads

🔖 Q5 : What is the hidden directory ? <br>
A  : /panel/

<h3> 📃 Task 3 :  Getting a shell </h3>

<h3> 📃 Task 4 :  Privilege escalation </h3>

