<h1>Blocking DHCP and SMB Services Using GPO and firewall</h1>
<p>Before configuring the firewall settings, it’s important to verify that DHCP and SMB services are currently working on MS1 server. This ensures you can confirm the effectiveness of the new firewall rules once applied.</p>

<br>
<h3>*Verifying DHCP Service</h3>
<p>1. To verify DHCP service before configuration, I opened command prompt on Windows 11, I typed in <b><i>"ipconfig /release"</i></b> to release the computer's IP address and afterwards typed <b><i>"ipconfig /renew"</i></b> to get a new IP address</p>
<p align="center"><img src="https://i.imgur.com/jH0Yp9Y.png" height="50%" width="50%" alt="image"/>

<h3>*Verify SMB Access</h3>
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



  
<p align="center"><img src="" height="50%" width="50%" alt="image"/>
