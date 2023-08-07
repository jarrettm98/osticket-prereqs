<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>
<h1>osTicket Installation and prerequisits</h1>
This is a tutorial of how to set up and install the open-source help desk, osTicket. Microsoft Azure will be the tool of choice to create a Virtual Machine, which will be used to set up the Help desk. Users such as Admins and Agents will be able to sort and resolve tickets (Ones created by yourself of course). OsTicket is a helpful tool to learn how setup a help desk as well as use one to resolve client issues in a help desk. <br/>
<h2>Technology used in this project</h2>

- HeidiSQL
- Internet Information Services (IIS)
- Microsoft Azure (Virtual Machines/Compute)
- osTicket
- Remote Desktop
  
<h2>Operating Systems Used</h2>

- Windows 10 (21H2)

<h2>Installation Files Used</h2>

- HeidiSQL
- mysql
- osTicket
- php
- PHPManagerForIIS
- rewrite_amd64
- VC_redist.x86

<h2>Installation Steps</h2>

- Create A Virtual Machine with Azure
- Use Remote Desktop Protocol into your Windows 10 virtual machine
- Install / Enable IIS in Windows with CGI
- Download and install PHP Manager for IIS
- Download and install the Rewrite Module
- Create the directory C:\PHP
- Download PHP 7.3.8 and unzip the contents into C:\PHP
- Download and install VC_redist.x86.exe
- Download and install MySQL 5.5.62
- Open IIS as an Admin and register PHP from within IIS
- Install osTicket v1.15.8
- Download and install HeidiSQL
- Continue to set up osTicket in the browser

<h2>osTicket Installation</h2>

<p>
First, create a Virtual Machine in Azure. Using the IP address and login that has been set up with the Virtual Machine, connect through Remote Desktop Connection. There might be a popup about identity verification of the remote computer not being verified, go ahead and click "Yes" to connect remotely to the Virtual Machine. </p>

<p>
When the VM starts up It will ask a few questions about privacy settings, just tick all of the boxes so they are disabled. Use this link for all of the necessary links to download for this project. https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6</p>

<p>
Before installing anything from this list, it's time to install some IIS features. Go to Control Panel > Programs and Features and click on "Turn Windows features on or off" Make sure the box for "Internet Information Services" is checked. Then expand IIS as well as "World Wide Web Services" and "Application Development Features" and check the box next to "CGI." Also expand "Common HTTP Features" and tick all of the boxes in the dropdown that are not already ticked. After all boxes mentioned above are checked, click "OK" then "Apply" to install features. 
</p>

