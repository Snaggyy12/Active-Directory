# Active-Directory
Creating Home Lab Running Active Directory
# Purpose 
The purpose of this Active Directory home lab is to simulate a corporate IT environment and gain hands-on experience managing and troubleshooting systems within a controlled virtual network.
This lab replicates real-world administrative responsibilities, including network configuration, user management, automation, and system security to strengthen practical IT and systems administration skills.

By building this lab, it is aimed to:

• Design and deploy a virtualized network using industry-standard tools.

• Implement Active Directory services to manage users, groups, and policies.

• Practice automation with PowerShell to streamline administrative tasks.

• Understand how network routing, DNS, and DHCP work together in a Windows domain.

• Develop critical troubleshooting and problem-solving skills in an enterprise-style setup.

# Skills Acquired
• Virtualization & Networking – Deployed multiple virtual machines using VirtualBox and configured internal/external networks to simulate an enterprise topology.

• Active Directory Management – Installed and configured Windows Server 2019 as a Domain Controller, created and managed users, groups, and organizational units.

• Automation with PowerShell – Automated user account creation and administrative tasks through scripting, reducing manual workload.

• User Access Control – Configured users with different privileges, applying least-privilege principles and security best practices.

• Network Design & Configuration – Designed a functional network with DHCP, DNS, and remote services for centralized management.

• Traffic Redirection – Configured routing to divert internet traffic from one domain controller to a private network for secure internal access.

• Troubleshooting & Maintenance – Diagnosed and resolved connectivity, authentication, and configuration issues across servers and clients.

# Tools Used
• VirtualBox – Virtualization platform for creating isolated network environments.

• Windows Server 2019 – Core infrastructure for Active Directory, DNS, and DHCP services.

• Windows 10 Pro – Client machines joined to the domain for user testing.

• Active Directory – Centralized management of users, groups, and network resources.

• PowerShell – Scripting and automation of administrative tasks.

• DHCP & DNS – Automated IP address assignment and name resolution within the domain.

• Remote Services – Managed systems and performed administrative tasks remotely.

