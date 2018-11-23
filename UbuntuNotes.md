# Ubuntu(Linux) Notes

## Contents
- [Trouble shooting](#trouble-shooting)
   - [Can't shutdown or reboot properly](#cant-shutdown-or-reboot-properly)
   - [Can't suspend (xps-15)](#cant-suspend-xps-15)
   - [DNS_PROBE_FINISH_BAD_CONFIG error on chrome](#dns-probe-finish-bad-config-error-on-chrome)
- [Backup linux](#backup-linux)
   - [Generate the backup file](#generate-the-backup-file)
   - [Recover from the backup file](#recover-from-the-backup-file)
   - [Using Cron Job to make backups automatically](#using-cron-job-to-make-backups-automatically)
   - [Upload to Google Drive](#upload-to-google-drive)
- [Install bash](#install-bash)
   - [Dual system installation](#dual-system-installation)
   - [Install install .sh files](#install-install-sh-files)
   - [Yes to all during the installation](#yes-to-all-during-the-installation)
- [Bluetooth device connection](#bluetooth-device-connection)
   - [Connect from `bluetoothctl`](#connect-from-bluetoothctl)
   - [Logitech Anywhere 2S can't connect with bluetooth](#logitech-anywhere-2s-cant-connect-with-bluetooth)
- [SSH settings](#ssh-settings)
   - [ssh login without passwords](#ssh-login-without-passwords)


## Trouble shooting
            
### Can't shutdown or reboot properly
  - Ubuntu 16.04 hangs on shutdown/restart, requires pressing and holding the power key to turn the machine off.
   <br/> Try [this][5]:
     1. Go to `/etc/default/grub`
     2. Edit this line:
        ```
        GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
        ```
     3. To this line:
        ```
        GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi=force"
        ```
     4. Then run `update-grub` 
   
    
  <br/> __However, for my Dell-XPS15 the problem was fixed by [this solution][6].__
        
     the problem was caused by drivers: I managed to install the NVIDIA drivers from terminal 
     usingsudo ubuntu-drivers autoinstall er
  <br/> After `sudo ubuntu-drivers autoinstall`, this __Warning__ poped up:
     
     W: Possible missing firmware /lib/firmware/i915/kbl_guc_ver9_14.bin for module i915
     W: Possible missing firmware /lib/firmware/i915/bxt_guc_ver8_7.bin for module i915re 
     
   This [__answer__][7] right here should help!
     
### Can't suspend (XPS-15)
  After installing the NVIDIA driver, the shutdown and reboot problem were solved. But now the problem is unable to wake from suspend. The problem is the same as [__this discusss__][8] on NVIDIA webpage. The problem seems to be caused by Intel pci-bridge and there is no proper solution so far. <br/>
  <br/> However, the problem of unable to hibernate is solved on [__this post__] (this post doesn't solve the suspend though). So what I did is change all the suspend command into hibernate, like when closing the lid or inactivate for some time.Here is how to do it:
  <br/> Edit this file
  ```
  /etc/systemd/logind.conf  
  ```
  <br/> __Remove the `#`__ and change the lines into this
  ```
  HandleLidSwitch=hibernate
  HandleSuspendKey=hibernate
  ```
   <br/> We can also use hybrid-sleep instead of hibernate. With faster waking time, the hybrid-sleep will consum more energy though.
  
### DNS_PROBE_FINISH_BAD_CONFIG error on chrome
In my case, it only happens to certain wifi router. The connection go ons and offs for like a couple week, then it totally crashed and show `DNS_PROBE_FINISH_BAD_CONFIG` for some sites (facebook and outlook still work for some reason).
The fix is just add `8.8.8.8` to your DNS setting:
1. `sudo vim /etc/resolv.conf` for temporary setting or `sudo vim /etc/resolvconf/resolv.conf.d/head` to set permanently
2. Then add these to line at the bottom of the file:
   
   ```
   nameserver 8.8.8.8
   nameserver 8.8.4.4
   ```

3. Restart the network-manager:
   ```
   sudo service network-manager restart
   ```

__Sources__:[stack overflow][sf]

         
 [6]:https://askubuntu.com/questions/882410/ubuntu-16-10-wont-shutdown
 [7]:https://askubuntu.com/questions/832524/updated-kernel-to-4-8-now-missing-firmware-warnings
 [8]:https://devtalk.nvidia.com/default/topic/1017185/linux/problem-with-resume-from-suspend-ubuntu-16-04-gt-940mx-/1
 [9]:https://devtalk.nvidia.com/default/topic/969433/-quot-solved-quot-suspend-resuming-and-wakeup-with-nvidia370-28/
 [sf]:https://stackoverflow.com/questions/32045682/dns-probe-finished-bad-config-error       

## Backup linux 
### Generate the backup file
It's easy to do the backup on linux
  ```  
   tar -cvpzf backup.tar.gz --exclude=/proc --exclude=/lost+found --exclude=/backup.tgz --exclude=/mnt --exclude=/sys /
  ```
The last `/` means what (where) do you want to back up. And if you don't want to compress it then it will just be a __tar__ rather than a __tar ball__.
<br/> And the following table is what they stands for:

  | arguments | meaning |
  | :---: | :---: |
  | 'c' | create new file (overwrites old file) |
  | 'v' | verbose, letting you know what's going on on terminal |
  | 'p' | preserving permissions for all the files |
  | 'z' | compression the file (not like windows, nothing bad would happen) |
  | 'f' | allow to set file names for the backup |

### Recover from the backup file
  
  ```  
   sudo tar -xvpzf TARFILE -C /RECOVERY_DIRECTORY
  ```
After the __capital C__ is the directory where you want to extract this tar-ball to.

  | arguments | meaning |
  | :----: | :---: |
  | 'x' | extract the tar file |
  | 'C' | this argument (in capital) is behind the tar file, <br/> to extract in different directory |


### Using Cron Job to make backups automatically

To edit the Crontab file:
  
  ```
  sudo crontab -e
  ```
  | arguments | meaning |
  | :---: | :---: |
  | 'e' | edit the  current  crontab  using  the  editor specified |
  | 'r' | causes the current crontab to be removed |
  | 'l' | causes the current crontab to be displayed on standard output |
 
You will be asked to choose an editor upon editing for the first time.
<br/> The format would be : 

  ```
  minute (0-59), hour (0-23, 0 = midnight), day (1-31), month (1-12), weekday (0-6, 0 = Sunday), command
  ```
  
Examples:

  ```
  # m h  dom mon dow   command
  # backup every day at 10:30
  30 10 * * * sudo tar -cpzf /home/liuyc/backupfolder/backup_moby.tar.gz /home/liuyc/moby_*
  ```
source vedio:[check this out !][tar]

[tar]:https://www.youtube.com/watch?v=hGqjM9Wz-pU

### Upload to Google Drive
#### Install gdrive
```
sudo wget -O /usr/bin/gdrive "https://docs.google.com/uc?id=0B3X9GlR6EmbnQ0FtZmJJUXEyRTA&export=download"
sudo chmod +x /usr/bin/gdrive
```
After the installation, use `gdrive about` to authorize __gdrive__ your account. (*remove the `~/.gdrive`  if not using for security purpose*)

#### Upload using gdrive
1. First use `gdrive list` to get the __ID__ for the directory you want to upload to.
2. Using this command to upload, add to a bash file for crontab to execute:
   ```
   #!/bin/bash   PATH=/opt/ros/kinetic/bin:/home/liuyc/bin:/home/liuyc/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
   sudo gdrive upload --parent --recursive 1hFb8GS0UvYFgUGBbywHszF0eTVjVWL-l "/home/liuyc/backupfolder"
   ```
   Using `--recursive` to upload a directory. Add `PATH` at the begining to add `gdrive` in path. (See this [discussion][gdrive_dis]) 
   
Add this line to `sudo crontab -e` to upload automatically:
```
25 10 * * * sudo /home/liuyc/backupfolder/upload_gdrive.sh
```
For more usage of `gdrive`, check [original github repo][gdrive_repo].

[gdrive_repo]:https://github.com/prasmussen/gdrive
[gdrive_dis]:https://github.com/prasmussen/gdrive/issues/151

## Install bash
  
  ### Dual system installation
  - Win10/Ubunt16.04 Installation fail doing manual partition : can't find any disks
  ```
   1. Run Command Prompt as Admin
   2. Invoke a Safe Mode boot with the command: bcdedit /set {current} safeboot minimal
   3. Restart the PC and enter your BIOS during bootup.
   4. Change from IDE to AHCI mode then Save & Exit.
   5. Windows 10 will launch in Safe Mode.
   6. Right click the Window icon and select to run the Command Prompt in Admin mode from among the various options.
   7. Cancel Safe Mode booting with the command: bcdedit /deletevalue {current} safeboot
   8. Restart your PC once more and this time it will boot up normally but with AHCI mode activated.
   9. Bask in the reflected glory of being a total Windows 10 God 
  ```
  source : see [this][3] and [this][4]
  
  ### Install install .sh files
  - Use `bash` command
  ```
  sudo bash install.sh
  ```
  - Make the file executable
  ```
  chmod +x install.sh
  sudo ./install.sh
  ```
  
  ### Yes to all during the installation
  ```
  yes "yes" | script.sh
  ```
  This can also work removing files or other command with Y/N
  ```
  yes "yes" | rm -i file1 file2 file3
  ```

## Bluetooth device connection
  ### Connect from `bluetoothctl`
  This is modified from [ArchWiki Bluetooth][1] and [ArchWiki Bluetooth Headset][2].
  ```
  # bluetoothctl
  ```
  After greeted by its internal command prompt, enter:
  ```
  # power on
  # agent on
  # default-agent
  # scan on
  ```
  Make sure the device is in paring mode, it should be discovered shortly, for example:
  ```
  [NEW] Device 00:1D:43:6D:03:26 Name_Of_The_Divice
  ```
  shows a device that calls itself "Lasmex LBT10" and has MAC address 00:1D:43:6D:03:26. We will now use that MAC address to initiate the pairing:
  ```
  # pair 00:1D:43:6D:03:26
  ```
  Some devices require passkey to pair, type the passkey on the device, for example:
  ```
  [agent] Confirm passkey 680044 (yes/no): yes
  ```
  Just type `680044` and it will pair sucessfully.<br/>
  After pairing, you also need to explicitly connect the device (every time?):
  ```
  # connect 00:1D:43:6D:03:26
  ```
  > If everything works correctly, you now have a separate output device in PulseAudio. Note: The device may be off by default. Select its audio profile (OFF, A2DP, HFP) in the "Configuration" tab of pavucontrol.
    You can now redirect any audio through that device using the "Playback" and "Recording" tabs of pavucontrol.
  
  If you trust the device and want it to be connected automatically(whenever your device is on), open `/etc/bluetooth/main.conf` with vim, edit the following line:
  ```
  [Poicy]
  AutoEnable = true
  ```
  Then go back to `bluetoothctl` enter this line:
  ```
  trust 00:1D:43:6D:03:26
  ```
  
  You can now disable scanning again and exit the program:
  ```
  # scan off
  # exit
```
### Logitech Anywhere 2S can't connect with bluetooth
Use `bluetoothctl` to start the setting.
</br> Then try this
```
[bluetooth]# power off
[bluetooth]# power on
[bluetooth]# scan on
[bluetooth]# connect XX:XX:XX:XX:XX:XX
[Arc Touch Mouse SE]# trust
[Arc Touch Mouse SE]# connect XX:XX:XX:XX:XX:XX
[Arc Touch Mouse SE]# pair
[Arc Touch Mouse SE]# unblock
[Arc Touch Mouse SE]# power off
[bluetooth]# power on
```
It should work after this. If the error shows: `No default controller available`, you can check if anything is wrong by `systemctl status bluetooth`.Then try:
```
sudo systemctl start bluetooth
```

(check these pages for more detail:[connect to anywhere 2s][anywheresolver], [solving no_controller][bluetooth])

[anywheresolver]:https://askubuntu.com/questions/741330/how-do-i-get-logitech-mx-anywhere-2-to-work-in-16-04-bluetooth-smart
[bluetooth]:https://forums.bunsenlabs.org/viewtopic.php?id=4375

## SSH settings
 ### ssh login without passwords
 __On machine A:__ (client)
 <br\>Generate the rsa-key, for any pup-up question, just press `enter`
 ```
 ssh-keygen
 ```
 then use `vim` to get the `id_ras`
 ```
 vim id_ras.pub
 ```
 __On machine B:__ (server)
 <br\>create a file called `authorized_keys`
 ```
 touch authorized_keys
 ```
 then paste the id_ras of machine A into this file
 
 __Faster version__
 ```
 ssh-keygen -t rsa
 scp id_rsa.pub server_hostname:~/.ssh/
 ssh server_hostname
 cat .ssh/id_rsa.pub >> .ssh/authorized_keys
 ```
 to get more info, check out [this][ssh_1] and [this][ssh_2]
  
  
  [1]:https://wiki.archlinux.org/index.php/bluetooth
  [2]:https://wiki.archlinux.org/index.php/Bluetooth_headset
  [3]:https://www.tenforums.com/drivers-hardware/15006-attn-ssd-owners-enabling-ahci-mode-after-windows-10-installation-5.html
  [ssh_1]:http://www.linuxproblem.org/art_9.html
  [ssh_2]:https://blog.longwin.com.tw/2005/12/ssh_keygen_no_passwd/
  [4]:https://askubuntu.com/questions/696413/ubuntu-installer-cant-find-any-disk-on-dell-xps-13-9350
  [5]:https://askubuntu.com/questions/764568/ubuntu-16-04-hangs-on-shutdown-restart
  
