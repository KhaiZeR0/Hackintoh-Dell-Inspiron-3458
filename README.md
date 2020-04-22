# Hackintosh-Dell-Inspiron-3458
Hackintosh on Dell inspiron 3458
## Laptop Specs
- Intel Core i3 5005u (Broadwell)
- GPU intel HD 5500
- Ram 4GB
- WIFI AC 3160 (Replace Later)
- Audio ALC 255
- Ethernet RL8100
## Working
- Native Power Management
- USB ports
- Battery status
- Keyboard & TrackPad
- Internal Audio & Microphone
- Headphone Jack
- HDMI Port
- Graphics (Brightness Control)
- Sleep/Wake
- Ethernet
- Battery
- Bluetooth
- Icloud/Facetime/imessage
## Not Working
- SD card reader (untest)
- Wifi with continuity features (Intel card not support)

![info](https://user-images.githubusercontent.com/54585187/78202425-80b25300-74be-11ea-846d-3c16924c3772.png)

## Pre Condition

**Bios configuration**
Bios Config | Setting 
:---:| :---:
Intel SpeedStep | Enabled
Virtualization    | Disabled
USB Wake Support | Disabled
SATA Operation | AHCI


## 1. Change DVMT settings

Update your Bios to Lastest

## IMPORTANT: DO THIS STEP CAREFULLY

1. Launch Universal BIOS Backup ToolKit 2.0.exe

2. Press Read, when Finsh, Click on backup, save as *.rom

3. Launch Launch UEFITool.ext

4. Click File, open image file, browse to *.rom file

5. Click File -> Search by GUID (899407d7-99fe-43d8-9a21-79ec328cac21)

6. Double-click on GUID (Example: GUID pattern "899407d7-99fe-43d8-9a21-79ec328cac21" found as "D7079489FE99D8439A2179EC328CAC21" in 899407D7-99FE-43D8-9A21-79EC328CAC21 at header-offset 0h Pattern)

7. Expand until you see PE32 image section

8. Right click on and extract PE32 image section->Extract Body (save as *.bin file)

9. Launch Universal IFR Extractor.exe and browse to *.bin file

10. Extract and save as *.txt file.

11. Open *.txt file with Notepad (Search for DVMT)

(For example my Pre-Allocated are 0x15B, 0x15C, 0x15D but 0x15B and 0x15C are need to changed to 0x3)

12. Format USB as Fat32 and Copy EFI shell into it (Change EFI Shell name into EFI)

13. Boot with USB

14. At the grub prompt, enter these commands, hit enter after command, then exit and reboot

Example: Setup_var 0x15B 0x3

(To verify if the value was updated, just enter setup_var 0x15B and hit enter, the value will be listed
More detailed instruction in attachment)

## And now you have successfully changed the DVMT settings and fixed the kernel panic for graphics

## 2. Create OSX Installer
(I will use Olarila High Sierra with my custom EFI folder)

** Note: Apfs.efi and HFSplus.efi for some reason it will make clover blackscreen so Please detele it (replace with VboxHFS.efi or you can use my EFI folder) and if you wanna use mojave or newest, pls use HFS patch to continued

 1. Download High Sierra From Olarila [here](https://drive.google.com/file/d/1wjy6rU0sDLN_Lav8KE6gKT9vr9mOUpMg/view "Here")
 
 2. Download [this](https://www.balena.io/etcher/ "this")
 
 3. Extract the .raw image
 
 4. Open Etcher, select image, select Drive and flash (Use USB 16GB or higher)
 
 ![Etcher](https://user-images.githubusercontent.com/54585187/78206356-cc69fa00-74c8-11ea-87d4-f380bd9d2b66.gif)

## 3. Install OSX

1. When Clover boot screen appears, choose Install OS High Sierra

2. The system will then boot into the OS X Installer

3. For a new installation of OS X, you MUST erase and format the destination drive according to the following steps before continuing.

   a. From the menu bar, click Utilities -> Choose Disk Utility
   
   b. Highlight your target hard drive for the High Sierra installation in left column.
   
   c. Click Erase tab
   
   d. Under Scheme: GUID Partition Map
   
   e. Under Name: type HD (You can name anything you want)
   
   f. Under Format: choose Mac OS Extended (Journaled)
   
   g. Click Erase
   
   h. Close Disk Utility

4. For some old HIgh Sierra installer, you will get this error (Mac OS X could not be installed) so you have to change date to 2017 to contined (Disable Internet needed)

   a. Form the menu bar, click Utilities -> Choose Terminal
   
   b. Form terminal, type (Date -u 1111111117), it will show time updated to 2017
   
   c. Exit and continued install MacOS
   
5. After installed successfull, copy your EFI folder from your USB to Hard drive and ready to go :)

## IF you wanna ask something: 
- [Olarila](https://www.olarila.com "Olarila") Website
- [Olarila](https://www.facebook.com/groups/122585311156411 "Olarila") Facebook group
- If you are VietNamese you can go to this [group](https://www.facebook.com/groups/224780132268974/?ref=share "group")
