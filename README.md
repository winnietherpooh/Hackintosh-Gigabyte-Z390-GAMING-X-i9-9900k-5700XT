# Hackintosh Gigabyte GAMING X i9-9900k 5700XT

## Verified working with 10.15.5.
![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot_Info.png)

## Configuration
- Motherboard: Gigabyte Gaming X
- BIOS: f10c
- CPU: i9-9900K  
- RAM: 2x 8GB Crucial Ballistix Sport LT BLS2K8G4D30BESBK 3000 MHz, DDR4
- Storage: Samsung 950 EVO M.2 512GB  
- dGPU: ASUS 5700XT (Reference)  
- WIFI/BT: FV-T919  

- SMIBIOS 19,1
- OpenCore 5.8

## Confirmed working
- Quick boot into MacOS and rock solid
- NVRAM if CFG Lock is disabled (see below)
- Fan and CPU temp information

![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot_temp.png)

- iMessage,Handoff and Approve with Apple Watch
- Sleep and Wake from bluetooth mouse or keyboard
- iGPU Framebuffer for hardware acceleration (encoding/decoding/preview) including AppleTV DRM movies (shikivga=80) and SideCar

![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot_Hackintool_1.png)
![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot%20Framebuffer.png)


## Known Issues
- Unlock with Apple Watch does not work (for me)
- Multiple key press to wake from sleep with bluetooth (known issue with Gigabyte Gaming X or M boards)


## Bios Setup:

- Make sure the IGP is set to Enabled for the Framebuffer to be recognized (Auto will not work)
- Advanced Mode > Settings > Above 4G Decoding > Enabled
- Advanced Mode > Settings > USB Configuration > XHCI Hand-off > Enabled
- Advanced Mode > Boot > CSM Support > Disabled

## USB Setup:

Some ports have been disabled to stay below the 15 port limit
Ignore the Thunderbolt controller, this has been removed from this EFI.

![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot_USB_Layout.png)

![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot_USB.png)

## Post Installation
1. Setup Bios as per above
2. Open your config.plist and populate the Serial, Board Serial, UUID and MAC address. Make sure to edit the config.plist only with ProperTree
3. Go to System Preferences > Startup Disk and select your startup disk.
4. Disable CFG Lock and save profile in Bios (see below)
5. Done.

if you get stuck at opencore boot, try to clear nvram via opencore settings  

![](https://github.com/extric99/Hackintosh-Gigabyte-Z390-GAMING-X-i7-9900k-5700XT/blob/master/screenshot/Screenshot_MAC.png)

## Disable CFG Lock

Disable CFG Lock (MSR 0x5C1) in BIOS via modified GRUB Shell, follow the guide [HERE] (https://www.tonymacx86.com/threads/gigabyte-z390-m-gaming-build-with-working-nvram.291193)

Credits pastrychef

Unlock MSR (NVRAM will not work with locked MSR) <-This value is ONLY for the Gigabyte Z390 M Gaming or Gaming X!!
1. Download the EFI Shell and unZip it.
2. Copy the EFI folder to the EFI partition of your USB flash drive. (EFI Agent can help with mounting of EFI partitions.)
3. Boot from the USB flash drive.
4. At the Grub prompt, enter:

setup_var_3 0x5C1 0x0

5. Reboot in to BIOS.
6. Save your BIOS settings profile to USB flash drive. If your BIOS ever resets itself, you won't have to manually unlock MSR again, just load your BIOS setting profile and MSR will be unlocked.
7. Done.
* Note/Warning: The MSR address is the same for every BIOS version for this motherboard, so far. This MSR address is only for this motherboard. If you are on another motherboard, you will need to find what your MSR address is.

## Tips
- User [EFI-shell] (https://www.tonymacx86.com/attachments/efi-shell-zip.448321)
- Use [Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip) to validate correct implementation of Framebuffer and USB
- Use [macinfo](https://github.com/acidanthera/MacInfoPkg) to generate your S/N