• Command Prompt – Used for diagnostics, scripting, and troubleshooting network or domain issues.
# Screenshots and Explanation
![Active Directory](https://github.com/user-attachments/assets/0d24be1d-ddda-4db4-8710-661224848dc2)
The diagram illustrates the structure of the Active Directory home lab, showing how different components such as domain controllers, client machines, and network services (DNS, DHCP, etc.) are connected within the virtual network. It visually represents how the simulated corporate environment is organized and how devices communicate within the domain
# Windows 2019 Server Setup
Before setting up the Domain Controller, I first created a new virtual machine in VirtualBox and used the Windows Server 2019 ISO file. I made sure to tick the option “Skip Unattended Installation” so that I could go through the setup manually instead of it being done automatically. I also adjusted the hardware settings by giving the VM around 3GB of RAM and a few processors to make sure it would run smoothly during the installation and when configuring Active Directory later on.

Although I don’t have a screenshot from my setup, this image shows a similar step I completed when creating my virtual machine. At this stage, I chose to create a new virtual hard disk and used the VDI (VirtualBox Disk Image) format, which is standard for VirtualBox. I set the size to around 50GB to make sure there was enough space for Windows Server and the Active Directory roles later on. Once I was happy with the settings, I clicked Finish to finalise the virtual machine setup.
<img width="778" height="478" alt="image" src="https://github.com/user-attachments/assets/2c5bfb46-cebd-409f-821c-7fe9b69764a3" />

This will enable us to drag and drop items from the physical machine to the virtual machine and escape the virtual machine without having to use the host key.

<img width="778" height="478" alt="image" src="https://github.com/user-attachments/assets/fd032781-2fac-4b5a-b0a3-8abad0ae35ce" />

This is the part where you are able to adjust the settings of the windows 2019 server to be able to withstand the processes without any performance issues which will hinder with our process of creating our Domain Controller.
<img width="778" height="478" alt="image" src="https://github.com/user-attachments/assets/551310f1-3bec-4cd7-a3c1-26c6d11b6bda" />
<img width="778" height="478" alt="image" src="https://github.com/user-attachments/assets/86583857-e4a8-4e32-8979-17b1bd5b1e69" />

Here, the network adapters for the virtual machine have been configured in preparation for setting up the Domain Controller. Adapter 1 is set to NAT, which allows the virtual machine to access the Internet through the host computer’s network connection. Adapter 2 is configured as an internal network, which will later be used for communication between the Domain Controller and other virtual machines within the same environment. Once these settings are applied, the virtual machine is ready to start the Active Directory setup. This is also part of the process that is shown from the very first screenshot with the diagram on what part of the process we are working on.

<img width="1026" height="854" alt="image" src="https://github.com/user-attachments/assets/93180f16-22c4-4389-8d5b-8ccc4637c925" />

For my Windows Server 2019 VM, I set up the network adapters to prepare for making it a Domain Controller. I gave the internal adapter a static IP and set the DNS to 127.0.0.1 so the server can handle DNS requests itself.
I renamed the adapters to “Home Internet” and “Internal Internet” to make it easy to tell which is for the internet and which is for the internal network. This helps avoid confusion since the server will manage different tasks on each network.
This setup keeps the internal domain separate from the internet and follows the project diagram, making it ready for installing Active Directory.

# Active Directory Creation

To start installing Active Directory Domain Services using Server Manager, I first went to “Add Roles and Features” and added the Active Directory role. I selected the server that would become the Domain Controller, chose Active Directory Domain Services, and then clicked Next through the prompts until the installation of AD DS was complete.

<img width="1026" height="854" alt="image" src="https://github.com/user-attachments/assets/414c1ce0-47dc-445f-900a-b5df3b9ed57b" />
<img width="858" height="738" alt="image" src="https://github.com/user-attachments/assets/d5791727-49cd-4999-b797-8c21e64a45f5" />
<img width="1043" height="854" alt="image" src="https://github.com/user-attachments/assets/a029f0c1-fff1-4539-9a1a-c13b578a8dcf" />
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/0e7eca73-287d-424b-aed9-a3710687bd6c" />

# Deployment of a Domain for Active Directory

After installing AD DS, I had to turn the server into a Domain Controller. I went through the setup wizard until I reached the Domain Controller options, set a password for recovery, and since this was the first Domain Controller, I created a new forest to make it the root. Once everything was configured, the server restarted to finish the setup.

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/5a62c239-cbd9-4a8f-94e1-fa2754073ada" />
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/973852c6-35a4-479b-83fe-e96da4d1947b" />

After the system restart I was then able to log into the Domain Controller administrator user that we have created, and seen that on our server manager dashboard that it is configured.

<img width="956" height="854" alt="image" src="https://github.com/user-attachments/assets/21d6e4f4-b556-49aa-a960-d2ffe8801e60" />

Next, I added another user for administrative purposes—a second Domain Admin account. I opened Active Directory Users and Computers from the Start menu, created a new Organizational Unit under mydomain.com, and named it _ADMINS to keep all admin accounts organised

<img width="961" height="854" alt="image" src="https://github.com/user-attachments/assets/7f2270b8-1178-48b8-b2a7-f334e3fd6f01" />
<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/cbaeea6c-1d36-4926-a0ea-1aab4064a81a" />
<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/440d3ca1-d2fd-4acb-aa40-ad8b98190e1a" />

Here, I created a Domain admin account and then logged into that account to ensure it was working. Because it is a lab environment, things like the password never expiring are tolerated. In a production environment, this would not be checked.

# Installing RAS/NAT

The next step was to set up RAS/NAT services on the Domain Controller so the client machine (Windows 10) could access the internet while staying on a private network. I added this by going to Add Roles and Features and selecting Remote Access, making sure to check Routing before completing the installation. Once it was installed, I started configuring the service to manage internet traffic between the Domain Controller and the client.

<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/b0f79ce3-6a2c-4970-af18-5f56df2fd37e" />
<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/621ef1e8-8e75-460f-8a5a-5aba343f136d" />
<img width="963" height="854" alt="image" src="https://github.com/user-attachments/assets/f7e6a60c-24e5-498e-8dcc-789256bfecf5" />

# Configuring RAS with NAT

In the configuration tab, I selected the NAT option so that all clients could access the internet through the Domain Controller’s IP address. For this step, on the Windows 10 Pro client, I chose Adapter 1 because it matches my Active Directory diagram and is the adapter connected to the internet. I’ll be showing a screenshot of this setup later to illustrate the configuration.

<img width="962" height="854" alt="image" src="https://github.com/user-attachments/assets/58c36ed4-1b42-447e-b3a0-ea9c68fd9ea2" />
<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/c7c7082c-f7bb-41f8-95b3-57093fc7b6fd" />
<img width="962" height="854" alt="image" src="https://github.com/user-attachments/assets/23af5d01-1469-47eb-b28f-575e1a844c12" />

# Installing DHCP

The next step was to install DHCP this will be used to automatically assign our client machine an ip address.

<img width="962" height="854" alt="image" src="https://github.com/user-attachments/assets/e0afadb1-1931-45a8-af25-358320bbaa2e" />
<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/b22af0e7-52f6-4d02-ab7b-7c017df9939f" />

# DHCP Configurations

Next, I worked on configuring DHCP. I opened the DHCP console and, as shown in the screenshot, I right-clicked on IPv4 to add a new scope. For the scope name, I entered 172.16.0.100-200 to define the range of IP addresses that the server can assign to clients.

<img width="1001" height="854" alt="image" src="https://github.com/user-attachments/assets/1ae03ea7-dbcb-4a56-82ed-55f2bcc0344d" />
<img width="961" height="854" alt="image" src="https://github.com/user-attachments/assets/001941d6-752a-49d9-97e4-4d7940b5961b" />
<img width="961" height="854" alt="image" src="https://github.com/user-attachments/assets/815e36b4-685d-4d9f-b694-ba23a726abd5" />

Next, I configured the IP address range for the DHCP server. I set the start IP to 172.16.0.100 and the end IP to 172.16.0.200, which defines the pool of addresses the server can assign to clients. I set the prefix length to 24, which corresponds to a subnet mask of 255.255.255.0. This means all devices in this range are on the same network, allowing them to communicate with each other efficiently while staying organized within the subnet.

<img width="958" height="854" alt="image" src="https://github.com/user-attachments/assets/4aea9e9f-0c01-4519-93a4-03df03163c86" />

In this step, I set the DHCP lease duration to 8 days. This means that any IP address the server assigns to a client will remain valid for 8 days before the client needs to renew it. Setting a lease period helps manage IP addresses efficiently, ensuring devices keep the same address for a reasonable time while allowing unused addresses to be reassigned if needed.

<img width="959" height="854" alt="image" src="https://github.com/user-attachments/assets/f9d0864f-5d80-4173-a4bb-810f3c24a7c0" />

# DHCP gateway

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/7fa53ae1-ba0f-46c4-afa9-d165aaa9de42" />
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/8c2a6711-230b-41fe-a1cf-e7e73bb1aeb2" />

In the next part, I added the IP address for the router that clients will use to access the network, which is set to 172.16.0.1. Immediately after, I configured the domain name and DNS server for the DHCP scope. I entered the parent domain as mydomain.com and set the DNS server IP to the same address, ensuring clients would be able to resolve domain names correctly

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/6f167650-bb28-43fa-b575-e43ae8333977" />

After finishing the DHCP configuration, I noticed that both IPv4 and IPv6 have a green check mark in the DHCP window. This indicates that the DHCP server is running properly and is authorized to assign IP addresses for both protocols on the network. The green tick confirms that the server is functioning and ready to manage client IP assignments.

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/07c02b5a-c82c-46ca-9921-194036d6e4f9" />

The Internet Explorer Enhanced Security Configuration (IE ESC) was turned off for both Administrators and Users. This means that Internet Explorer will not apply its strict security restrictions on this server, making it easier to browse websites without constant security warnings. In a lab environment, this is convenient for testing, but in a production environment, leaving IE ESC on helps protect the server from potentially harmful websites.

# Script for testing with different users
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/e0cba4eb-90cd-4499-b916-8710f99f2108" />
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/2d7a8072-9ebf-4aa4-b0ab-6aaf47f91ee4" />
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/7444535c-2d6f-4d9b-9838-f47b29496540" />

After that, I found and used a script to bulk-generate user accounts for testing. The script created multiple test users quickly (so I didn’t have to add them one-by-one), which made it easy to simulate real-world activity and test permissions and group policies. I ran the script from the Domain Controller with the appropriate admin rights and saved screenshots showing the script and the accounts it produced. Since this is a lab, using an automated script was fine for speed, but in a production environment I’d review the script carefully and follow stricter security practices before running anything like this.

# Windows 10 Pro Client 

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/383bd4fd-97ff-4b48-bfea-1bd34c43df5b" />

For the other ISO, I connected its network adapter to the internal network while the Domain Controller ISO was running. This is crucial because it allows the client machine to communicate directly with the Domain Controller over the private network. Without this, the client wouldn’t be able to join the domain, receive DHCP assignments, or access domain services, which are essential for testing and managing the Active Directory environment

<img width="1026" height="854" alt="image" src="https://github.com/user-attachments/assets/4c8be271-2366-43d2-ab28-eb7ca89e087d" />

Using Windows Pro for the client machine is better for testing because it includes features that aren’t available in Home editions, like joining a domain, Group Policy support, and Remote Desktop hosting. These features are essential when working with a Domain Controller and Active Directory, allowing the client to fully interact with the domain, receive policies, and test administrative configurations as it would in a real-world environment.

<img width="1026" height="849" alt="image" src="https://github.com/user-attachments/assets/cf843497-6fe4-4c2a-ac15-cb445827fa52" />
<img width="1026" height="849" alt="image" src="https://github.com/user-attachments/assets/c798c644-91a8-40b5-8777-4148f8cff3df" />

Here, I logged into the client machine using one of the test user accounts to check if the DHCP was working correctly. I saw that the client automatically received an IP address within the range I set in the DHCP scope, which shows that it’s configured properly. On the client, I ran ipconfig /all in Command Prompt and noticed that the DHCP server address was the same as the default gateway. The DNS domain name also showed up correctly, meaning both DNS and DHCP are working together as expected.

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/61f0b173-3517-46c8-99e2-27dae090487a" />
<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/9ee78f80-295f-4145-83a0-557d5653f14b" />

After that, I went back to the Domain Controller to check the DHCP settings. Under IPv4 → Address Leases, I could see the client machine listed, showing that it had successfully received an IP address from the server. I also opened Active Directory Users and Computers and looked under mydomain.com → Computers, where I found the test virtual machine listed by its name. This confirmed that the client was properly connected to the domain and communicating with the Domain Controller

<img width="1026" height="848" alt="image" src="https://github.com/user-attachments/assets/fabef4c1-80e1-407b-b217-4996b9cf7ec2" />

Finally, I went back to the client machine, logged out, and then signed in using one of the user accounts that was created with the script. This was to test if the domain login worked properly for other users. In the final screenshot, you can see that the login was successful, confirming that the Domain Controller and Active Directory setup are functioning correctly


# Reflection

Building this lab helped me connect theory with practice. I learned how different network services rely on one another and how automation can make system management much easier. Although it took time to troubleshoot certain issues, solving them deepened my understanding of how Active Directory operates in real-world environments.

This project gave me confidence in managing servers, networks, and users, which are skills that are directly transferable to professional system administration roles.
