#  Dell Latitude 5290 2-in-1 UHD620 iGPU CLOVER

## Specifics

- CPU : Intel® Core™ i5-8350U Processor (6M Cache, up to 3.60 GHz)
- Graphics : Intel® UHD Graphics 620
- Sound : Realtek ALC3253 (ALC225)
- Display : 12.3 Inch 1920 X 1280 (WUXGA+) 3:2 10 Points Multi Touch
- Memory : Samsung LPDDR3 8GB 1867MHZ (4GB * 2 Dual Channel)
- SSD : TOSHIBA KXG60ZMV256G 256GB (2280), Western Digital PC SN520 NVMe SSD 512GB (2230)
- Wireless : BCM943602BAED(DW1830) (WWAN Slot * 1)
- External Port & Slot : USB 3.2 Gen 1  * 2, TYPE C * 2 (USB 3.2 Gen 1, Displayport, Power Delivery), I2C PORT * 1, Audio Jack * 1, Smart Card Reader * 1 USIM Slot * 1, Noble Wedge Lock Slot *1
- Battery : 42WHr
- Windows 10 Pro


## Bios/Clover Bootloader/macOS Version

- Bios : 1.7.3
- Clover Bootloader : Above v2.5k
- macOS : 10.14.x


## Bios Setup

- Load Optimized Defaults


## DSDT Patch

- [misc] Remove _PRW from LID
- [sys] AC Adapter Fix
- [sys] Add IMEI
- [sys] Fix _WAK Arg0 v2
- [sys] Fix Mutex with non-zero SyncLevel
- [sys] Fix PNOT/PPNT
- [sys] HPET Fix
- [sys] IRQ Fix
- [sys] OS Check Fix (Windows 10)
- [sys] RTC Fix
- [sys] Shutdown Fix
- [sys] Shutdown Fix v2
- [sys] SMBUS Fix
- [GPIO] GPIO Controller Enable [SKL+]


## Drivers64UEFI

- ApfsDriverLoader-64.efi
- AptioMemoryFix-64.efi
- FSInject-64.efi
- VBoxHfs-64.efi
- VirtualSmc.efi


## Kexts

- AirportBrcmFixup.kext
- AppleALC.kext
- BrcmFirmwareRepo.kext
- BrcmPatchRAM2.kext
- CodecCommander.kext
- EFICheckDisabler.kext
- Lilu.kext
- NullEthernet.kext
- SMCBatteryManager.kext
- SMCLightSensor.kext
- SMCProcessor.kext
- SMCSuperIO.kext
- USBPorts.kext    -    Hackintool generated, HS / SS port matching and realignment
- VirtualSMC.kext
- VoodooI2C.kext
- VoodooI2CHID.kext
- VoodooPS2Controller.kext    -    Edit VoodooPS2Trackpad.kext's plist (ProductID:1218, VendorID:044E)
- WhateverGreen.kext


## ETC

***After installation***
- Turn off FileVault2 (necessary)  
- Remove these boot flags  
    -v  
    debug=0x100  
    keepsyms=1
- Additional patches are required for iMessage and Facetime activation
- HiDPI 1920 * 1280 (3840 * 2560) can be added, but it requires more resources
- It is recommended that you do a new ACPI patch on your system

***Intel UHD Graphics 620***
- This build is compatible for 'Dell Latitude 5290 2-in-1' system uses iGPU of 'Intel UHD Graphics 620'  
  If your iGPU is not 'Intel UHD Graphics 620', additional graphics patches might be required

***Thunderbolt 3***
- This build is compatible for 'Dell Latitude 5290 2-in-1' system without 'Thunderbolt 3'  
For Thunderbolt 3 built-in model, it must repatch and regenerate DSDT.aml, SSDT-UIAC.aml, SSDT-USBX.aml, and USBPorts.kext  
Additional patches might be required for working Thunderbolt 3

***NullEthernet.kext & ssdt-rmne.aml***
- Null Ethernet is a way to prevent a Mac address-based license for some software from being broken when a wireless card is absent or replaced (including iCloud)  
  If you do not need to consider blocking software licenses by changing your Mac address, you can remove it

***Fn Key***
- 'Fn' + 'r' || PrtScr = F13
- 'Fn' + 's' = F14 (Brightness down)
- 'Fn' + 'b' = F15 (Brightness up)


## What Works

