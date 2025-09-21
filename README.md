<p align="center">
<img src="https://i.imgur.com/CtGfsq8.png" alt="osTicket logo"/>
</p>

<h1>Learning DNS in Azure</h1>
In this lab, we will experiment with DNS using the Active Directory Lab. This lab will help us have a better understanding of DNS.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- DNS Manager
- Powershell

<h2>Operating Systems Used</h2>

- Windows Server (22H2)
- Windows 10 Pro (22H2)

<h2>List of Prerequisites</h2>

- Active Directory Lab (Client & Server)
- Client Machine joined the Domain
<br />

<h3>A-Record exercise</h3>
<p>
  1. Connect/log into DC-1 as your Domain Admin account (mydomain.com\jane_admin)

  2. Connect/log into Client-1 as an admin (mydomain\jane_admin)
  
  3. From Client-1, try to ping “mainframe” (Random Name) from Powershell. Notice that it fails.

  4. Use Nslookup “mainframe”, notice that it fails (no DNS record).
</p>
<p>
  <img src="https://i.imgur.com/hEK8bjk.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  When the computer tries to interact with any host’s name on the Network, whether it's browsing to it or trying to ping it, the computer will first check its Local DNS cache,
  
  - If it’s not found, then it will check its Local Host File, 
  
  - If it’s not found there, then it will check its DNS Server as a last resort.

  Therefore, it appears that the name “mainframe” is not found in any of these three.  
</p>
<p>
  5. Go to DNS Manager on DC-1, and create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address, (10.0.0.4).
</p>
<p>
  <img src="https://i.imgur.com/xkjOzEw.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
  <img src="https://i.imgur.com/bCHACop.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  6. Go back to Client-1 and try to ping it. Observe that it works.
</p>
<p>
  <img src="https://i.imgur.com/xiG9ab2.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h3>Local DNS Cache exercise</h3>
<p>
  7. Go back to DC-1 and change the "mainframe’s" record IP address to (8.8.8.8). 
</p>
<p>
  <img src="https://i.imgur.com/pjvhP6v.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  8. Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address.
</p>
<p>
  <img src="https://i.imgur.com/Tlf0WAL.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
  Mainframe’s IP Address still points to 10.0.0.4.
</p>
<p>
  9. Observe the local DNS cache with the command (ipconfig /displaydns).
</p>
<p>
  <img src="https://i.imgur.com/8pFkbxV.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  It's A (Host) Record still says address 10.0.0.4, that’s a problem, it should be 8.8.8.8 after the changes we made in the DNS server.

  Here's how we troubleshoot it❗
</p>
<p>
  10. Flush the DNS cache with the command (ipconfig /flushdns) to refresh or update.

  - To flush the DNS cache, we need to use PowerShell as an Admin.
</p>
<p>
  <img src="https://i.imgur.com/jsGO0le.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  11. Observe that the cache is empty with the command (ipconfig /displaydns).
</p>
<p>
  <img src="https://i.imgur.com/RDlrYyJ.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  12. Attempt to ping “mainframe” again. Observe that the address of the new record is showing up, which is 8.8.8.8
</p>
<p>
  <img src="https://i.imgur.com/S0y2vDj.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  This shows why the “ipconfig /flush” command is good to use. If someone in the organization can’t access the same resources as everyone else, it may have something to do with the DNS and Local Cache. 
  
  It would be best to try refreshing or updating the DNS cache. 
</p>
<br />

<h3>CNAME Record exercise </h3>
<p>
  13. Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”.
</p>
<p>
 <img src="https://i.imgur.com/gIB8cEA.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
 <img src="https://i.imgur.com/cCWXxSI.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  14. Go back to Client-1 and attempt to Ping “search”, and observe the results of the CNAME record. 
</p>
<p>
  <img src="https://i.imgur.com/xRhK54m.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  15. On Client-1, use the command nslookup “search”, and observe the results of the CNAME record.
</p>
<p>
  <img src="https://i.imgur.com/2At9LqL.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
  This lab had a high overview of DNS (Domain Name System).
</p>

