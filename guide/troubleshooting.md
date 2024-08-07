<img align="right" src="https://github.com/govro150/woa-pong/blob/main/pong.png" width="350" alt="Windows 11 running on pong">

# Running Windows on the Nothing Phone (2)

## Troubleshooting Issues
> Below you will find a list of common problems and their solutions

## Cannot mount Windows in Android
If mounting Windows produces an empty folder, you either don't have Windows installed, or your rom does not have mount support.

##### Finished!

## Cannot write to Windows in Android
> This is caused by shutting down Windows instead of restarting it.
- To solve this, boot to Windows and then press "restart", then as the screen shuts off boot to TWRP and from there load up Android.
- Or, disable hibernation in Windows. 
> Alternatively, if you have already set up the Switch to Android app, simply use this to switch to Android.

##### Finished!

## USB does not work
Enable USB host mode using the optional [post install guide](materials.md#toggling-usb-host-mode).

##### Finished!

## DISM Error:87 The add-driver option is unkown
This usually means that you have an unclean Windows image with some other drivers. You need to get a clean Windows image (which means you didn't follow instructions).

##### Finished!

## 0xc000021a BSOD
This usually means that winlogon.exe has failed, and you may need to reapply the Windows image.

##### Finished!

## The computer restarted unexpectedly or encountered an unexpected error
If you stumble upon this error, you may need to redeploy the Windows image. Use the [reinstall guide](https://github.com/Project-Silicium/WoA-Guides/blob/main/Mu-Qcom/OS/Windows/Win.md#installing-step-3) for this.

##### Finished!

## INACCESSIBLE_BOOT_DEVICE BSOD
This Blue Screen of Death likely means some broken driver installation. To fix this, reinstall the drivers using the [reinstall guide](https://github.com/Project-Silicium/WoA-Guides/blob/main/Mu-Qcom/OS/Windows/Win.md#installing-step-3).

##### Finished!



















