## Command line File Sync Application

 Rsync is a very robust CLI tool that provides fast incremental file transfer with many features:

-   Checksum verification

-   Automation via Bash script

-   Resume broken transfer

-   Preinstalled on Most Linux/Unix Systems

https://rsync.samba.org/

### Pulling files from your slot using Rsync

Given the fact Rsync is included on Most if not all modern Distros, It is simple to begin pulling files from your Ultraseedbox slot. First login to the machine you plan on storing the pulled files. Not your Ultraseedbox Slot

`rsync -aHAXxv --numeric-ids --info=progress2 --bwlimit=20000 user@lwxx.usbx.me:./path/to/download/ /home/targetusername/path/to/save/to`


Rsync will now ask you if your hostkey is correct, If this is your first time connecting this is totally normal type `yes` and hit Enter. This will now prompt you for your Ultraseedbox SSH Password.

| Argument          | Effect                                                                                                           |
|:-------------------:|:------------------------------------------------------------------------------------------------------------------:|
| -a                | Tells rsync to recursively copy everything                                                                       |
| -H                | This tells rsync to look for hard-linked files in the source and link together the matching files on the target  |
| -A                | Tells Rsync to keep permissions the same on target                                                               |
| -X                | Tells Rsync to keep any file attributes the same on target                                                       |
| -x                | Tells Rsync to avoid copying Mounts and fuse based filesystem                                                    |
| -v                | show all output                                                                                                  |
| --bwlimit=20000   | Apply a Bandwidth limit of 20 Megabytes                                                                          |
| user@lwxx.usbx.me | Fill this with your Ultraseedbox Username and Server address                                                     |



### Uploading files to your slot using Rsync

Uploading to your slot is just as simple as downloading from your slot to a new location. Login to your Ultraseedbox Slot
`rsync -aHAXxv --numeric-ids --info=progress2 --bwlimit=20000 -e "ssh -p portnumberhere" username@remoteip:/home/remoteusername/ ~/Rsyncdrop
`

Please note `portnumberhere` this is added so if your target machine is using an ssh port that is not the standard 22 you can insert it here, otherwise please enter 22 in its place

Like when Pulling files from your Ultraseedbox slot, you will be prompted to confirm your hostkey and remote machines SSH Password.

### Creating a Full copy of a Userspace from a remote Server

You will find this familiar if you have followed our provider migration guide, However now is a good time to refresh yourself on the Process as it can be adjusted for many different paths etc.

So exactly like before when uploading files to your Ultraseedbox Slot you will need to run this from your slot.

We recommend running a screen if you are copying a large directory structure.

`screen -r usercopy`

`rsync -aHAXxv --numeric-ids --info=progress2 --bwlimit=20000 -e "ssh -p portnumberhere" username@host:/home/remoteusername usercopy`

Press `CTRL A+D` to detach leaving the transfer running
you can reattached with `screen -rd usercopy`

This will place all of your remote servers /home/username directory to a folder called `usercopy` on your Ultraseedbox Slot.
