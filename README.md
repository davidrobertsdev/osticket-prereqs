
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket on a Windows virtual machine in Azure.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- PHP Manager for IIS
- MySQL
- HeidiSQL

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure account with an active subscription (to create the Windows VM)
- Remote Desktop client to connect to the VM
- Internet Information Services (IIS) with CGI enabled
- PHP 7.3.8 (nts, VC15 x86), PHP Manager for IIS, IIS URL Rewrite Module, and Visual C++ Redistributable (VC_redist.x86)
- MySQL 5.5.62 and HeidiSQL (database server and client)
- osTicket v1.15.8

<h2>Installation Steps</h2>

<p>
<img src="YOUR-IMGUR-LINK-1" height="80%" width="80%" alt="Azure virtual machine"/>
</p>
<p>
<b>Step 1: Create the Azure VM.</b> In the Azure portal, create a Windows virtual machine in its own resource group (here, OSTICKET_GROUP in South Central US). Once it finishes deploying, copy the VM's public IP address. (Screenshot: Azure Virtual machines list)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-2" height="80%" width="80%" alt="Installation files in Google Drive"/>
</p>
<p>
<b>Step 2: Download the installation files.</b> Connect to the VM with Remote Desktop, then open the Installation Files folder in Microsoft Edge. It contains everything needed: PHP 7.3.8, PHP Manager for IIS, the Rewrite module, VC_redist.x86, MySQL 5.5.62, HeidiSQL, and the osTicket v1.15.8 zip. (Screenshot: Drive folder list view)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-3" height="80%" width="80%" alt="Creating the PHP directory"/>
</p>
<p>
<b>Step 3: Prepare PHP.</b> After enabling IIS with CGI, install PHP Manager for IIS, the Rewrite module, and VC_redist.x86. Then create the <code>C:\PHP</code> folder in PowerShell with <code>mkdir C:\PHP</code> and extract the PHP 7.3.8 zip into it. (Screenshot: PowerShell mkdir)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-4" height="80%" width="80%" alt="Restarting IIS"/>
</p>
<p>
<b>Step 4: Register PHP and restart IIS.</b> Open PHP Manager in IIS and register <code>C:\PHP\php-cgi.exe</code>. Then select the server in the Connections pane and click <b>Restart</b> under Manage Server so the changes take effect. (Screenshot: IIS Manager with Restart circled)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-5" height="80%" width="80%" alt="Enabling PHP extensions"/>
</p>
<p>
<b>Step 5: Enable required PHP extensions.</b> After extracting osTicket into <code>C:\inetpub\wwwroot\osTicket</code>, open PHP Manager's PHP Extensions page and enable <code>php_imap.dll</code>, <code>php_intl.dll</code>, and <code>php_opcache.dll</code>. (Screenshot: PHP Extensions with the three circled)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-6" height="80%" width="80%" alt="Installing HeidiSQL"/>
</p>
<p>
<b>Step 6: Install MySQL and HeidiSQL.</b> Install MySQL 5.5.62 and set a root password. Then install HeidiSQL, open the Session Manager, and create a new session to connect to the local MySQL server. Create a database named <code>osTicket</code>. (Screenshots: HeidiSQL setup complete and Session manager)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-7" height="80%" width="80%" alt="ost-config.php permissions"/>
</p>
<p>
<b>Step 7: Set permissions on ost-config.php.</b> Rename <code>ost-sampleconfig.php</code> to <code>ost-config.php</code> in <code>C:\inetpub\wwwroot\osTicket\include</code>. Right-click it, open Properties > Security > Advanced, disable inheritance, and give Everyone full control so the installer can write to it. (Screenshots: ost-config.php Properties and Advanced Security Settings)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-8" height="80%" width="80%" alt="osTicket installer database settings"/>
</p>
<p>
<b>Step 8: Run the osTicket installer.</b> Browse to <code>http://localhost/osTicket/setup/install.php</code>. Fill in the admin details, then enter the database settings: prefix <code>ost_</code>, hostname <code>localhost</code>, database <code>osTicket</code>, and your MySQL username and password. Click <b>Install Now</b>. (Screenshot: Database Settings form)
</p>
<br />

<p>
<img src="YOUR-IMGUR-LINK-9" height="80%" width="80%" alt="osTicket login page"/>
</p>
<p>
<b>Step 9: Verify and clean up.</b> After a successful install, the osTicket login page loads, confirming the help desk is working. For security, delete the <code>setup</code> folder and change <code>ost-config.php</code> back to read-only, since the installer no longer needs write access. (Screenshot: osTicket login page)
</p>
<br />