![IIS CGI](https://github.com/jarrettm98/osticket/assets/140662793/bd129eea-be91-4c33-8b7e-4a4f74ab44e5)

![IIS COMMON HTTP](https://github.com/jarrettm98/osticket/assets/140662793/1bbbd548-c7ca-4d6d-a16b-df90fdfd3d5f)

<p>If you want to test your web server, you can open your browser and type in 127.0.0.1 into the address bar. You should be able to see the IIS page appear. If not, you may have to re-check the instructions above. Example image below:
</p>
<p>
  
  ![Loopback link works](https://github.com/jarrettm98/osticket/assets/140662793/98fd70e9-9029-473b-ab4e-f157953e58c2)

</p>

<p>After that is complete, it is time to install a few things. Go to the files linked above and install "PHPManagerForIIS" and "rewrite_amd64." Once those are installed, create a folder on the C: Drive and name it "PHP." Download the php-7.3.8-nts-Win32-VC15-x86.zip file and extract the files in the "PHP" folder that was just created.</p>
<p>
Now after all of the files are extracted, download and install "VC_redist.x86.exe" and "mysql-5.5.62-win32.msi". 
</p>
<p>
When installing MySQL choose a "typical" installation and make sure the "Launch the MySQL Instance Configuration Wizard" box is checked. When it is launched choose the "Standard Configuration" and click next. On the next page choose "Install As Windows Service" and click next. Next you will be creating a password for the server and click next. You can use your own password, however I like to make my password to be "Mypassword123" because it is easy to remember. If needed, the password can be written down in a notepad so it isn't forgotten. It will be used later.
</p>
<p>
After MySQL is finished installing, go to Windows Explorer and search for Internet Information Services(IIS) Manager and right click it to open it as Administrator. When you open IIS, there will be an option for "PHP Manager." Click on that and "register new PHP version". Navigate to the "PHP" folder that was created earlier and choose the "php-cgi" executable. If you dont see it, make sure the box to the right of the file name box is set to "PHP executable." Now reload IIS by clicking on your local host server "VM-osTicket" and clicking "Restart" under Manage Server.
</p>

<p>
  
![IIS WINDOW](https://github.com/jarrettm98/osticket/assets/140662793/1253f608-f165-4403-b46e-c4264970d309)
</p>
<p>
Now download osTicket from Installation Files Folder, Extract and copy the “upload” folder to C: > inetpub > wwwroot. In C:\inetpub\wwwroot, rename the “upload” folder to “osTicket”. To do this, open two separate File Explorer windows. On one, navigate to the Downloads folder and double click the "osTicket-v1.15.8" folder. There, you will find the "upload" folder. On the other window, click on Windows (C:) drive, locate the "inetpub" folder, open it, then open the "wwwroot" folder. Drag the "upload" folder into the wwwroot folder. Once the upload folder is dragged into the wwwroot folder, rename the upload folder to "osTicket."
</p>
<p>
After the upload folder is transferred and renamed, go back to IIS and restart server. Now in IIS, expand VM-osTicket > Sites > Default Web Site > osTicket and click on Browse *:80 (http) (Should be under "Manage Folder" options on the right side of the window. This will take you to the osTicket Installer website for your help desk.
</p>
<p>

  ![osTicket Installer without extentions](https://github.com/jarrettm98/osticket/assets/140662793/858202fe-5f76-4b2f-8418-05f33eb93d29)

</p>
<p>
  Notice that there are some features without a checkmark by them. This is where we will add the "imap" and "intl" features. Go back to VM-osticket > Sites > Default Web Site > osTicket and find "PHP Extensions" on the main page. Under that, there will be an option "Enable or disable an extension." Click that and it will bring up a list of features. There will be 3 features that will be enabled ("php_imap.dll", "php_intl.dll", and "php_opcache.dll") Find these in the list, right-click on them, then enable them. Refresh your webpage for the osTicket Installer. Two checkmarks should be enabled. (PHP IMAP Extension and Intl Extension)
</p>


  
<p>
  There will be two more things to be done before continuing on the webpage. Find the "ost-sampleconfig" file in C:/ > inetpub > wwwroot > osTicket > include > ost-sampleconfig.php and rename it to "ost-config.php". Lastly, with the newly-named ost-config.php file, right-click it and go to properties > security tab > advanced. Click the "Disable Inheritance" button and "Remove all inherited permissions from this object." Click the "Add" button, then "Select a principle." In the text window write "Everyone" and Check names. Click OK and check the "Full control" button to give everyone Full control. Make sure to apply these changes.
</p>
<p>
Finally, it is time to continue on the webpage by clicking the continue button at the bottom of the page. There will be some features still un-added but it will not matter for this tutorial. In the next page, there will be basic information for the help desk that will need to be filled out. The only real important information that needs to be remembered will be the login credentials. (Username and password) Make sure to write these down, because they will be used to administrate the help desk. Before installation, download HeidiSQL from the Installation Files above. When installing HeidiSQL make sure it Launches after install. When Heidi launches, click "New" in the bottom left corner. Using the MySQL login credentials from before, input the user and password. (User should be "root" if it isn't already) Click the "Open" button. Then in the created database, right-click the "Unnamed" session and click "Create new" and then click "Database." Name the database "osTicket" and then click OK.
</p>
<p>
Back on the webpage, Input "osTicket" in MySQL Database, "root" in MySQL Username, and the password for MySQL, then click "Install."
</p>
<p>
The Help desk is now created. However, there is still a little cleanup left before continuing. Go to the C: Drive > inetpub > wwwroot > osTicket. In the osTicket folder, delete the "Setup" folder. After deleting the setup folder, go to C: Drive > inetpub > wwwroot > osTicket > include and right-click on ost-config file. Go to Properties > Security Tab > Advanced. Click on the "Everyone" option in the list and click "Edit." Uncheck all of the boxes except for "Read" and "Read & execute." Apply the changes.
</p>
<p>
Congrats! You created your help desk! Now copy and paste the following URL in your browser: 
  
  http://localhost/osTicket/scp/login.php
  
  This will let you access the Staff Control Panel
</p>
<p>

  ![osTicket Installer complete](https://github.com/jarrettm98/osticket/assets/140662793/0f1691e7-69d9-4565-8d1f-44668a2cc3e9)

</p>
For setting up the Help desk, go to the following link for that tutorial.

https://github.com/jarrettm98/osticket-post-install-config
