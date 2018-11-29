---
title: Installation
---
# Installation Insctructions
<br />
## Stuff To Download
To get setup with the SWG Source platform,  you will need the server and client archives:
* [SWG Source Server v1.2.1](https://bit.ly/SWGSourceServer121)
* [SWG Source Client v1.2.1](https://bit.ly/SWGSourceClient121)

You will also need [7zip](https://www.7-zip.org/) to open those archives and [Oracle VirtualBox](https://www.virtualbox.org/) to run the server VM. (It is also recommended that you install the Extension Pack for USB 3.0 support.)

## Server Setup
After unpacking the server, open VirtualBox, select `Machine -> Add...`, and navigate to the directory in which you extracted the archive. Select `SWG Source v1.2.1.vbox` and click Open. You should click Settings and make sure everything is set correctly for your system. By default, the VM will only use 2 cores, but you can give it more if you have them available. The RAM is set to 8192MB by default but you should increase this if you want to run more than one or two planets at a time. (At least 16GB is recommended if you want to run all zones.) The network adapter is set to Bridged by default, which tends to work best, but you can adjust the network settings as needed.

When you're ready, click Start.

## Configure for your IP Address
By default, the VM will get an IP Address from the DHCP server in your router. If your router lets you set a DHCP reservation, you should do that. The VM's MAC Address is 08002785E97A. Otherwise, you should manually set a static IP Address outside your DHCP range by going to `Start Menu -> Settings -> Network Connections`, clicking Edit, selecting IPv4 Settings, and selecting Manual. Then fill out your Address, Netmask, and Gateway information and click Add.

__*Protip:*__ The IP Address currently used by your VM is shown in the information sidebar on the desktop.

You will then need to put your IP Address in your hosts file. Open a terminal and type `sudo nano /etc/hosts`. (The password is swg). Then navigate to the second line (ending in swg) and replace the IP Address there with whichever one you are using.

Next, you will need to put your IP Address in the SWG config files. Open the link on the desktop to access your config files.
The files you need to edit are:
* localOptions.cfg (4 instances)
* nodes.cfg
* default.cfg

## Adjust other config settings as needed

Most of the stuff you might want to change is in localOptions.cfg. Notably, this is the file where you can select which zones (ie: planets) are going to load. By default, only Tatooine will load. This is a great way to make sure everything will run. If you want to load more zones, first make sure that you have enough RAM. Then, remove the # from each line that you want to load. Save the file, and you're ready to rock and roll...

## Run your server!

Open Terminator terminal by clicking the red terminal link towards to left hand side of the taskbar. This should bring up a window with 4 terminals. The top two give you helpful information about your system. The bottom two will run your server. First, use the bottom right hand window to run `./chatServer`. Then, in the bottom left hand window, run `./startServer.sh`. Wait for the server to load. The terminal will let you know when the server is ready for players.

## Run your client!

Unpack the client archive with 7Zip. First, run SwgClientSetup_r.exe and make sure all your settings are correct for your system. Then, open login.cfg with a text editor (Notepad++, Atom, or whatever you happen to prefer). Change the loginServerAddress0 setting to match the IP Address of your Server VM. Save and close. Finally, run SwgClient_r.exe. You can login with username:swg password:swg to access some characters already on the server, or optionally login with whatever username and password you want to make your own account.

## Thats it!

To read about updating your server and client with the latest patches and updates from the SWG Source community, check out the Getting Updates guide (coming soon...)
