Write-up for home lab kerberoasting project
Author: Tim Pricer

3 VMs Were used for this project (via VirtualBox)
Windows Server 2025 as the Domain Controller (w/ AD Domain Services)
Windows 11 as the Management Client
Kali linux as the Attacker OS

All 3 were spun up from ISO images available publicly or on Microsoft Azure

Note: Some steps will not be used in the kerberoasting experiment, but are rather to create a fully flushed out AD for future labs

CREATING ENVIRONMENT:
I added an "Employees" OU
I added a "Service Accounts" OU


I added user "Jack Smith" to the domain. He will act as our compromised account. Added to Employees OU.
I added user "Alice Brown" to the domain. Added to Employees OU.
I added user "Jane Johnson" to the domain. Added to Employees OU.
I added user "Admin" to the domain to act as a secured administrator. It is added to Domain Administrators.
I added user "svc-http" to act as the http service account. It has a weak password. Added to Service Accounts OU
