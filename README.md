# 🍔 bigmac

Big Sur macOS 11 Mac Pro patcher 

## 🍔 Coming soon: bigmac2 
![image](https://user-images.githubusercontent.com/24852454/101307225-4c333a00-388a-11eb-99ee-28d6ea3b047f.png)
1. Native Airdrop and Handoff support! This may depend on your WiFi/BT card. I can update which hardware will work.
2. USB 1.1 Support, special thanks to JackLukem for the tip!
3. FireWire 400 and 800 Hard Drive and SSD Support (booting from FW currently fails)
4. Legacy WiFi 802.11n Patch
5. Legacy Bluetooth2 disabler, Bluetooth4 enabler (with card or BT4LE dongle)
6. BMO2.dmg a fully patched clean system disks with LegacyWiFi or 802.11ac WiFi.

## 💾 BMO2 
1. Is for users who cannot get the current installer to work
2. It is for R&D and testing purposes only, not to be redistributed, not for production purposes.
3. BMO2 is an experimental cloud based clean install.
4. The disk image is already updated with latest patches from the pre-release bigmac2 work.
4. A USB Hub for your keyboard, mouse or trackpad is highly recommended.
5. Bluetooth 2 is turned off on Big Sur via software. It causes a Kernel Panic.
6. Two versions of BMO2 are available. If you don't know which one, pick the legacywifi edition it is universal.
   * [Download BMO2_802.11n legacywifi edition](https://starplayrx.com/downloads/bigmac/BMO2n_legacywifi.dmg) for stock 802.11n cards (MacPro 3,1)
   * [Download BMO2_802.11ac_wifi_edition](https://starplayrx.com/downloads/bigmac/BMO2ac_wifi.dmg) is for 802.11ac cards only.
9. Format a disk using MacOS Extended Journaled.
10. Execute in Terminal `sudo asr -s ~/Downloads/BMO2* -er -t dragDiskHere`
11. When asr is 100% complete, open System Preferences, select BMO2 as your startup disk and reboot.
12. bigmac2's pre-release patches have already been applied. When finished, move the BMO2 disk image in the Trash and delete permanently. 

<b>One More Thing</b> A Big Mac is better than a New Mac. [Please donate.](https://www.paypal.com/donate?hosted_button_id=M3U48FLF87SXQ) Thank you!

## Requirements 
1. Mac Pro 2008 - 2012
1. SIP, a.k.a. System Integrity Protection, must be disabled. If it's on booting the installer might panic.
2. Boot screen. If you don't have a boot screen, support will not be provided. I'll leave that adventure up to you.
3. [Download APFS ROM patcher by dosdude1](http://dosdude1.com/apps/APFS%20ROM%20Patcher.zip).  Then enter password: `apfs` and follow the instructions.
4. Your GPU must support Metal. I highly recommended this GPU: Radeon RX 580 8 GB Mac Edition on eBay for $299
5. 1 external USB SSD or hard drive. Fast flash drives may work. Slow thumb drivers are not supported.
6. For the actual installation, an SSD or hard drive with 60GB or greater. 256GB recommended.

## How to boot a USB (Requires a Video Card with a Mac Boot ROM)
1. Be sure your Mac Pro can boot APFS volumes directly. There is an APFS ROM Patch for Mac Pro 3,1s.
2. Be sure to disable System Integrity Protection as soon as possible (`csrutil disable ; csrutil authenticated-root disable`).
3. Plug a USB 2.0 keyboard and pointing device directly into your Mac Pro's USB 2.0 ports.
4. Plug the bootable installer into your Mac Pro.
5. Press and hold the Option (Alt) ⌥ key immediately after turning on or restarting your Mac Pro.
6. Release the Option key when you see a gray boot screen showing your bootable volumes.
7. Select the volume containing the bootable installer. Then click the up arrow or press Return. 
8. Choose your language, if prompted.
9. Open the Terminal.
10. Execute `cd /Volumes/bigmac; .preinstall.sh`, and quit Terminal.
11. Select Install macOS Big Sur from the Utilities window, then click Continue and follow the onscreen instructions.

Legacy USB 2.0 for keyboard and mouse devices is not working 100%. If you leave them plugged into a USB 2.0 port, they will work. If you disconnect them, they won't reconnect. This is a problem with Big Sur which Apple introduced on their own. A workaround is use a USB3.0 PCIe card but this only works when the system is booted, not from a cold start. USB 3.0 hubs plugged into a USB 2.0 port may also work. A patch may be implemented to take care of this issue.

Note: Option boot using a boot screen requires a keyboard in directly into the machine and not a PCIe card. Bluebooth keyboards do not catch up in time and PCIe cards don't work without an OS. There used to be a a Bluetooth fix in NVRAM for this. If I locate the fix, will update.

## BigMac's Workflow in a Nut Shell 🥜
1. Workflow -> Download Big Sur -> Create USB Installer
2. Create your unpatched USB installer disk with bigmac on another partiton with `./bigmac.sh`
3. Execute `cd ~/Downloads/bigmac.master`
4. Execute `./bigmac.sh`
5. Reboot -> hold down OPTION key -> macOS Big Sur Installer
6. Workflow -> Boot USB -> Preinstall.sh -> Install -> Postinstall.sh
7. Boot the USB installer, from its Terminal type:
8. Execute `cd /Volumes/bigmac`
9. Execute `./preinstall.sh`
10. Wait for the install is fully completed (hint: it takes 3 stages to complete.)
11. Boot the USB installer, from its Terminal type:
12. Execute `cd /Volumes/bigmac`
13. Execute `./postinstall.sh`

### Pre Install Track, Before you open the Big Sur Installer (Works with All Macs)
1. Boot up the Install macOS Big Sur USB Disk (Don't have it? Execute `sudo ./bigmac.sh`).
2. Execute `cd /Volumes/bigmac`.
7. Execute `./preinstall.sh`.
8. set boot-args to `-no_compat_check -v`.
9. Quit the Terminal. Open the big Sur installer app.
10. Big Sur installs in three stages.

### Post Install Track, Required for Mac Pro 3,1
1. Boot up the Install macOS Big Sur USB Disk (Don't have it? Run `sudo ./bigmac.sh`)
2. Execute `cd /Volumes/bigmac`.
4. Type `./postinstall.sh` and type in the volume name of the install you just did (e.g., `/Volumes/Macintosh\ HD` (This will be improved in a future version); You may have to use `ls -al` in volumes to get the name before hand. (e.g., `./postinstall.sh /Volumes/Macintosh\ HD`)
5. Quit the Terminal and select your startup disk.

### Notes about Big Sur Installs
1. The install process is done in three stages each varying in time.
2. Allow all three stages to fully complete!
3. Mac Pro 3,1 Early 2008 owners will need to stop an infinite loop after the 4th or 5th reboot. Wait until you see a pattern before killing it). Hold option-key to see if you can get to a boot screen between the kernel panics. If all else fails, hold the power button down and then hold down the option-key.
4. the `-v` boot-arg helps monitor the progress.
5. After about 45 - 60 minutes, the installer should be complete.

### Special Notes with Mac Pro Early 2008 and Metal AMD Cards 
1. Big Sur's video drivers are not compatible with the Penryn style CPU.
2. The Post Install script using MousSEE to emulate a couple instructions.
3. This allows AMD Radeon cards that support Metal to be used on a MP3,1.

### Telemetry and Mac Pro Early 2008
1. The telemetry plugin on Big Sur is not compatible with the Penryn style CPU.
2. The post install script installs one that is compatible.

### Mac Pro Early 2008 Installation Notes
1. In between installer tasks, Big Sur's install runs through 3 complete reboot cycles.
2. If you see kernel panics, or fast reboots after the 5th reboot, you will need to kill the cycle by holding the power button down, or if possible hold down the Option-key see if you can get back to your boot screen.
3. Then you can run the post install script from which method you ran the pre install script.
4. The post install script patches your system and allows it to boot up.

### Pre Install Notes
1. The Preinstall script runs in memory. It does not physically touch the installer. If you reboot before running the Big Sur installer app/task, you will need to run the Preinstall script again. 
2. Because the preinstall script runs in memory, do not attempt run the preinstall twice in the same boot session. This will cause major delays when opening the Big Sur install app/task.

### How to turn off System Integrity Protection (this is now built into preinstall.sh)
1. Open Terminal in the booted recovery disk (and possibly external USB Big Sur USB installer disks made with createinstallmedia).
2. Execute `csrutil disable`.
3. Execute `csrutil authenticated-root disable` (can only be done from Big Sur Recovery disks).
4. Use Start up disk (top left to select your installation).

## Videos
1. https://starplayrx.com/downloads/preinstall_bigmac.mov
2. https://starplayrx.com/downloads/postinstall_bigmac.mov
3. https://starplayrx.com/downloads/recovery_external_usb_bigsur_only.mov
4. https://starplayrx.com/downloads/disable_sip_and_authenticated_root_bigsur.mov

## How to clone your system
* Execute `sudo asr -s /drag/source/here -t /drag/target/here -er -nov`.

## Known issues with USB 2.0
1. Input devices that get disconnected do not reconnect. Workaround, use a USB 2.0/3.0 hub. Plug that into a Mac USB port and plug your input devices into the hub. This has been tested. USB 3.0 PCIe cards will also work but not at boot time.
2. USB storage devices are hotswapped with issue.
3. Certain thumb drives via USB 3.0 PCIe card, some will disconnect on idle. USB Thumb drives tend to not work on USB 2.0 unless seen at boot time.

## Known issues with MAME input devices
* USB 1.1 will be supported in bigmac2.

## 🍟 Special thanks to the following contributors:

Dosdude1, ASentientBot, BarryKN, JackLukeM, Parrotgeek, Ritchie333, seyoon20087

See Credits file for our list of contributors

Sending a warm welcome to the Unsupported Macs Team, you are the Best. And Sending back kudos to the Open Core Legacy Macs Team for mentioning bigmac and all our bloggers and video bloggers who have made how to's using bigmac. The bigmac community is growing every day. And this is the main reason I am doing a follow up version called bigmac2. 

If anyone wantss to collaborate together with future versions of Big Mac. I don't mind if you are on a different unsupport mac team including Open Core. I am at a point where working together on something will do more for the greater good than I can do by myself. If you are interested at all and I don't mind if you have years to decades of experience or just have an interest in computers in general, please post an issue and would love to work with you. 

Updated on December 7, 2020 for macOS 11.0.1 (20B50), Mac Pros 2008, 2009, 2010, 2012, bigmac Copyright 2020 by Todd Bruss | NiceMac LLC

A Big Mac is better than a New Mac. Please donate to [NiceMac LLC](https://www.paypal.com/donate?hosted_button_id=M3U48FLF87SXQ)
