# Ubuntu(Linux) Notes

## Install bash
  
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
