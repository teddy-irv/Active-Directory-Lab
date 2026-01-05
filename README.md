# Active-Directory-Lab

<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
This project shows my Windows Active Directory lab environment on a personal computer using VMware that can add & manage users using PowerShell scripts. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b>
- <b>VMware</b>
- <b>Windows Servers 2022</b>
- <b>Windows 11</b>
- <b> Active Directory </b>

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

After logging back on, I created our first admin user through "Active Directory Users and Computers": <br/>
<img src="https://i.imgur.com/gwzxnkf.png" height="80%" width="80%"/>
<br />
<br />

Going back to the homescreen you can see that we are given the option to log in under my domain with a username and password: <br/>
<img src="https://i.imgur.com/2tWV21a.png" height="80%" width="80%"/>
<br />
<br />

We then enter back into the Server Manager dashboard and through the "Add Roles and Features" I enable both Remote Acess and NAT: <br/>
<img src="https://i.imgur.com/sD5rbyx.png" height="80%" width="80%"/>
<br />
<br />

After successfully enabling NAT and going to our DHCP settings in Tools, under our IPv4 connectivity we can enable a scope of addresses to be assigned to any user connecting to our domain. We'll use the example from the original diagram and select the range 172.16.0.100-200: <br/>
<img src="https://i.imgur.com/hkNiXjg.png" height="80%" width="80%"/>
<br />
<br />

By using a script in Powershell we can then bulk add users, while this isn't necessary for current use, for orginzational use a powershell script can simplify adding/removing large quantities of users at once: <br/>
<img src="https://i.imgur.com/FhEOUcP.png" height="80%" width="80%"/>
<br /> Names from text file: <br />
<img src="https://i.imgur.com/WmRvcF2.png" height="80%" width="80%"/>
<br /> Script successfully ran in Powershell: <br />
<img src="https://i.imgur.com/phGzHE0.png" height="80%" width="80%"/>
<br /> New users created from script: <br />
<img src="https://i.imgur.com/UmxkYRD.png" height="80%" width="80%"/>
<br />
<br />

We can now switch back over to the Windows 11 client we created, and as long as the network adapters are correctly setup, you'll notice after entering ipconfig into command prompt we are located under teddysdomain.com. I also test our internet connectivity  by pinging www.google.com, and you can see we receive a response: <br/>
<img src="https://i.imgur.com/ZCheSPm.png****" height="80%" width="80%"/>
<br />
<br />

We'll then change the name of the Windows 11 desktop to match that of our diagrams naming conventions, changing it to Client1: <br/>
<img src="https://i.imgur.com/pWA7tgp.png" height="80%" width="80%"/>
<br />
<br />

Going back to our Windows 2022 Server Manager dashboard, we can see in our DHCP settings that under computers is "Client1" and in the scope we created, the computer has been assigned an address between it: <br/>
<img src="https://i.imgur.com/NZlV3Yj.png" height="80%" width="80%"/>  <br/>
<img src="https://i.imgur.com/gRDzRJU.png" height="80%" width="80%"/>
<br />
<br />

Lastly, now we may go back to our Windows 11 user and see that our computer is now prompted to enter a username and password under our domain: <br/>
<img src="https://i.imgur.com/ypnjtSW.png" height="80%" width="80%"/>
<br />
<br />

After logging on and using command prompt, you can see we have successfully created our user: <br/>
<img src="https://i.imgur.com/iAdS4Iw.png" height="80%" width="80%"/>
<br />
<br />

</p>
