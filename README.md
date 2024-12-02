<h1>Blocking DHCP and SMB Services Using GPO and firewall</h1>
<p>Before configuring the firewall settings, it’s important to verify that DHCP and SMB services are currently working on MS1 server. This ensures you can confirm the effectiveness of the new firewall rules once applied.</p>

<br>
<h3>*Verifying DHCP Service</h3>
<p>1. To verify DHCP service before configuration, I opened command prompt on Windows 11, I typed in <b><i>"ipconfig /release"</i></b> to release the computer's IP address and afterwards typed <b><i>"ipconfig /renew"</i></b> to get a new IP address</p>
<p align="center"><img src="https://i.imgur.com/jH0Yp9Y.png" height="50%" width="50%" alt="image"/>

<h3>*Verifying SMB Access</h3>
<p>1. To Verify SMB Access before configuration, On the Member Server(MS1) I created a new shared folder by clicking on File and Storage services</p>
<p align="center"><img src="https://i.imgur.com/fNlYdur.png" height="50%" width="50%" alt="image"/>

<p>2. On the File and Storage Services > Shares page, I clicked on the Tasks dropdown and selected New Share</p>
<p align="center"><img src="https://i.imgur.com/bFVVlkH.png" height="50%" width="50%" alt="image"/>

<p>3. On the Select the profile for this share, left it at the default (SMB Share - Quick), then clicked NEXT</p>
<p align="center"><img src="https://i.imgur.com/DxliQRN.png" height="50%" width="50%" alt="image"/>

<p>4. On the Select the server and path for this share, Selected C drive and clicked NEXT</p>
<p align="center"><img src="https://i.imgur.com/sDcypni.png" height="50%" width="50%" alt="image"/>

<p>5. On the Specify Share name, I typed in the name, then clicked NEXT</p>
<p align="center"><img src="https://i.imgur.com/YZUtAbg.png" height="50%" width="50%" alt="image"/>

<p>6. On the Configure Share settings, left it at default, then click NEXT</p>
<p align="center"><img src="https://i.imgur.com/w59uZoe.png" height="50%" width="50%" alt="image"/>

<p>7. On the Specify permissions to control access page, I added domain users by clicking on customize permission and gave them full control, then click NEXT</p>
<p align="center"><img src="https://i.imgur.com/fUnrYV0.png" height="50%" width="50%" alt="image"/>

<p>8. On the Confirm Selections page, I clicked CREATE</p>
<p align="center"><img src="https://i.imgur.com/ZL75Ht5.png" height="50%" width="50%" alt="image"/>

<p>9. On the View results page, I clicked Close</p>
<p align="center"><img src="https://i.imgur.com/A7ERLju.png" height="50%" width="50%" alt="image"/>

<p>10. Back on the client computer(windows 10), opened file explorer, typed in \\win-ms1\shared-folder to access the shared folder created on the member server from windows 10</p>
<p align="center"><img src="https://i.imgur.com/MFEgPXr.png" height="50%" width="50%" alt="image"/>

<p>11. And there it is, 'the shared folder' and I also created another folder in it called ‘Test’.</p>
<p align="center"><img src="https://i.imgur.com/9Gr9b4k.png" height="50%" width="50%" alt="image"/>


<h2>Create and Edit the New GPO for Firewall Rules</h2>
<p>1. From the Group Policy Management, created a new GPO and named it "Block DHCP and SMB".</p>
<p align="center"><img src="https://i.imgur.com/tFJW5Fw.png" height="50%" width="50%" alt="image"/>
<p align="center"><img src="https://i.imgur.com/zeaIiQi.png" height="50%" width="50%" alt="image"/>
  
<p>2. Then to edit the newly created GPO, went to this path: <b><i>Computer Configuration → Policies → Windows Settings → Security Settings → Windows Defender Firewall with Advanced Security → Inbound Rules</i></b>. Then right-clicked on Inbound rules and click New rule</p>
<p align="center"><img src="https://i.imgur.com/eiHM6EY.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Creating Rules to Block DHCP Services</h3>
<p>1. On the New Inbound Rule Wizard>Rule Type page, I selected Port, clicked NEXT </p>
<p align="center"><img src="https://i.imgur.com/JyDqeWi.png" height="50%" width="50%" alt="image"/>

