<p align="center">
<img src="https://i.imgur.com/CtGfsq8.png" alt="osTicket logo"/>
</p>

<h1>Learning DNS in Azure</h1>
In this lab, we will experiment with DNS using the Active Directory Lab. This lab will help us have a better understanding of DNS.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- DNS
- Powershell

<h2>Operating Systems Used</h2>

- Windows 10 Pro (22H2)

<h2>List of Prerequisites</h2>

- Active Directory Lab (Client & Server)
- Client Machine joined the Domain
<br />

<h3>A-Record Exercise</h3>
<p>
  1. Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
  
  2. Connect/log into Client-1 as an admin (mydomain\jane_admin)
  
  3. From Client-1, try to ping “mainframe” (Random Name) from Powershell. Notice that it fails.

  4. Use Nslookup “mainframe”, notice that it fails (no DNS record).
</p>
<p>
  <img src="https://i.imgur.com/hEK8bjk.png" height="90%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
  When the computer tries to interact with any host’s name on the Network, whether it's browsing to it or trying to ping it, the computer will first check its Local DNS cache,
  
  If it’s not found, then it will check its Local Host File, 
  
  If it’s not found there, then it will check its DNS Server as a last resort.

  Therefore, it appears that the name “mainframe” is not found in any of these three.  
</p>
<p>
  5. Go to DNS Manager on DC-1, and create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address, (10.0.0.4) 
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

<h3>Local DNS Cache Exercise</h3>
<p>
  7. Go back to DC-1 and change the "mainframe’s" record IP address to 8.8.8.8. 
</p>

