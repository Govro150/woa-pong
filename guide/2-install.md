<img align="right" src="https://github.com/govro150/woa-pong/blob/main/pong.png" width="350" alt="Windows 11 running on pong">

# Running Windows on the Nothing Phone (2)

## Installing Windows

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)
  
- [Modded OFOX](https://github.com/n00b69/woa-polaris/releases/download/Files/ofox.img)

- [UEFI image](https://github.com/n00b69/woa-polaris/releases/tag/UEFI)

### Boot to OFOX recovery
> If your recovery has been replaced by the stock recovery, flash it again using
```cmd
fastboot flash recovery path\to\ofox.img reboot recovery
```

#### Enabling mass storage mode
> If it asks you to run it once again, do so
```cmd
adb shell msc
```

### Diskpart
> [!WARNING]
> DO NOT ERASE, CREATE OR OTHERWISE MODIFY ANY PARTITION WHILE IN DISKPART!!!! THIS CAN ERASE ALL OF YOUR UFS OR PREVENT YOU FROM BOOTING TO FASTBOOT!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for taking the device to Xiaomi or flashing it with EDL, both of which will likely cost money)
```cmd
diskpart
```

#### Selecting the Windows partition
> Use `list volume` to find it, replace **$** with the actual number of the Windows volume (it should be around the same size you picked on the last page)
```diskpart
select volume $
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Formatting Windows drive
```cmd
format quick fs=ntfs label="WINPOLARIS"
```

#### Selecting the ESP partition
> Use `list volume` to find it, replace **$** with the actual number of the ESP volume (it should be around 286MB)
```diskpart
select volume $
```

#### Add letter to ESP
```cmd
assign letter y
```

#### Formatting ESP drive
```cmd
format quick fs=fat32 label="ESPPOLARIS"
```

#### Exit diskpart
```cmd
exit
```

### Installing Windows
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file

> If it asks you to enter a letter, enter the drive letter of **WINPOLARIS** (which should be **X**), then press enter

> [!WARNING]
> DO NOT USE DISM++
  
#### Create Windows bootloader files
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

### Unassign disk letters
> So that they don't stay there after disconnecting the device
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace "$" with the actual number of **WINPOLARIS**
```diskpart
select volume $
```

#### Unassign the letter X
```diskpart
remove letter x
```

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace "$" with the actual number of **ESPPOLARIS**
```diskpart
select volume $
```

#### Unassign the letter Y
```diskpart
remove letter y
```

#### Exit diskpart
```diskpart
exit
```

### Reboot to fastboot
> Hold **volume down** + **power** to force reboot your phone into fastboot mode

### Fixing touch
> Replace `path\to\devcfg-polaris.img` with the actual path to the image
```cmd
fastboot flash devcfg_ab path\to\devcfg-polaris.img
```

### Booting Windows
> Replace `path\to\firstboot.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\firstboot.img
```

> [!Important]
> After Windows boots and you've completed the Windows setup, press **Restart** in the start menu to boot back to Android for the last step

## [Last step: Setting up dualboot](/guide/dualboot.md)

















