# Ubuntu(Linux) Notes

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
  source : see [this][3]
  
  ### Install install.sh files
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

## Bluetooth Device Connection
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
  
  
  
  
  
  [1]:https://wiki.archlinux.org/index.php/bluetooth
  [2]:https://wiki.archlinux.org/index.php/Bluetooth_headset
  [3]:https://www.tenforums.com/drivers-hardware/15006-attn-ssd-owners-enabling-ahci-mode-after-windows-10-installation-5.html
