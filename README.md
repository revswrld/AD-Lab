<div style="max-width: 900px; margin: auto; line-height: 1.6;">

<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
I will be using Oracle VirtualBox to create a functional Active Directory lab. This demonstrates setting up a domain controller, configuring network adapters, and installing essential services like DHCP. I will also demonstrate creating users, adding users to groups, and more.
<br />

<h2>Environments Used </h2>

- <b>Windows Server 2025</b>
- <b>Windows 10 Pro</b>

<h2>Lab walk-through:</h2>
<br/>

<p align="center">
Install Windows Server 2025 on the domain controller VM. <br/> Ensure the VM has two network interfaces, one NAT interface to access the internet, and one internal interface for the local devices to connect to. <br/>
<img src="https://i.imgur.com/RJRTA0o.png" height="50%" width="50%" alt="Installing Windows Server"/>
<br />
<br />
Once the OS has finished installing, open Network Connections in the Control Panel. <br/>There should be two connections. Check the status of these connections to determine which one is the NAT interface and which is the internal interface. The NAT interface will have incoming and outgoing traffic, while the internal interface will only have outgoing or no traffic yet. Name them accordingly.
<br/>
<img src="https://i.imgur.com/TUuVFHT.png" height="50%" width="50%" alt="Renaming Network Connections"/>
<br />
<br />
On the internal network connection, configure the IPv4 properties to match your IP scheme.
<br/>
<img src="https://i.imgur.com/uEw5ONA.png" height="50%" width="50%" alt="Setting DC IP address"/>
<br />
<br />
In the settings, rename the PC to DC01, or whatever name you want your domain controller to go by. It will want to restart after.
<br/>
<img src="https://i.imgur.com/3wQfJUT.pngg" height="50%" width="50%" alt="Renaming PC to DC01"/>
<br />
<br />
Open the Server Manager and click <b>Add roles and features</b>. Follow the steps to install Active Directory Domain Services.
<br/>
<img src="https://i.imgur.com/yvRmXlD.png" height="50%" width="50%" alt="Installing ADDS"/>
<br />
<br />
Once ADDS is finished installing, click the flag with a warning icon in Server Manager. Click <b>"Promote this server to a domain controller"</b>.
<br/>
<img src="https://i.imgur.com/awsW7Lv.png" height="50%" width="50%" alt="Promoting server to a domain controller"/>
<br />
<br />
Add a new forest with whatever domain name you want. 
<br/>
<img src="https://i.imgur.com/SiWMzmi.png" height="50%" width="50%" alt="Creating domain"/>
<br />
<br />
Follow any instructions to complete the creation of the domain and the promotion of the server to a domain controller. Leave everything default.
<br/>
<img src="https://i.imgur.com/3zeUBb7.png" height="50%" width="50%" alt="Finish promoting server to a domain controller"/>
<br />
<br />
Log into your domain through the Administrator account, then search <b>"Active Directory Users and Computers"</b> in the search bar. Create an Organizational Unit called "Admins".
<br/>
<img src="https://i.imgur.com/fe2gI5P.png" height="50%" width="50%" alt="Creating an organizational unit in Active Directory"/>
<br />
<br />
Create a user inside of the Admins OU and name it after yourself. This will be your own administrator account. Ensure that your password does not have to be reset before the next sign-in and never expires. When finished, right-click the user and select "Add to a group...". Type "Domain Admins" and check names. Hit OK.
<br/>
<img src="https://i.imgur.com/CgYQGXf.png" height="50%" width="50%" alt="Creating a user in Active Directory"/>
<br />
<br />
Log into your new user account. 
<br/>
<img src="https://i.imgur.com/WjF6DeH.png" height="50%" width="50%" alt="Log into user account"/>
<br />
<br />
In Server Manager, click <b>"Add roles and features"</b>. This time, install the "Remote Access" role. On the "Role Services" page, select Routing. This will check both Routing and DirectAccess and VPN (RAS). Leave everything else default and install.
<br/>
<img src="https://i.imgur.com/ocdJrCe.png" height="50%" width="50%" alt="Installing RAS and NAT"/>
<br />
<br />
In Server Manager, click Tools > Routing and Remote Access. Right-click the machine name and click "Configure and Enable..." Select "Network address translation (NAT)". If no interfaces show up on the next page, close Routing and Remote Access and reopen it through Server Manager. It should look like the image. Select the NAT interface you labeled earlier and finish. This will allow the internal devices to connect to the internet using 1 IP address.
<br/>
<img src="https://i.imgur.com/mV5jWqY.png" height="50%" width="50%" alt="Configuring NAT settings"/>
<br />
<br />
In Server Manager, click <b>"Add roles and features"</b>. Install the "DHCP Server" role.
<br/>
<img src="https://i.imgur.com/zH1TbQc.png" height="50%" width="50%" alt="Installing DHCP to the domain controller"/>
<br />
<br />
In Server Manager, click Tools > DHCP. Right-click IPv4 under your domain and add a new scope.
<br/>
<img src="https://i.imgur.com/NSCTJNd.png" height="50%" width="50%" alt="Add a DHCP scope"/>
<br />
<br />
When prompted to configure DHCP options now, say yes. Add your domain controller's IP address where it asks for a router IP. Click next until you finish. In DHCP, right-click your domain controller and hit "authorize".
<br/>
<img src="https://i.imgur.com/xsZUuzZ.png" height="50%" width="50%" alt="Configure DHCP options"/>
<br />
<br />
Go back to Active Directory Users and Computers and create a new user on your own. Ensure that your password does not have to be reset before the next sign-in and never expires.
<br/>
<img src="https://i.imgur.com/5ejTedn.png" height="50%" width="50%" alt="Add a new user"/>
<br />
<br />
Install Windows 10 Pro on the workstation VM. It should only have one network interface, which should be internal. If done correctly, you will already have an internet connection when you first turn on the VM.
<br/>
<img src="https://i.imgur.com/1ou6msu.png" height="50%" width="50%" alt="Install Windows 10 Pro"/>
<br />
<br />
On the workstation VM, open command prompt and test to see if you can ping the domain controller. Also ping a website to test if you have an internet connection. If everything is configured correctly, you will get replies from both pings.
<br/>
<img src="https://i.imgur.com/56C2rWF.png" height="50%" width="50%" alt="Test connection to the DC and internet"/>
<br />
<br />
On the workstation VM, open settings and go to about. Instead of renaming the PC normally, scroll down until you see "Rename this PC (advanced)". A System Properties window will pop up. Click "Change" on the "Computer Name" tab.
<br/>
<img src="https://i.imgur.com/GzRJ3pa.png" height="50%" width="50%" alt="Join the domain and rename PC"/>
<br />
<br />
Type the new computer name in the top bar, and select "Domain". Enter your domain name and hit OK. This means that you will join the domain and rename the VM simultaneously. Enter a user's credentials, such as your admin account's or your example user's. When finished, restart the machine.
<br/>
<img src="https://i.imgur.com/NT6YR7l.png" height="50%" width="50%" alt="Join the domain and rename PC"/>
<br />
<br />
When you sign into the VM, click "Other User" to sign into a domain account. Use your admin account or example user's credentials to sign in.
<br/>
<img src="https://i.imgur.com/K9SBYV3.png" height="50%" width="50%" alt="Log into the domain on the workstation VM"/>
<br />
</p>

<h2>Summary</h2>
In this lab, you created a functional Microsoft Active Directory domain controller with virtualization. You set up a domain controller, configured network adapters, installed and configured services such as DHCP, created users, added users to groups, and joined a workstation to the domain.

</div>
