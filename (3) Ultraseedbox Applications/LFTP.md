## Command line based FTP client

 LFTP is a fully featured FTP client with a CLI interface:

-   Multiple segmented Download/Upload

-   Automation via Bash script

-   Multiple simultaneous downloads

-   Directory Navigation

https://lftp.yar.ru/

### Pushing files from your slot using LFTP

This is for those that would like to automate downloading or "pushing" files off of your Ultra.cc Slot to another FTP server. For example you may run a Network Attached Storage device at home which is able to run a simple SFTP/FTP server. This command below can be setup to run automatically and send anything in one folder to your Server at your residence while you sleep. Great for grabbing the latest Nightlight Linux distro's.  

`lftp -u destinationusername,destinationpassword -e 'mirror --reverse --parallel=3 --continue --use-pget-n=5 --only-missing /home3/usbdocs/files/LFTP /home/destinationusername/LFTP; quit' sftp://destinationip:port`

The Path `/home3/usbdocs/files/LFTP` is used purely as an example you could change this to any path on your Ultra.cc Slot and LFTP would push that path to the target. You may also add multiple copies of the above line when creating your bash script (details below) to sync multiple folders to multiple target servers and/or folders.

| Argument          | Effect                                                                                                                                                                                                                                                                                                                                                |
|:-------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| use-pget-n=2    | Number of Segments per file, This is best matched to the number of Parallel downloads for example if your parallel=2 then pget-n=2 too. Don’t aim for two high a number for example 4 and 4 would be 4 downloads each in 4 segments for 16 threads even this maybe higher then required. Experiment to see what works best for your target connection |
| continue        | Create .part files in case of accidental disconnection. This will allow the next run of lftp to pick up where it left off. This may need disabling if you fine the end transfer to be corrupted (just delete --continue)                                                                                                                               |
| mirror          | specify a source and target directory                                                                                                                                                                                                                                                                                                                 |
| parallel=number | Number of files to Push to target at once                                                                                                                                                                                                                                                                                                             |
| reverse         | reverse mirror i.e. put all files from a Ultra.cc slot to a Target Server                                                                                                                                                                                                                                                                         |
| only-missing    | Push only files not already present on the target server                                                                                                                                                                                                                                                                                              |
sftp://destinationip:port| This will need to be changed to reflect the type of server your connecting to SFTP/FTP the example here connects to an SFTP server. destinationip and port will need filling based on your target connection details.


### Uploading files to your slot using LFTP

Uploading to your slot is just as simple as downloading from your slot "pushing". Using the same command above will work as long as it is run from the location you want your files to arrive at.
`lftp -u usbslotusername,usbslotpassword -e 'mirror --reverse --parallel=3 --continue --use-pget-n=5 --only-missing /home/destinationusername/LFTP /home3/usbdocs/files/LFTP; quit' sftp://destinationip:22`

Notice that the main changes are the order of directory and the address at the end. The function of the command is exactly the same, It is just the direction that has changed.

### Automating the Process With Bash and Crontab

Your first step is to find the full path of your home directory `pwd` will output your full home path.

Something like this will be outputted be sure to make a note of it :


`/home3/usbdocs`

then create two new folders, one may already exist this is fine

`mkdir ~/lock`

`mkdir ~/scripts`


Then you need to enter the new folder called scripts

`cd ~/scripts`

And create the script file

`nano LFTP.sh`

Paste the following lines into it :
```
#!/bin/bash
exec {lock_fd}>/home1/usbdocs/lock/lftpLock || exit 1
flock -n "$lock_fd" || { echo "ERROR: flock() failed." >&2; exit 1; }
if [ -z "$STY" ]; then exec screen -dm -S lftp /bin/bash "$0"; fi

lftp -u destinationusername,destinationpassword 'mirror --reverse --parallel=3 --continue --use-pget-n=5 --only-missing /home3/usbdocs/files/LFTP /home/destinationusername/LFTP; quit' sftp://destinationip:port

flock -u "$lock_fd"
```
Save it by pressing Ctrl+X then Y then Enter. You will need to change the paths “home3/usbdocs” to match your own home and username.

Now we need to set a few things that will be passed to LFTP automatically ready for automation.

create a folder to house the configuration file.

`mkdir ~/.lftp`

now create the rc file to place the options inside

`nano ~/.lftp/rc`

Paste these lines in and save
```
set net:limit-total-rate 0:41943040
set ssl:verify-certificate no
```

#### Testing the script before Automating

So to test first we navigate to ~/scripts folder we made earlier

`cd ~/scripts`

Then we need to allow the LFTP.sh permissions to run

`chmod +x LFTP.sh`

And finally, run it

`./LFTP.sh`

If the script is running and you were to run it again, you may see an error message “Flock Failed” this is a file lock to stop multiple backups running and is totally normal. If you are sure it isn’t running you can delete the lock file from ~/lock. You can also check the progress of the backup script which is running in a screen with the command

`screen -rd lftp`

#### Setting the automation and time

If all is well after the test we can automate the check via crontab

Open crontab with

`crontab -e`

You may have a choice of editors we recommend Nano

Inside the crontab add a single line under everything else in the file that looks like this

`0 */4 * * *  /home3/usbdocs/scripts/LFTP.sh`

Save it by pressing Ctrl+X then Y then Enter.

Once again we want to remind you that the paths will need changing to reflect the path shown by the `pwd` command

The script will now run every 4 hours checking for files that have changed and sync them to the target server. Please be aware anything removed from the Target will be synced again. Remove the item from the source or move it to a non synced folder.