***Graphics/Display***
- Intel® UHD Graphics 620 QE/CI, 2048MB Vram
- Type C DP 2 ports Video / Audio output Hot Swap
- Brightness control
- Lid Close Sleep with Magnetic Travel Keyboard
- I2C touch screen Up to 4 points Gesture action (recognized as Magic Trackpad 2)

***Audio***
- Built-in speaker
- Built-in microphone
- Line input
- DP Audio Output

***Input***
- I2C touch screen Up to 4 points Gesture action (recognized as Magic Trackpad 2)
- I2C Keyboard (Magnetic Travel Keyboard) with Backlight
- Touchpad (Magnetic Travel Keyboard, recognized as mouse)
- Volume button, window button, power button

***Power Management***
- CPU/Speed Step
- Battery
- Type C PD 2 Ports Charging, PowerShare
- Sleep/Wake

***Storage Device***
- Full Size/ Type C USB 2.0, 3.0 Hot Swap
- m.2 NVME 2280/ m.2 SATA 2280 1 Slot and m.2 NVME 2230(2242)/ m.2 SATA 2230(2242) 1 Slot

***Wireless communication***
- iMessage/FaceTime/App Store
- Wi-Fi, Bluetooth, Airdrop, Continuity with macOS compatible wireless card


## Issues
- If USB device is connected to Full size USB port with power connected state, it wakes up immediately after sleeping  
  Fixed after Full size USB port as internal port  
  As a result, if you connect a device above USB 3.0 to the Full size USB port, it will be recognized as an internal disk icon

- When the battery is in use, the disk not ejected properly after sleeping  
  Fixed with SafeSleepUSB.app or Jettison.app

- WWAN communication via WWAN card, USIM, and Legacy_Sierra_QMI.kext is feasible, but has not been tested yet

- If wired USB LAN is connected with power connected state, it wakes up immediately after sleeping.

- Wireless Communication - DW1830(BCM943602BAED) is not recommended on this model  
  &ensp; Issues 1 : When the battery is in use, bluetooth not works properly after sleep  
  &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; It needs to reinstall the Bluetooth driver on Windows to get back to normal  
  &ensp; Issues 2 : If check 'Wake for Wi-Fi network access', wifi speed will be very slow after sleep  
  DW1560(BCM94352Z) will be tested soon

- MicroSD slot not working properly  
  If you use modified Sinetek-rtsx.kext, you can use HFS + formatted SD card, but there are still some problems

- I2C front and rear camera (AVStream2500, OV5670, OV8858) not recognized

- Compared to Windows, white noise occurs a little on speakers

- In case of new installation, Magic Trackpad 2 touch screen via VoodooI2C, VoodooI2CHID is not immediately recognized and suddenly recognized after specific setup / injection event after personal setting  
  Once recognized, the touch screen will not be lost  
  After recognized the touch screen, the touch pad of the Magnetic Travel Keyboard is disabled, which can be activated using Karabiner

- 3:2 resolution HiDPI of under 1913 * 1275 (3825 * 2550) not works through known method

- FileVault2 not works

## Screenshots

![01SystemOverview](https://user-images.githubusercontent.com/46496967/60284881-9ac76f80-9947-11e9-9127-c1dde7dc62b0.png)

![02SystemDisplay](https://user-images.githubusercontent.com/46496967/60283632-9cdbff00-9944-11e9-88d5-adb758d4b514.png)

![03VideoProc](https://user-images.githubusercontent.com/46496967/60283640-a1081c80-9944-11e9-979e-c31ffce3ceab.png)

![04IntelPowerGadget](https://user-images.githubusercontent.com/46496967/60283642-a1a0b300-9944-11e9-8b3e-e1a7283cd61f.png)

![05Geekbench_CPU](https://user-images.githubusercontent.com/46496967/60283643-a1a0b300-9944-11e9-98b4-fd5650762e0c.png)

![06Geekbench_GPU](https://user-images.githubusercontent.com/46496967/60283649-a2d1e000-9944-11e9-847e-7d6399875ad6.png)

**Origin USB Ports**
![07USBOrigin](https://user-images.githubusercontent.com/46496967/60283654-a36a7680-9944-11e9-8ca0-efb77f46b023.png)

**Edited USB Ports**
![08USBEdit](https://user-images.githubusercontent.com/46496967/60283655-a49ba380-9944-11e9-98ad-48ce1f903b61.png)
