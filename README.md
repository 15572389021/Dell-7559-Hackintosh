### This is a guide for install MacOSX on Dell 7559 Laptop
In this guide, all operation take my Dell 7559 as exmaple, APCI files(SSDT and APCI fixed in clover may not compatible with your hardware, be careful to using them, repatch in need).
  1. CPU: i5-6300HQ (Skylake,6th)      Mem:  4G DDR3, in one slot
  2. Graphic: Intel HD Graph 530 + Nvida GTX960M
  3. Display: 1920x1080 FHD screen     Disk: 128G SSD + 500G HDD
##### Before Start：
    1. There's something must noticed:
        A. The i7 edition is easy to make Hackintosh
        B. The i5 editon is hard to boot frome UEFI Clover
    2. There's Something you must have and keep for long time on you Hackintosh way
        A. noun  B. patience  C. time  D. learning skill

### Prepare: 
##### 1.Understand your hareware:
- Have a look into Laptop Guide from manufacturer
- Check hardware on the normal running Operation Systme（Windows/linux，etc.）
- List and record hardware details
##### 2. Download files:
- Get a working Mac OSX and download installer image from Mac app stroe
- Create bootable USB installer with Clover follow this [thread](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/).
- Format usb disk into GPT disk, operate in terminal:
```zsh 
$crackselfs-MBP:~ crackself$ diskutil list
/dev/disk0 (internal, physical):
#:       TYPE NAME\                                   SIZE       IDENTIFIER
0:       GUID_partition_scheme                        *128.0 GB  disk0
1:                        EFI EFI                     209.7 MB   disk0s
2:         Microsoft Reserved                         16.8 MB    disk0s2
3:       Microsoft Basic Data Windows                 63.8 GB    disk0s3
4:                  Apple_HFS Mac                     63.3 GB    disk0s4
5:                 Apple_Boot Recovery HD             650.0 MB   disk0s5
 
/dev/disk2 (external, physical):
#:                       TYPE NAME                   SIZE      IDENTIFIER
0:       GUID_partition_scheme                        *15.6 GB   disk2
1:                        EFI EFI                     209.7 MB   disk2s1
2:       Microsoft Basic Data                         15.2 GB    disk2s2
```
For example, `/dev/disk2` is my usb disk.

- Format it as one GPT partiton whit EFI partiton in Terminal:
```ash
diskutil partitionDisk /dev/disk2 1 GPT HFS+J "install_osx" R
```
##### 3.Write installer inamge into usbdisk
For Hight Sierra(10.13.x):
```bash
sudo "/Applications/Install macOS High Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
```
For Sierra(10.12.x):
```bash
sudo "/Applications/Install macOS Sierra.app/Contents/Resources/createinstallmedia" --volume /Volumes/install_osx --applicationpath "/Applications/Install macOS Sierra.app" --nointeraction
```
For El Capitan(10.11.x):
```bash
sudo "/Applications/Install OS X El Capitan.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --applicationpath "/Applications/Install OS X El Capitan.app" --nointeraction
```
##### 4.rename usb disk as 'install_osx'
 - Noticed: Dell 7559 with Skylake cpu, OS support from 10.11
##### 5. Install Clover into usb EFI partition:<br>
Here suggest using [origin installer](https://sourceforge.net/projects/cloverefiboot/).<br>

##### A.UEFI boot:
###### check all this:
    Only install UEFI
     Theme
       BGM
    install in EFI partition
     Drivers64UEFI
       AptioMemoryFix
##### B.UEFI and Legacy clover boot:
###### check all this:>
    Install in EFI partition
    Theme
      BGM
    Bootloader
      Bios boot0af
    CloverEFI
      CloverEFI 64bit BiosBlockIO
    Drivers64UEFI
      AptioMemoryFix

- Noticed: UEFI & Legacy clover Boot model suggeste for this Laptop with i5-6300HQ CPU .
##### 6.replace universal config.plist files frome RehabMan,place need kexts into Clover/Kext/Ohters.

Postinstall:
-
#### About save backlight level:
install clover into SSD HDD EFI partiton as well as operate on installer,but check install RCscripts in target partiton, This afect store your backlight level.<br>

### Need kextx instalation position:
Due to kextcache reason, some kext cann not work when install in S/L/E. Noticed by RehabMan, you need to install them into L/E<br>

### Before install kexts into final position:
Do make sure they are the lasted released, compare with RehabMan's.

##### Others:
Using my Clover files to test, if your hardware do not work perfect, Repatch your APCI files and check kexts, in additon, RehabMan suggest Kest install into L/E, 'rebuild kextcache' wiht comandline "sudo kextcache -i /".

##### Get hardware work normally:<br>
Graphic<br>
Audio:<br>
Wi-Fi card<br>
Ethernet<br>
Keyboard and mouse<br>
Power Manager(Sleep and wake )<br>
....
