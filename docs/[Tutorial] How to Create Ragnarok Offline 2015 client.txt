Link to forum:
https://rathena.org/board/topic/104452-tutorial-how-to-create-ragnarok-offline-2015-client/


Hi Everyone,
 
    This is an updated and detailed guide on how to setup a Ragnarok Offline 2015 client. Thanks to Scylla for assisting me step by step on how to setup!

  Let me know if I should clarify/change some information in the tutorial
 
 
Required Software/Files
 
Server-Side
 
rAthena 
Xampp (for the mysql database and sql script execution)
Visual Studio Community Edition (for compiling rAthena solution. Couldn't find any earlier version of VS express)

Client-Side
 
Latest KrO client (Update the client using the patchers before proceeding with the client side setup)
Lastest Client (Executable file)
NEMO
RO Translation
 
I suggest you download all the files first so you dont need to go back in configuring other things
 
Setup Server Side
 
Configuring rAthena
 
Change packet_db_ver
 
1. Open rAthena/db/packet_db.txt
2. Modify packet_db_ver: default to packet_db_ver: XX      where XX is the version of the packet_db_ver of your KrO client (55 when I installed it)
3. Save
 
Change  #define PACKETVER
 
1. Open rAthena/src/common/mmo.h
2. Modify #define PACKETVER YYYYMMDD      where YYYYMMDD is the date of the client. Example, #define PACKETVER 20151104 (I used 20151104 to match my exe download)
3. Save
 
Comment #define PACKET_OBFUSCATION
 
1. Open rAthena/config/core.h
2. Modify #define PACKET_OBFUSCATION to //#define PACKET_OBFUSCATION <-- if error occurs in the end of the guide such as server disconnects you after character select, as per user iantoom, do not modify. Do not check Disable Packet Encryption in the Diff Ragexe using nemo, refer to the Setup Client-Side below) Note: You have to recompile rathena if you have changed this setting 
(I left this defined and just did not check disable packet encryption)
3. Save
 
Compile rAthena using a compiler(I used Visual Studio)
I wont go into further details in compiling rAthena for it is already explained specifically at the wiki .
 
 
Setup rAthena config
 
I wont go into further details in configuring IP in rAthena for it is already explained specifically at the wiki . IP address should be 127.0.0.1
 
 
 
Setup Database
 
You may refer at the wiki regarding how to setup the database. In my case, I use a different approach by using Xampp.
Xampp Setup
 
1. Install Xampp
2. Launch Xampp Control Panel
3. Start Apache
    If Apache doesnt start, do the following configurations:
    Modify ports 80,443
      -Click Config button for apache
      -Select httpd.conf
      -Modify Listen 80 to Listen 81
      -Save
    
      -Click Config for apache
      -Select httpd-ssl.conf
      -Modify Listen 443 to Listen 444
      -Save
    You should be able to start apache now
 
4. Start MySql
 
Create account and database setup
 
1. On your web browser go to http://localhost:81/phpmyadmin/ (or http://localhost/phpmyadmin/ if you did not modify the ports 80 and 443)
2. Click User Accounts
3. Click Add User Accounts
4. Set username and password to ragnarok
5. Select hostname as local
6. Check Create database with same name and grant all privileges.
7. Check All in Global Priveleges (just to be sure)
8. Click Go
 
Execute all SQL scripts in rathena
1. In phpmyadmin, click the ragnarok database
2. Click SQL
3. Open rathena\sql-files folder
4. Open .sql files(one by one, including ,sql files in subfolders) and copy paste it in the SQL phpmyadmin textarea
5. Click Go
6. Repeat step 4 until all .sql files are executed.
 
Create Account in Database
1. In phpmyadmin, expand the ragnarok database
2. Click Login table
3. Click Insert
4. Fill in username, password and gender
5. Set group id to 99
6. Click Go
 
Run rAthena Server
1. Open rAthena folder.
2. Run runserver.bat
 
The 3 servers should be running properly :)
 
My screenshot of the 3 running servers I configured
 
zGXRe9N.png
 
Setup Client Side
 
Diff Ragexe
1. Open NEMO
2. Browse for Input Exe File. Locate the Client Exe file you have downloaded
3. Click Load Client.
4. Click Select Recommended.
5. Just click OK to the Window that pops up
6. Check Disable Packet Encryption <-- if error occurs such as server disconnects you after character select, as per user iantoom, do not check. Enable Packet Obfuscation instead, refer to the configuring rathena above.
7. Check Use Ragnarok Icon
8. Check Read data folder first
9. Click Apply Selected
 
You should now have a patched exe file in the same folder location(of the exe you downloaded)
 
Placing all processed files in one folder
 
1. Create New Folder
2. Copy Data and System Folder from your downloaded RO Translation folder to your New Folder
3. Copy BGM and SaveData folder from your downloaded/installed kRo Folder to your New Folder
4. Copy data.grf from your downloaded/installed kRo Folder to your New Folder
5. Copy All dll files from your downloaded/installed kRo Folder to your New Folder
6. Copy Setup.exe  from your downloaded/installed kRo Folder to your New Folder
7. Copy patched exe file to your New Folder
 
Modify ClientInfo.xml
 
1. Open data/clientinfo.xml in your New Folder
2. Modify Address to 127.0.0.1
3. Modify Version to XX    where XX is the packet_db_ver (55)
 
 
Launch patched exe file
 
Login using the account created earlier. Enjoy Playing!
Sample Screens of my server

fwTmBjP.jpg
 
7d0dyvo.jpg
 
NOTE:
- Make sure you set the group id of your account in the database to 99. This will make the account a Game Master
- On the first login, characters are spawned in the bugged izlude map (black screen and unable to move). Use the @go 0 command to teleport to prontera
- Also I apologize that I can't help you guys with the other concerns (Weird server errors etc.) . I made this guide based on how Scylla helped me step by step. I am also not that knowledgeable to determine your issues. It is preferable you go at discord and ask our awesome veteran members for concerns like this :)
