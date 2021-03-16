 **Sonarr** is a PVR for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new episodes of your favorite shows and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.

Major features include:

* Support for major platforms
* Automatically detects new episodes
* Can scan your existing library and download any missing episodes
* Can watch for better quality of the episodes you already have and do an automatic upgrade. _eg. from DVD to Blu-Ray_
* Automatic failed download handling will try another release if one fails
* Manual search so you can pick any release or to see why a release was not downloaded automatically
* Fully configurable episode renaming
* Full integration with SABnzbd and NZBGet
* Full integration with Kodi, Plex (notification, library update, metadata)
* Full support for specials and multi-episode releases
* And a beautiful UI

You can view the application's repo here: [https://github.com/Sonarr/Sonarr](https://github.com/Sonarr/Sonarr)

![](https://docs.usbx.me/uploads/images/gallery/2019-09/scaled-1680-/image-1568548187358.png)

***

## Initial Setup

In this section, we’ll be setting up Sonarr for the first time. This guide assumes that this is your first time installing Sonarr and you'll be storing your media locally, saving to `~/media`. We'll be doing the following:

1.  Enabling automatic organization and adding a root Folder
2.  Adding indexers
3.  Connecting your download clients
4.  Adding your first series

### Enabling Automatic Organization and Add Root Folder

* Access and login to your Sonarr instance using the credentials you set during installation
* Go to **Settings**

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581419597706.png)

* Make sure that advanced settings is set to **Shown** and click **Media Management**

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581419650980.png)

* Under Episode Naming section check Rename Episodes
  * You can leave the rest of the options as-is. The defaults work well with Plex's naming scheme.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581419756894.png)

* Under Importing section make sure that **Use hardlinks instead of copy** is checked
  * Hardlinks effectively creates a file that points directly to your source file in the disk. You can do anything to this file without affecting your source file and vice versa. This is useful when you're seeding from torrents.
    * This is to prevent to have 2 copies of the same movie without affecting your files.
      * If your root folder is located on a mount (eg using a rclone mount), you should set this to **No**.
        * Hardlinks does not work on mounts. Sonarr will resort to copying, which is prone to errors.
          * For this, consider using [Rclone VFS and MergerFS Setup](https://docs.usbx.me/books/rclone/page/rclone-vfs-and-mergerfs-setup)

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581419843155.png)

* Then on Root Folders, select **Add Root Folder**

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581420185797.png)

* This will bring up the File Browser window.
* Select `homexx` folder where `homexx` contains the node where your seedbox is in.
    *   In the screenshot, the node where the seedbox is in `home1`

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581420233225.png)

* Once opened, select your seedbox (indicated by your seedbox username)

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581420350002.png)

* Then select the media folder and select TV Shows. Click **OK** after.
  * This folder is generated upon receiving your seedbox. This is where you'll be saving your media.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581420399482.png)

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581427179448.png)

* Once that's done, click **OK**. You'll see the absolute path of the Root folder.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581432213121.png)

* Click **Save changes** to save your changes

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581432295172.png)

### Adding indexers

* Now click the Indexers tab (red box)
* Add an indexer by clicking the big plus button (Blue box) and input what is asked on each indexer you wish.
  * Depending on the indexer, it'll ask for your account credentials or a passkey. Refer to your indexer/tracker for more information on what to put.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581432442828.png)

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581432490163.png)

* Once that's done, click **save changes**.

### Adding Download Clients

* Now, click the Download client tab

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581939206720.png)

* To add your preferred client, click the big + button then select your preferred client.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581939312684.png)

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1581939369821.png)

- Be Sure to enable "Show Advanced settings" Using the Cog Icon in the top left hand side to show URL Base Field

#### Torrent Clients

##### Deluge

```
Host: {username}.{servername}.usbx.me
Port: 443
URL Base: /deluge
Password: As configured in UCP under Deluge
Category: tv-sonarr
Add Paused: NO
Use SSL: YES
```

##### rTorrent

```
Host: {username}.{servername}.usbx.me
Port: 443
URL Path: /RPC2
Username: {username}
Password: As configured in UCP under ruTorrent
Category: tv-sonarr
Add Stopped: NO
Use SSL: YES
```

##### Transmission

```
Host: {username}.{servername}.usbx.me
Port: 443
Username: {username}
Password: As configured in UCP under Transmission
Category: tv-sonarr
Add Stopped: NO
Use SSL: YES
```

#### Usenet Clients
##### SABnzbd

