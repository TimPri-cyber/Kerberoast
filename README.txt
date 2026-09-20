Write-up for home lab kerberoasting project
Author: Tim Pricer

Note: Some steps will not be used in the kerberoasting experiment, but are rather to create a fully flushed out environment for future labs

3 VMs Were used for this project (via VirtualBox)
Windows Server 2025 as the Domain Controller (w/ AD Domain Services)
Windows 11 as the Management Client
Kali linux as the Attacker OS

All 3 were spun up from ISO images available publicly or on Microsoft Azure



CREATING ENVIRONMENT:
I added an "Employees" OU
I added a "Service Accounts" OU


I added user "Jack Smith" to the domain. He will act as our compromised account. Added to Employees OU.
I added user "Alice Brown" to the domain. Added to Employees OU.
I added user "Jane Johnson" to the domain. Added to Employees OU.
I added user "Admin" to the domain to act as a secured administrator. It is added to Domain Administrators.
I added user "svc-http" to act as the http service account. It has a weak password. Added to Service Accounts OU. 

No actual server is created for svc-http for the sake of simplicity

EXPLOIT:
I assumed the attacker would have the following information:
-Credentials for Jack Smith's employee account
-The name of the target domain
-The IP address of the server
-Access to company VPN credentials (to get access to the same network as the DC). This is simulated by having the Kali and Windows server VMs on the same network

I booted up the Kali Linux attackers VM
Used impacket scripts from Kali's tools

Ran into issues with the hypervisor isolating the two VMs, preventing easy communication between them
Used impacket-GetUserSPNs
-encountered "No entries found", fixed by assigning SPN the the svc-http account
-encountered "Clock skew too great", fixed by running rdate on the same like as impacket

Hash successfully aquired from the DC, used echo to write to test.hash
Used John The Ripper on the hashed file, decrypted the password
Used password to gain access to the services account

