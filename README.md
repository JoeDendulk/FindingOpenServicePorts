<h1>Finding Open Service Ports</h1>

<h2>Description</h2>
In this lab, I will use Nmap to detect open ports and identify the operating system of targets.
<h2>Tools and Languages Used</h2>

- <b>Linux</b>
- <b>Nmap</b>
- <b>Grep</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Steps Taken:</h2>

<p align="center">
<b>Discovering outward facing open service ports</b>
<br />
<br />
To avoid permission issues, I signed in as root, and opened a terminal.
<img src="https://i.imgur.com/QjX2jRp.png" height="80%" width="80%"/>
<br />
<br />
I entered the following command to perform a port scan of the top 100 common ports of the company's border router Internet facing interface at 203.0.113.1, using the SYN scan method, while identifying the services on open ports and the OS, disable host discovery, and saving the results into a file.
<br />
<b>nmap 203.0.113.1 -F -sS -sV -O -Pn -oN border-scan.nmap</b><br />
<img src="https://i.imgur.com/CxPNQnA.png" height="80%" width="80%"/>
<br />
<br />
Then to show only the open port we run <b>grep open border-scan.nmap</b>
<img src="https://i.imgur.com/0DW6wkw.png" height="80%" width="80%"/>
<br />
<br />
We also find the OS with <b>grep OS border-scan.nmap</b>
<img src="https://i.imgur.com/ROXhR24.png" height="80%" width="80%"/>
</p>
<br />
<br />
<p align="center">
<b>Discover threat vectors from a guest network</b>
<br />
<br />
An improperly configured guest network can expose companies to attacks.
<br />
<br />
Switching to the Guest network, I can run another command <b>dhclient -r && dhclient</b> to release the previously assigned IP address from the internet subnet and obtain a new IP address in the server subnet.
<br />
<br />
From there I can run <b>ip a s eth0</b> to display the IP configuration for the eth0 interface.
<img src="https://i.imgur.com/UncPoI8.png" height="80%" width="80%"/>
<br />
<br />
I used the following command to perform a port scan against the guest network's gateway device: <br /><b>nmap 192.168.16.254 -F -sS -sV -O -oN guest-scan.nmap</b>
<img src="https://i.imgur.com/xNK3qvI.png" height="80%" width="80%"/>
<br />
<br />
The service detected on ports 80, 443, and 8000 is the firewall. These ports can be used to access the firewall's management interface. 
<br />
<br />
Being able to determine the OS of a target may allow an adversary to select a more effective exploit based on OS type and version.
<img src="https://i.imgur.com/3szOAru.png" height="80%" width="80%"/>
<br />
<br />
</p>
