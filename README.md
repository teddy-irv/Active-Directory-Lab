# Active-Directory-Lab

<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
This project shows how I built a Windows Active Directory lab environment on a personal computer using VMware and then add & manage users using PowerShell scripts. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b>
- <b>VMware</b>
- <b>Windows Servers 2022</b>
- <b>Windows 11</b>
- <b> Active Directory </b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Windows Servers 2022</b>

<h2>Goal:</h2>
<b> 1. Create a Domain Controller hosting a Windows Server with 2 network adapters, one external to connect to the internet, and one internal for other virtual machines to connect to. <br />
<br /> <b> 2. A client virtual machine hosting Windows 11 that will connect to the domain using one of our domain accounts we will create. <br />
<br /> <b> 3. Create a domain using Active Directory, for this project it will be "teddysdomain.com" <br />
<br /> <b> 4. Configure NAT & Routing so clients on the private network can receive internet through Domain Controller. <br />
<br /> <b> 5. Set DHCP so that when connecting to the domain, our client will automatically receive an IP address within its scope. <br />
<img src="https://i.imgur.com/Hwo6TYx.png" height="80%" width="80%"/>

<h2>Walk-through:</h2>

I installed VMware and downloaded the ISO files online for both Windows 11 and Windows Server 2022. After VMware finished installing, select create new Virtual Machine and do this with both ISO files: <br/>
<img src="https://i.imgur.com/f45sZoe.png" height="80%" width="80%"/>
<br />
<br />

Afterwards, on the left side of your screen you should see both the Windows Client and Windows Server Virtual machine. I've created a folder for mine under my name: <br/>
<img src="https://i.imgur.com/3fU83V2.png" height="80%" width="80%"/>
<br />
<br />

It's important to configure both the server and the clients network adapter settings otherwise they will not be able to communicate with eachother. On the windows server, set the first network adapter to NAT and the second to VMnet2. The first adapter will be used to connect to the internet, while the second will be used to communicated internally with other Virtual Machines, providing them access. For the client, you only need 1 adapter that configured to VMnet2: <br/>
<img src="https://i.imgur.com/HCdpZKT.png" height="80%" width="80%"/>
<br />
<br />

After Windows 2022 server ISO boots up, go to Network Connection settings and you'll notice two network adapters, one for your external network and one for your internal, configure the internal to match our previous diagram as follows: <br/>
<img src="https://i.imgur.com/mCl8le0.png" height="80%" width="80%"/>
<br />
<br />


Use the Add Roles and Features in Windows Server manager to download Active Directory Domain Services, afterwards I named my domain "teddysdomain.com": <br/>
<img src="https://i.imgur.com/a9Ipz2t.png" height="80%" width="80%"/>
<br />
<br />

Restarting the computer after shows that our domain was succesfully created: <br/>
<img src="https://i.imgur.com/bU1onjQ.png" height="80%" width="80%"/>
<br />
<br />

After logging back on, I created our first admin user through "Active Directory Users and Computers" <br/>
<img src="https://i.imgur.com/gwzxnkf.png" height="80%" width="80%"/>
<br />
<br />


</p>
