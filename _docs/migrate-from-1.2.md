---
title: Migrate from v1.2
---
# Are you already running SWG Source v1.2?
Great! You can get caught up to v1.2.1 without even loosing your database. Here's how:

__*Protip:*__: Take a snapshot of your VM before starting just in case you need to revert.

## Recommended Method

The best way to get all synced up is to rebuild your server. First, navigate to your home folder and rename swg-main to swg-main-old. (You can delete this directory later, but it's good practice to keep it until you're all set up just in case you need to revert.) Then, open a terminal and run the following commands one at a time:
```
cd ~
git clone https://github.com/SWG-Source/swg-main.git
cd swg-main
touch .setup
./build_linux.sh
```
The build_linux script will ask you to pull rest of the repos and rebuild everything. Answer yes to everything and let it do it's work. (When it asks for release or debug, choose release.)

After running the build script, you may choose to adjust any configuration files as needed in order to turn zones off or on, or set whatever else you like.

Finally, boot your server!

## Update Your Client

If you are using the v1.2 Client, you can configure it to get updates from the client-assets repository.

If you haven't already, you will need to install Git for Windows from [here](https://git-scm.com/download/win).

Open a GIT Bash in your client folder. Run the following commands one at a time:
```
git init .
git remote add -f origin https://github.com/SWG-Source/client-assets.git
git checkout master
```
You may now get updates to your client by opening a GIT Bash and running: `git pull`

__*Note:*__ If you have already configured your client to get updates from the client-assets repository on BitBucket, you should not use the commands listed above. Instead, you should be able to use these:
```
git remote remove origin
git remote add origin https://github.com/SWG-Source/client-assets.git
```
Test with `git pull` to make sure the reconfiguration worked.
