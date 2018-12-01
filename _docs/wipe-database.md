---
title: Wipe Your Database
---
# Wipe Your Database
You might sometimes want to wipe your SWG database and start all over. This guide will help you do that. This guide assumes that you are already up and running on the v1.2.1 SWG Source Server VM.

In your VM, go to `Start -> Logout -> Logout`. You will be brought to a login page. Login with Username: `oracle` and Password: `swg`.
[![Login as oracle](/assets/images/wipe-database-1.PNG)](/assets/images/wipe-database-1.PNG)
Use the button at the top of the desktop to open a terminal. Enter the command `dbca` and press enter.
[![dbca](/assets/images/wipe-database-2.PNG)](/assets/images/wipe-database-2.PNG)
This will open the Oracle Database Configuration Assistant. The first thing we will do it delete the database that already exists. Select "Delete database" and click Next.
[![Delete Database](/assets/images/wipe-database-3.PNG)](/assets/images/wipe-database-3.PNG)
You will need to provide the password (`swg`) and click Next again.
[![password](/assets/images/wipe-database-4.PNG)](/assets/images/wipe-database-4.PNG)
You will then be given the option to De-Register from EM Cloud Control. Just leave it unchecked and click Next.
[![Leave Unchecked](/assets/images/wipe-database-5.PNG)](/assets/images/wipe-database-5.PNG)
You will be given a summary of what is about to happen. Click Finish to run the operation.
[![Finish](/assets/images/wipe-database-6.PNG)](/assets/images/wipe-database-6.PNG)
Click Yes when prompted.
[![yes](/assets/images/wipe-database-7.PNG)](/assets/images/wipe-database-7.PNG)
Click Close when the operation has finished.
[![close](/assets/images/wipe-database-8.PNG)](/assets/images/wipe-database-8.PNG)
Use the Terminal to run the `dbca` command again. This time, we want to Create a database, so make sure that's selected and click next.
[![Create a database](/assets/images/wipe-database-9.PNG)](/assets/images/wipe-database-9.PNG)
You will now need to enter all the information Oracle needs in order to make your new database. Also, be sure to uncheck the "Create as a container database" selection. It's easiest if you choose `swg` for the Global database name and the password. You might be prompted that your password is not good enough, but you can just click Yes to continue.
[![swg](/assets/images/wipe-database-10.PNG)](/assets/images/wipe-database-10.PNG)
You will again be presented with a summary of what is about to happen. Click Finish to run the operation. This one may take several minutes.
[![finish](/assets/images/wipe-database-11.PNG)](/assets/images/wipe-database-11.PNG)
Click Close when the database creation is complete.
[![close](/assets/images/wipe-database-12.PNG)](/assets/images/wipe-database-12.PNG)
Next, enter the command `sudo nano /etc/oratab` and press enter. This will open the oratab configuration file.
[![oratab](/assets/images/wipe-database-13.PNG)](/assets/images/wipe-database-13.PNG)
Use your arrow keys to navigate to the bottom of this file and change the last character on the last line from `N` to `Y` as shown. This tells the system to automatically start your new database at the system's boot time.
[![Y](/assets/images/wipe-database-14.PNG)](/assets/images/wipe-database-14.PNG)
When you're finished, press CTRL+X to exit. Nano will ask you if you want to save. Press Y then Enter to save and close. You should now reboot your VM by going to `Start -> Logout -> Restart`.

When your VM has rebooted, use the small button near the start menu to open SQL Developer. Right click on the existing connections to delete them.
[![Delete connections](/assets/images/wipe-database-15.PNG)](/assets/images/wipe-database-15.PNG)
Next, use the green plus sign to make a new connection. Enter a name that makes sense, then Username: `system` and Password: `swg`. Set your SID to `swg`. It's also helpful to check the Save Password checkbox. (Even though I didn't in the screenshot, I should have, haha.) You can then press the Test button to make sure everything's working. If so, click Save and close the window.
[![enter info](/assets/images/wipe-database-16.PNG)](/assets/images/wipe-database-16.PNG)
Double click on your new connection to connect to it. Once you've connected, you will need to copy the following commands into the Query Builder worksheet that was opened:
```
ALTER USER SYSTEM IDENTIFIED by "swg";
ALTER SESSION SET "_ORACLE_SCRIPT"=true;
CREATE USER swg IDENTIFIED by "swg";
GRANT ALL PRIVILEGES TO swg;
GRANT UNLIMITED TABLESPACE TO swg;
alter system set sessions=3000 scope=spfile;
alter system set processes=3000 scope=spfile;
alter profile default limit password_life_time unlimited;
```
After pasting these commands, click the "Run Script" button, that is, the play icon with the paper behind it. (NOT "Run Statement", that is, the regular play icon.)
[![sql query](/assets/images/wipe-database-17.PNG)](/assets/images/wipe-database-17.PNG)
You will now need to add another connection, so click the green plus sign once more. This time, your Username, Password, and SID should all be `swg`. Again, check the Save Password checkbox, even though I forgot to in the screenshot. Click Test, then Save if your test was successful.
[![swg connection](/assets/images/wipe-database-18.PNG)](/assets/images/wipe-database-18.PNG)
You may now close SQL Developer and open Terminator terminal. In the bottom left window, use the command `./build_linux.sh`.
[![build linux](/assets/images/wipe-database-19.PNG)](/assets/images/wipe-database-19.PNG)
You can skip most steps by entering `n`. The step you're interested in is importing the database. Select `y` for this one. The script will ask you a series of questions to get the information it needs to set up your new database. Use these responses:
```
Enter the DSN for the database connection: //127.0.0.1/swg

Enter the database username: swg

Enter the database password: swg

Enter value for max_characters_per_account: 10

Enter value for max_characters_per_cluster: 10

Enter value for character_slots: 10

Enter value for cluster_name: swg

Enter value for host: 127.0.0.1
```
That's it! Start up your server and enjoy your fresh database.
