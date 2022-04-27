# Write-up-Retro-Tryhackme
## Premier Write-up français sur le CTF "Retro" de la plateforme TryHackMe

Le CTF "Retro" est disponible sur la plateforme TryHackMe et a la difficulté "hard" (i.e. difficile en français). Nous allons décomposer le Write-Up selon les étapes suivantes :
**1. Enumeration ;**
**2. Exploitation ;**
**3. Escalation de privilège.**
Nous allons devoir trouver les flags sur un serveur web basé sur Windows.

:information_source: MACHINE_IP représente l'IP de la machine "Retro".
:information_source: le signe "$" représente le début d'une commande sur shell.

*********************

### 1/ Enumeration

Il faut premièrement énumérer les ports ouverts via Nmap

`$ nmap -Pn -sV MACHINE_IP`

`PORT     STATE SERVICE       VERSION`<br/>
`80/tcp   open  http          Microsoft IIS httpd 10.0`<br/>
`3389/tcp open  ms-wbt-server Microsoft Terminal Services`<br/>
`Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows`<br/>

Deux ports sont ouverts, le port 80 et 3389. Concentrons-nous en premier sur le serveur web (port 80), voici la page principale : 

![Capturewriteupretro](https://user-images.githubusercontent.com/67973590/165582217-37554dc4-7154-4c61-ac39-b0c48fe8c3c5.PNG)

Nous allons à présent utiliser Gobuster (Dirsearch et Dirbuster fonctionnent également) afin de trouver les autres pages : 

`$ gobuster dir -u http://MACHINE_IP -w /usr/share/dirb/wordlists/big.txt`<br/>
`===============================================================`<br/>
`Gobuster v3.0.1`<br/>
`by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)`<br/>
`===============================================================`<br/>
`[+] Url:            http://10.10.207.134`<br/>
`[+] Threads:        10`<br/>
`[+] Wordlist:       /usr/share/dirb/wordlists/big.txt`<br/>
`[+] Status codes:   200,204,301,302,307,401,403`<br/>
`[+] User Agent:     gobuster/3.0.1`<br/>
`[+] Timeout:        10s`<br/>
`===============================================================`<br/>
`2021/04/07 09:01:21 Starting gobuster`<br/>
`===============================================================`<br/>                                                   
`/retro (Status: 301)`<br/>
`===============================================================`<br/>
`2021/04/07 09:03:43 Finished`<br/>                                                                              
`===============================================================`<br/> 