<p>2. On the Protocol and Ports page, selected UDP , then typed in 67 and 68 then clicked NEXT (DHCP listens on 67 and 68)</p>
<p align="center"><img src="https://i.imgur.com/oioS5Zi.png" height="50%" width="50%" alt="image"/>

<p>3. On the Action page, selected Block the connection, then clicked NEXT</p>
<p align="center"><img src="https://i.imgur.com/4B5AAab.png" height="50%" width="50%" alt="image"/>

<p>4. On the profile page, the Domain, Private and Public checkboxes is ticked, then click NEXT</p>
<p align="center"><img src="https://i.imgur.com/IBgVdBD.png" height="50%" width="50%" alt="image"/>

<p>5. On the name page, typed in a descriptive name, then clicked FINISH</p>
<p align="center"><img src="https://i.imgur.com/reGmodG.png" height="50%" width="50%" alt="image"/>

<p>6. Back on the Group Policy Management Editor>the Inbound rule, on the right pane, the configured rule is shown</p>
<p align="center"><img src="https://i.imgur.com/0AllHFC.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Creating Rules to block SMB Services</h3>
<p>1. I went through the same path, right-clicked on Inbound rules, clicked New rules, selected Port, then on the protocols and port, selected TCP and input 445 as the port number (Server message block listens on Port 445), then click NEXT</p>
<p align="center"><img src="https://i.imgur.com/IDUDAzl.png" height="50%" width="50%" alt="image"/>

<p>2. On the Action page, selected Block the connection, then clicked NEXT</p>
<p align="center"><img src="https://i.imgur.com/a7lb4Jr.png" height="50%" width="50%" alt="image"/>

<p>3. On the profile page, the Domain, Private and Public checkboxes is ticked, then click NEXT</p>
<p align="center"><img src="https://i.imgur.com/pwIxnVo.png" height="50%" width="50%" alt="image"/>

<p>4. On the name page, typed in a descriptive name, then clicked FINISH</p>
<p align="center"><img src="https://i.imgur.com/xJOGT5J.png" height="50%" width="50%" alt="image"/>

<p>5. Back on the Group Policy Management Editor>the Inbound rule, on the right pane, the configured rule is shown </p>
<p align="center"><img src="https://i.imgur.com/NxVSmHy.png" height="50%" width="50%" alt="image"/>

<br>

<h2>Linking the GPO</h2>
<p>Then I linked the GPO "Block DHCP and SMB"  to the "Servers" OU</p>
<p align="center"><img src="https://i.imgur.com/bIuLi5i.png" height="50%" width="50%" alt="image"/>
<p align="center"><img src="https://i.imgur.com/t7T4wDP.png" height="50%" width="50%" alt="image"/>

<p><b>N.B</b> After all these, a <b><I>"gpupdate /force"</I></b> command is necessary to force this policy</p>
<p align="center"><img src="https://i.imgur.com/ZOi7lMK.png" height="50%" width="50%" alt="image"/>

<br>

<h2>Test the Firewall Rules from the Client Computers</h2>
<h3>*Testing DHCP Access</h3>
<p><b>On WIndows 10</b> Now to test DHCP Access, I opened command prompt on windows 10, typed in <b><i>Ipconfig /release</i></b> and then <b><i>Ipconfig /renew</i></b>. I got an error which says:
<b><i>“An error occurred while renewing interface Ethernet1 : unable to contact your DHCP server : Request has timed out”</i></b></p>
<p align="center"><img src="https://i.imgur.com/BtMIVO4.png" height="50%" width="50%" alt="image"/>                    

<p> <b>On Windows 11</b> - I also opened power shell on windows 11, typed in <b><i>Ipconfig /release</i></b> and then <b><i>Ipconfig /renew</i></b>. I got an error which says:
<b><i>“An error occurred while renewing interface Ethernet1 : unable to contact your DHCP server : Request has timed out”</i></b></p>
<p align="center"><img src="https://i.imgur.com/uSJk8TU.png" height="50%" width="50%" alt="image"/>

<h3>*Test SMB Access</h3>
<p> To test SMB Access, I opened windows 11, I typed in the location path to access the shared folder on the network \\win-ms1\shared-folder and then I got a Network error message, <b><i>“Windows cannot access \\win-ms1\shared-folder”</i></b></p>
<p align="center"><img src="https://i.imgur.com/hULjMnC.png" height="50%" width="50%" alt="image"/>
  
<br>