```
Host: {username}.{servername}.usbx.me
Port: 443
URL Path: /sabnzbd
API Key: As obtained from SABnzbd
Username: {username}
Password: Configured during SABnzbd setup
Category: tv
Use SSL: YES
```

##### Nzbget

```
Host: {username}.{servername}.usbx.me
Port: 443
URL Path: /nzbget
Username: {nzbget username}
Password: {nzbget password}
Category: tv
Add Paused: NO
Use SSL: YES
```

***

## Adding Your First Series

* To add a series, click **Series**

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1582644002305.png)

*   Then click **Add New Series**

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1582644075866.png)

* This page will be shown. Search and select the series that you wish to grab.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1582644111951.png)

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1582644201738.png)

* Once selected, you can change if you want to monitor the series for any new releases, your preferred quality profile, and the series type.
* Once that's done, you can click the green button to add it to your Sonarr.
  * If you want to immediately search for the series in your indexers, check Start search for missing episodes.

![](https://docs.usbx.me/uploads/images/gallery/2020-02/scaled-1680-/image-1582644649509.png)

***

## Troubleshooting Information

**Why is Sonarr down with application error 502? It won't come back!**

If your Sonarr is reporting 502 and you have followed all the instructions on the error page (restarting, then upgrading if that fails), then something else is going on. All troubleshooting from here requires you to access your [SSH terminal](https://docs.usbx.me/books/secure-shell-%28ssh%29/page/how-to-connect-to-your-ultraseedbox-slot-via-ssh).

* If you use mergerfs in conjunction with Sonarr or Radarr, first ensure your mono instance is not defunct with `ps aux | grep defunct`. If it's defunct, killing your mounts will release the process, and you will be able to restart Sonarr/Radarr. Rclone cloud mounts should not be used directly with any application. MergerFS should be used.
* Have you been into the system settings of Sonarr recently and use a password manager? Your password manager may have auto-filled the port. The ports should not be modified as they are just the internal docker ports, and SSL is handled via nginx. Please check the ports in the applications config.xml with the following command:

```sh
cat .apps/sonarr/config.xml | grep Port
```

Sonarr output should look like this:

```sh
support@server:~$ cat .apps/sonarr/config.xml | grep Port
  <Port>8989</Port>
  <SslPort>9898</SslPort>
```

If they report other values, then use a text editor on `config.xml` and change to the port displayed above.

***

## Extra Guides

### Remote Path Mapping

In this guide, we'll be setting up Sonarr/Radarr to communicate to plex so that a plex scan occurs finding only the new downloads. This guide assumes the following:
•	You have a working Sonarr/Radarr
•	You have a working Download client installed and running on your Ultra.cc Slot, that is connected to sonar/radarr
•	Have MergerFS Mount setup and working correctly
•	Have the rclone upload script included in the docs up and running.

#### Create Folder Structure
Both Sonarr and Radarr offer an option called remote path mapping. Think of this as a shortcut between a local path in this case your Ultra.cc Slot and a Remote path where downloads are stored for processing, this could be another server or a cloud mount, In our case we will be using a MergerFS mount as our remote path, this has the effect of instantaneous media management.
So, the first steps are to create a download folder, we will create a Folder for both Torrent downloads and Usenet downloads
Deluge/Torrent Clients

`mkdir -p ~/Stuff/Local/Downloads/torrents/Deluge/`
This could be changed at the end to rutorrent transmission or any other client you may be using
Login via SSH to confirm your full download path.

`cd ~/Stuff/Local/Downloads/torrents/Deluge `

`pwd`

This will display a path like this
`/home3/usbdocs/Stuff/Local/Downloads/torrents/Deluge`

Proceed to set your Torrent Client to the same download path as you’ve just created.


![](https://i.imgur.com/RO4Ng1K.png)

ensure your download client is linked to your sonar/radarr with similar settings to these
![](https://i.imgur.com/sPHGddj.png)
![](https://i.imgur.com/0azOBxx.png)

#### NZB Downloaders

Now lets make one for NZBdownloads in this case NZBget

`mkdir -p  ~/Stuff/Local/Downloads/usenet/Sonarr`


`mkdir -p  ~/Stuff/Local/Downloads/usenet/Radarr`

NZB downloaders work a little differently so your need to make Categories for both sonarr and radarr  and point them to the respective folders like so

Login via SSH to confirm your full download path.
`cd ~/Stuff/Local/Downloads/usenet/Sonarr`
`pwd`
This will display a path like this

`/home3/usbdocs/Stuff/Local/Downloads/usenet/Sonarr`
For Radarr
`/home3/usbdocs/Stuff/Local/Downloads/usenet/Radarr`
Add these Categories to NZBget by navigating to the web UI, Click Settings at the top of the page and then Categories on the left hand side

![](https://i.imgur.com/eTp97BL.png)

![](https://i.imgur.com/0QMxbxB.png)

Be sure to scroll to the bottom and save.

#### Edit Upload script/Systemd/Bash Upload


We now need to tell rclone to ignore our Downloads and only touch Stuff/Local. Be sure to follow this or your end up being api banned for seeding from the cloud drive.

Original script can be found here:
https://raw.githubusercontent.com/ultraseedbox/UltraSeedbox-Scripts/master/MergerFS-Rclone/Upload%20Scripts/rclone-upload.sh

![](https://i.imgur.com/Gs6wIEq.png)

You need to add the `--exclude "Downloads/**" \` flag
The script will now look like this:

![](https://i.imgur.com/VjrgnKY.png)

#### Systemd

```
[Unit]
Description=RClone Uploader

[Service]
Type=simple

ExecStart=/home6/usbdocs/bin/rclone move /home6/usbdocs/Stuff/Local/ gdrive: \
    --config=/home6/kbguides/.config/rclone/rclone.conf \
    --drive-chunk-size 8M \
    --tpslimit 1 \
    --drive-acknowledge-abuse=true \
    -vvv \
    --delete-empty-src-dirs \
    --fast-list \
    --bwlimit=2M \
    --use-mmap \
    --transfers=1 \
    --checkers=1 \
    --drive-stop-on-upload-limit \
    --log-file /home6/kbguides/scripts/rclone-uploader.log
Restart=on-failure

[Install]
WantedBy=default.target
```

Just like the script above you can simply add `--exclude "Downloads/**" \` under `--config`

```
[Unit]
Description=RClone Uploader

[Service]
Type=simple

ExecStart=/home6/usbdocs/bin/rclone move /home6/usbdocs/Stuff/Local/ gdrive: \
    --config=/home6/kbguides/.config/rclone/rclone.conf \
    --exclude "Downloads/**" \
    --drive-chunk-size 8M \
    --tpslimit 1 \
    --drive-acknowledge-abuse=true \
    -vvv \
    --delete-empty-src-dirs \
    --fast-list \
    --bwlimit=2M \
    --use-mmap \
    --transfers=1 \
    --checkers=1 \
    --drive-stop-on-upload-limit \
    --log-file /home6/kbguides/scripts/rclone-uploader.log
Restart=on-failure

[Install]
WantedBy=default.target
```

save the file and run `systemctl --user daemon-reload` then `systemctl --user restart --now rclone-uploader.service`


### Configuring Sonarr/Radarr to use the remote mapping functions

Go to Settings => Download Clients

Scroll all the way down where you see Remote Path Mappings and click on the plus sign as pictured here.
![](https://i.imgur.com/VVXsBSj.png)
`Host: lwxxx.usbx.me/username.lwxxx.usbx.me (Must be the same one as your download client)`

`Remote Path:/home3/usbdocs/Stuff/Local/Downloads/torrents/Deluge (Path where torrent client is pointed)`

`Local Path:/home3/usbdocs/MergerFS/Downloads/ (path where Sonarr will look for downloads)`

Enable Hardlinking in Media Management as pictured here:
![](https://i.imgur.com/aGrCGQV.png)




### Backing Up and Restoring Sonarr

In this section, we'll be showing you how to backup and restore Sonarr v3.

#### Backing Up Sonarr

* Log into your Sonarr instance
* In System -> Backup, click Backup Now. This will create a zip containing your backup.

![](https://docs.usbx.me/uploads/images/gallery/2020-05/image-1590401915286.png)
![](https://docs.usbx.me/uploads/images/gallery/2020-05/image-1590401971684.png)

* Click your newly created backup to download it to your PC.

#### Restoring Sonarr

* On your newly installed Sonarr instance, go to System -> Backup
* Click Restore backup.

![](https://docs.usbx.me/uploads/images/gallery/2020-05/image-1590402217230.png)

* A window appears. Click Choose file and navigate to your Sonarr backup.

![](https://docs.usbx.me/uploads/images/gallery/2020-05/image-1590402363661.png)

* Once selected, click Restore and wait for a few moments.

![](https://docs.usbx.me/uploads/images/gallery/2020-05/image-1590402429481.png)

* Go back to the UCP then set a new password on Sonarr. Once it's set, login again and check all of your settings to make sure that it restored properly.
