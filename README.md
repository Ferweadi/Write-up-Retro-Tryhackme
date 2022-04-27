# Write-up-Retro-Tryhackme
## Premier Write-up français sur le CTF "Retro" de la plateforme TryHackMe

Le CTF "Retro" est disponible sur la plateforme TryHackMe et a la difficulté "hard" (i.e. difficile en français). Nous allons décomposer le Write-Up selon les étapes suivantes :
**1. Enumeration ;**
**2. Exploitation ;**
**3. Escalation de privilège.**
Nous allons devoir trouver les flags sur un serveur web basé sur Windows.

:information_source: MACHINE_IP représente l'IP de la machine "Retro".
:information_source: le signe "$" représente le début d'une commande sur shell.

### 1/ Enumeration

Il faut premièrement énumérer les ports ouverts via Nmap

`$ nmap -Pn -sV MACHINE_IP`

`PORT     STATE SERVICE       VERSION`<br/>
`80/tcp   open  http          Microsoft IIS httpd 10.0`<br/>
`3389/tcp open  ms-wbt-server Microsoft Terminal Services`<br/>
`Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows`<br/>
