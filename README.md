# Write-up-Retro-Tryhackme
## Premier Write-up français sur le CTF "Retro" de la plateforme TryHackMe

Le CTF "Retro" est disponible sur la plateforme TryHackMe et a la difficulté "hard" (i.e. difficile en français). Nous allons décomposer le Write-Up selon les étapes suivantes :
**1. Enumeration ;**
**2. Exploitation ;**
**3. Escalation de privilège.**
Nous allons devoir trouver les flags sur un serveur web basé sur Windows.

:information_source: MACHINE_IP représente l'IP de la machine "Retro".<br/>
:information_source: le signe "$" représente le début d'une commande sur shell.

*********************

### 1/ Enumeration

Il faut premièrement énumérer les ports ouverts via Nmap
```
$ nmap -Pn -sV MACHINE_IP

PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
3389/tcp open  ms-wbt-server Microsoft Terminal Services
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```
Deux ports sont ouverts, le port 80 et 3389. Concentrons-nous en premier sur le serveur web (port 80), voici la page principale : 

![Capturewriteupretro](https://user-images.githubusercontent.com/67973590/165582217-37554dc4-7154-4c61-ac39-b0c48fe8c3c5.PNG)

Nous allons à présent utiliser Gobuster (Dirsearch et Dirbuster fonctionnent également) afin de trouver les autres pages : 
```
$ gobuster dir -u http://MACHINE_IP -w /usr/share/dirb/wordlists/big.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.207.13
[+] Threads:        10
[+] Wordlist:       /usr/share/dirb/wordlists/big.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2021/04/07 09:01:21 Starting gobuster
===============================================================                                                   
/retro (Status: 301)
===============================================================
2021/04/07 09:03:43 Finished                                                                             
===============================================================
```
Nous avons trouvé la page `/retro` après l'énumération. Voici à quoi ressemble la page :

![Captureretrowtf](https://user-images.githubusercontent.com/67973590/165585365-c1945d37-e01f-412b-86ca-10eb2e5242eb.PNG)

On remarque que les articles du site sont tous écrits par **Wade**, en allant voir son profil, il est possible de voir ses derniers posts. En allant sur son post *"Ready Player One"* on aperçoit un commentaire écrit par lui-même contenant ce message : 


![Capturecommentretro](https://user-images.githubusercontent.com/67973590/165585514-92b93c05-8ec9-4d77-869e-9aa111f8fe77.PNG)
