# ICT171
Rishik Miryala (35693179) 
Global IP address: 3.24.44.143
DNS entry: mcserver.xyz
Reference:
Canonical. (2022, March 31). Linux gaming tutorial: Raspberry Pi Minecraft server on Ubuntu Desktop. Ubuntu. https://ubuntu.com/blog/linux-gaming-tutorial-raspberry-pi-minecraft-server-on-ubuntu-desktop


Install Ubuntu and VirtualBox on your computer's operating system, for example, mine is macOS.

Part 1: Domain and EC2 instance.
Sign in to Amazon and navigate to the AWS EC2 Console.
Launch a new Ubuntu 24.04 LTS instance.
Choose:
Instance type: t2.micro.
Key pair: Use or create a .pem file.
Set storage to 20 GB.
Used Namecheap to purchase a domain (mcserver.xyz). https://ap.www.namecheap.com/. 
Link the domain with the AWS EC2 Console by typing the Elastic IP into the domain.

<img width="617" alt="Screenshot 2025-06-09 at 12 19 01 PM" src="https://github.com/user-attachments/assets/f9dc9ce1-55d7-4b43-ac3a-33b3ab6d5feb" />

Part 2: Connect via SSH.
Launch VirtualBox> Ubuntu.
Open terminal, then enter ssh -i /path/to/<.pem file> ubuntu@<EC2_PUBLIC_IP>.
For example, mine is ssh -i ~/Documents/cashorcard.pem ubuntu@3.24.44.143.
This command securely connects your local computer to a remote server hosted on AWS using the ubuntu user account and authenticates with a private key file located at ~/Documents/cashorcard.pem. Once connected, you can run commands on that server as if you were using it directly.

<img width="236" alt="Screenshot 2025-06-09 at 12 20 44 PM" src="https://github.com/user-attachments/assets/25394268-7d73-4e70-87e7-af0b07c7b51c" />

Part 3: Update and Install Java.
In the terminal, following the previous command, type sudo apt update. 
This command updates my package list.
Follow it up with sudo apt install openjdk-17-jdk -y.
This command installs Java 17, which is required to run Minecraft version 1.17+ servers.

Part 4: Create a directory for the server and download it.
Put this into the terminal: mkdir minecraft.
This is so it makes a new folder to keep server files organised.
Then, input cd minecraft.
Enter the folder I just created.

<img width="437" alt="Screenshot 2025-06-09 at 12 23 47 PM" src="https://github.com/user-attachments/assets/ebed56fa-2504-49c8-9da0-e658c3eeb51d" />

wget https://piston-data.mojang.com/v1/objects/<latest_server_jar>/server.jar.
This command downloads the Minecraft server .jar file from Mojang (replace <latest_server_jar> with the actual download link).
The download link can be found at https://www.minecraft.net/en-us/download/server. 

Part 5: Accept the EULA.
In the terminal, type this: echo "eula=true" > eula.txt.
This creates a file named eula.txt and sets the value to true, indicating you agree to Minecraft’s End User License Agreement.

Part 6: Open the Minecraft server port in AWS.
Go back to the AWS console and navigate to security groups.
Edit inbound rules:
Add a rule.
Type: Custom TCP.
Port Range: 25565.
Source: Anywhere (0.0.0.0/0).
Description: Minecraft.

<img width="350" alt="Screenshot 2025-06-09 at 12 25 43 PM" src="https://github.com/user-attachments/assets/f569b3d4-3b53-410f-bfd2-c9b17df2ba2c" />

Part 7:  Start the server.
Paste this into the terminal:  java -Xmx1024M -Xms1024M -jar server.jar nogui.
This code starts the Minecraft server with 1 GB of RAM. The nogui disables the graphical interface (useful on servers).

<img width="499" alt="Screenshot 2025-06-09 at 12 26 58 PM" src="https://github.com/user-attachments/assets/9e34b85b-9f37-4a8b-ab91-d8c7a63048ae" />

Part 8: Join the server from Minecraft.
Open Minecraft. 
Click multiplayer > Add server. 
Enter server name (Can be anything). 
Enter your EC2 public IP (mine is 3.24.44.143) or domain name, for example, mine is mcserver.xyz.
This lets your Minecraft client connect to the remote server you started.

<img width="491" alt="Screenshot 2025-06-09 at 12 28 00 PM" src="https://github.com/user-attachments/assets/6e337607-b3d6-4512-aee8-ac71ba3fc437" />

<img width="575" alt="Screenshot 2025-06-09 at 12 28 13 PM" src="https://github.com/user-attachments/assets/a2af92f0-f3ba-466c-bbc6-3210d7f9ac7c" />

<img width="337" alt="Screenshot 2025-06-09 at 12 28 25 PM" src="https://github.com/user-attachments/assets/984a6770-9f74-4ee7-9389-301a6aa4cb22" />

Part 10: Stop running the server.
Type stop into the terminal.
The server will shut down.
Type exit after.
This is to exit out of the remote server hosted by AWS.

<img width="626" alt="Screenshot 2025-06-09 at 12 29 01 PM" src="https://github.com/user-attachments/assets/0a83a71a-d6a5-4858-9f89-30fcb72ce66d" />


Part 11: To quickly start the server
Open VirtualBox> Ubuntu 
Open terminal and paste ssh -i /home/rishik/Documents/cashorcard.pem ubuntu@3.24.44.143, this command is for example, which is mine.
Then cd minecraft.
To access the file where the server will start.
Type out this command: java -Xmx1024M -Xms1024M -jar server.jar nogui.
This starts the server.












