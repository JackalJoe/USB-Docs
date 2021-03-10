## SeedSync Lftp WebUI

>   Seedsync is an application designed to allow easy control and editing of
>   LFTP and its features:

-   Only requires Seedsync be installed on the source machine

-   AutoQueue functions can automate multiple files/folders

-   Can use SSHkey Authentication

<https://ipsingh06.github.io/seedsync/>

### Configuring SeedSync for the first time

Seedsync is a nice simple representation of the functions available in the LFTP
CLI application, As such you will want to install on a system you want files
pulled to for example a NAS on your home network. This guide will use
Ultra.cc slot as the origin of any files downloaded.

![]( <https://i.imgur.com/eIp0GzO.png>)

| Field                                       | Value                                                                                                                                                                   |
|:---------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Server Address                              | Your Ultra.cc Address (lwxx.usbx.me)                                                                                                                                |
| Server Username                             | Your Ultra.cc Username                                                                                                                                              |
| Server Password                             | Your Ultra.cc Password                                                                                                                                              |
| Server Directory                            | Folder path you would like downloaded to your local machine for example ~/files/                                                                                       |
| Local Directory                             | Folder path you would like the files stored on your local server for example /home/username/Ultra.cc (this folder will need to be created or already exist)         |
| Remote SSH Port                             | For Ultra.cc 22 is the default, but if you are connecting to a different machine you will need to change this to match the machine your downloading from            |
| Server Script path                          | This is the location that Seedsync will install its “watcher” which will allow Seedsync to know when new files are available in your Auto Queue settings                |
| Enable Auto Queue                           | Leave this checked as one of the main features of seedsync is the automation                                                                                            |
| Enable Auto Extraction                      | This is also best left on as if your Linux Iso is zipped to save space this will unpack it leaving you with a ready to use .ISO                                         |
| Extract archives in the download directory  | Disabling this will allow you to specify a directory for the extracted files to reside, leaving it enabled will extract to the same folder the original download is in  |
| Max Parallel Downloads                      | How many files to download together during a sync operation. (messing with these settings may degrade performance by setting to high a value)                           |
| Max Total Connections                       | Max number of connections made to a host when downloading. (messing with these settings may degrade performance by setting to high a value)                             |
| Max Connections Per file (single file)      | Number of connections for a single file download. (messing with these settings may degrade performance by setting to high a value)                                      |
| Max Connections Per file (Directory)        | Number of per file connections when downloading a complete directory. (messing with these settings may degrade performance by setting to high a value)                  |
| Max Parallel files (Directory)              | Max number of files to download together for a single directory download. . (messing with these settings may degrade performance by setting to high a value)            |
| Rename unfinished/downloading files         | Unfinished and downloading files will have the extension .lftp                                                                                                          |
| Remote Scan interval                        | How often the remote server is scanned for new files. This value is in milliseconds.                                                                                    |
| Local Scan interval                         | How often the local directory is scanned to ensure sync status                                                                                                          |
| Download scan interval                      | How often the download information is updated                                                                                                                           |
| Web GUI Port                                | The port at which the webui can be reached.                                                                                                                             |

Once your settings are all inputted, You will need to restart to apply them.

### Monitoring your Download Progress

Upon restarting Seedsync should install the required Watcher Scripts and begin
syncing the paths you specified.

![](<https://i.imgur.com/GzTSdSW.png>)

### Setting up AutoQueue

Before you can use the AutoQueue function you will need to enable Restrict to
Patterns in the Settings menu under Auto Queue Header. This will allow you to
only sync files that match a particular patten/extension etc. This is great if
you would like to send the unpacked .ISO file of your Linux distro without also
downloading the original .rar/.zip files also. This is as simple as typing
something you wish to match in the text box provided and Clicking the plus Icon.
The end result will look like this and now Seedsync will only download .ISO
files.

![](https://i.imgur.com/o4DtvnI.png)
