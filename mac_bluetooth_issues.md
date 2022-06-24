Many users have reported **Mac** **Bluetooth issues** that cause connected devices to behave erratically. These problems resulted in my **Wireless Keyboard, Magic Trackpad and Mouse** not working correct fly (i.e., erratic cursor movement) and disconnecting frequently. 

In this post, I describe the steps I took to troubleshoot the Bluetooth issues I have had on my Retina 5K iMac running macOS.

PS: I just purchased a new [iMac Pro](https://michaelkummer.com/technology/imac-pro-review/), running the latest version of macOS, and I have had several disconnects so far. As a result, it looks like as if even Apple’s latest Pro model is not immune from the issues I describe below.

The connectivity issues started a few years ago with my Bluetooth accessories becoming intermittently unresponsive, resulting in erratic cursor movements and clicks that I didn’t cause.

After some initial troubleshooting, I disconnected the Trackpad and paired my old Magic Mouse. After a few days without issues, the Magic Mouse started acting up as well, followed by my Wireless Keyboard sometimes not registering keystrokes.

After every “reconnect” or a reboot, the devices would work for a while. However, after a few days, the connectivity issues would resurface.

[![Magic Trackpad](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/apple_magic_trackpad-750x395.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/apple_magic_trackpad.jpg?strip=all&lossy=1&w=2560&ssl=1)

Magic Trackpad

## Potential Causes

I had OS X 10.11 Public Beta installed and figured the problem was either caused by a corrupt OS X installation or interference. I also learned that the OS X kernel could only handle a limited number of concurrently connected Bluetooth devices without running into congestion and interference issues.

That magic number appears to be 5 or 6; some even say it is as low as 4. But I only had three devices connected at the same time. Because it was unlikely that all three devices had defects, the cause had to be the iMac’s hard- or software.

[![Wireless Keyboard](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/apple_wireless_keyboard-750x376.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/apple_wireless_keyboard.jpg?strip=all&lossy=1&w=2560&ssl=1)

Wireless Keyboard

## **Unsuccessful Troubleshooting Steps**  

I did some research and found dozens of potential causes and fixes for Bluetooth issues on OS X. Not knowing the exact cause I tried most of them without success.

Ultimately I ended up having the antennas and AirPort card of the iMac replaced. Since hardware issues are not very common, I ran through the following steps first, before taking my iMac to the Apple Store:

### Shutdown iMac

I powered down the iMac and before booting it up into Safe Mode, I replaced the batteries of all three affected devices.

### **Re-Seat Batteries**  

In addition to using fresh batteries, I took a piece of aluminum foil, rolled it into a tiny ball and put it into the battery compartment before inserting the batteries. Some users reported their issues were caused by batteries not having proper contact on either side of the battery compartment.

[![Magic Mouse](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/apple_magic_mouse-750x400.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/apple_magic_mouse.jpg?strip=all&lossy=1&w=2560&ssl=1)

Magic Mouse

### **PRAM And SMC Reset**  

For resetting the iMac’s System Management Controller (SMC), I unplugged everything, waited 30 seconds and plugged the power cable back in.

Then I pressed the power button and booted the iMac up while holding the _Command + Option + P + R_ keys. For more information on how to reset SMC and PRAM, you can check out my earlier [post](https://michaelkummer.com/technology/mac-first-aid-fix-common-mac-problems/) about Mac OS X First Aid.

### **Boot Up In Safe Mode**  

After the PRAM reset, I power cycled again while holding down the Shift key. That boots the Mac into Safe Mode. Once I logged in, I power cycled the iMac again and booted up normally.

### **Un-Pair Devices Via Preference Pane**  

Until yesterday, I didn’t have a wired keyboard and mouse, so disconnecting all wireless devices would prevent me from controlling the iMac. As a workaround, I enabled Screen Sharing via _System Preferences —> Sharing_ on my iMac and then logged into it from my MacBook.

I deleted the Wireless Keyboard, Magic Trackpad, Magic Mouse, entered pairing mode and reconnected all three devices.

[![Mac Bluetooth issues affect keyboard and trackpad](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_system_preferences-750x489.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_system_preferences.jpg?strip=all&lossy=1&w=2560&ssl=1)

### Delete Bluetooth Preferences (plist File)

Next, I deleted the preferences files associated with Bluetooth and specifically my Bluetooth-enabled devices. I used Finder to navigate to _~/Library/Preferences_ (you can use the _Command+Shift+G_ keyboard shortcut in Finder), and I moved the following files to the trash.

[![Mac Bluetooth issues affect keyboard and trackpad](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_finder_library-750x330.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_finder_library.jpg?strip=all&lossy=1&w=2560&ssl=1)

Go to the hidden folder ~/Library/Preferences

[![Preferences in Finder](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_finder_library_preferences-750x476.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_finder_library_preferences.jpg?strip=all&lossy=1&w=2560&ssl=1)

Find the related “plist” files

-   com.apple.driver.AppleBluetoothMultitouch.trackpad.plist – Magic Trackpad
-   com.apple.driver.AppleBluetoothMultitouch.mouse.plist – Magic Mouse
-   com.apple.driver.AppleHIDMouse.plist – wired USB mouse
-   com.apple.AppleMultitouchTrackpad.plist
-   com.apple.preference.trackpad.plist

### **Update To Latest Public Beta**  

I would have done that even without having Bluetooth issues, but I updated OS X to the latest 10.11.1 Public Beta.

### **Remove Anything That Could Cause Interference**  

Nothing in my immediate environment had changed since I started having issues, but I decided to remove any device that could cause interference from my desk and the immediate surrounding.

### **Reinstall a Fresh Copy of macOS**  

Reinstalling OS X was my last hope and one I tried to avoid for as long as I could. I knew that reinstalling would require my iCloud Photo Library to [re-synchronize](https://michaelkummer.com/technology/icloud-photo-library-synchronization-performance/) and that’s one thing I wanted to avoid. But since nothing else seems to solve my Bluetooth issues, I had no other choice.

To make sure all Public Beta residue was gone, I re-installed OS X using [Internet Recovery](https://support.apple.com/en-us/HT201314) (hold _Command + Option + R_ while booting up). That allowed me to wipe my hard drive completely, including the recovery partition.

### Bring iMac to Apple Store

At the Apple Store Hunter, my favorite Genius ran a system diagnostics, but it didn’t show any issues. So we re-imaged my hard drive with a developer copy of OS X that is based on 10.11 GM.

A quick test using their Magic Mouse seemed promising, but shortly after I returned home with the iMac, the issue reappeared. Fortunately, Hunter was thinking ahead and already ordered replacement parts, including:

[![AirPort card](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_airport_card-750x563.jpeg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_airport_card.jpeg?strip=all&lossy=1&w=2560&ssl=1)

AirPort card

-   3 Antenna assembly
-   The AirPort/Bluetooth card, identified by its model number BCM94360CD, consisting of:
    -   Broadcom BCM4360KML1G 5G WiFi 3-Stream 802.11ac Gigabit Transceiver
    -   Skyworks SE5516 Dual-Band 802.11a/b/g/n/ac WLAN Front-End Module
    -   Broadcom BCM20702 Single-Chip Bluetooth 4.0 HCI Solution with Bluetooth Low Energy (BLE) Support

For more information on those parts, check out iFixit’s [teardown](https://www.ifixit.com/Teardown/iMac+Intel+27-Inch+Retina+5K+Display+Teardown/30260) of the 27” Retina 5K iMac.

I will get those parts replaced in the next few days and hope this fixes the problem. I don’t know what else it could be. Meanwhile, I bought a wired keyboard and mouse and can’t say I love those cables on my otherwise neatly kept desk.

[![Temporary setup with wired keyboard and mouse](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_wired_keyboard_mouse-750x563.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_wired_keyboard_mouse.jpg?strip=all&lossy=1&w=2560&ssl=1)

Temporary setup with wired keyboard and mouse

As soon as I get my iMac back from the Apple Store (3-5 days turn-around time), I’ll update this post and let you know, if replacing the mentioned parts fixed the issues I was having. If you have had Bluetooth issues with OS X as well and knew a fix, please leave a comment. If you haven’t found a fix, I’d also appreciate if you would let me know what steps you took that didn’t work.

#### **Hardware Repair Attempt #1**  

I got my iMac back from the Apple Store today. They replaced the AirPort module and three antennas and surprisingly also the full display. I immediately updated the iMac to the very latest 10.11.1 Public Beta (Build 15B30a) and so far, the issue hasn’t returned. I’ll keep you posted!

#### **Hardware Repair Attempt #2**  

The antenna and AirPort module replacement did not fix the problem, and neither did OS X 10.11.1. So I took the iMac back to the Apple Store, and they’re currently replacing the AirPort module again – this time with one from a different manufacturer.

Swapping my Wireless Keyboard and Magic Trackpad for the new Magic Keyboard and Magic Trackpad 2 didn’t make any difference either. I’m guessing we’re dealing with a bug in El Capitan that’s related to the iMac’s hardware.

### **Software Update**  

Issues have returned despite all the troubleshooting steps above. So I filed a bug report with the Apple development team. Then today, I saw the final OS X 10.11.2 update come in, and it lists BT issues in the release notes. Let’s see if this final build fixes the problem.

[![OS X El Capitan Release Notes](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_el_capitan_update-750x275.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/mac_bluetooth_issues_el_capitan_update.jpg?strip=all&lossy=1&w=2560&ssl=1)

## **Updates And Additional Information**  

### Apple Grand Central Dispatch (GCD)

Howard Oakley suspects that GCD is causing many of the issues in macOS, including the above Bluetooth problems. Check out his excellent [article](https://eclecticlight.co/2017/05/09/hasnt-macos-changed-how-it-doesnt-work-like-it-used-to/) on the topic.

### macOS 10.13 High Sierra

Unfortunately, I occasionally still experience Bluetooth issues with my keyboard and trackpad after having upgraded my Mac to macOS 10.13 High Sierra. It’s disappointing that Apple didn’t or couldn’t fix that annoying problem!

### macOS 10.13.4 Beta

I have been running Beta versions of High Sierra since Apple made the first Public Beta available. The good news is, I barely experience any Bluetooth issues anymore. The bad news is, they still occur, as infrequently as they may.

Anytime it happens, my trackpad would disconnect for a second or two, before re-connecting. I haven’t done a complete re-install in a while, but I had one planned anyway, to jump off the Beta bandwagon.

## **How To Solve The Problem?**  

Since I published this article in 2015, many readers have chimed in and offered potential solutions. Here are the most promising ones, that have helped numerous readers resolve the issue:

### Disable Handoff in Preferences Pane

[![Allow handoff between this Mac and your iCloud devices - Mac Bluetooth issues](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/system-preferences_allow-handoff-750x704.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/system-preferences_allow-handoff.jpg?strip=all&lossy=1&w=2560&ssl=1)

Allow Handoff between this Mac and your iCloud devices

Several readers have suggested that the issue isn’t related to BT at all and I think they are on to something. Michael Perry discovered that the culprit might be Apple’s [Handoff](https://support.apple.com/en-us/HT204681) feature. If disabled, the problem appears to be going away for many. Here is how you do it:

1.  System _Preference > General_
2.  Uncheck “_Allow Handoff between this Mac and your iCloud devices_.”
3.  Restart your Mac.

### **Reset Bluetooth Module Via Debug Menu**  

[![Show Bluetooth in menu bar - Mac Bluetooth issues](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/system-preferences_bluetooth-750x485.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/system-preferences_bluetooth.jpg?strip=all&lossy=1&w=2560&ssl=1)

Make sure “Show Bluetooth in menu bar” is checked

You can also try to reset the Bluetooth module on your Mac, and here is how to do it. Before you start, make sure the Bluetooth icon is visible in your Mac’s menu bar. If it is not, open System _Preferences > Bluetooth_ and make sure you have checked “_Show Bluetooth in menu bar_” at the bottom of the dialog.

[![Reset the Bluetooth module - Mac Bluetooth issues](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/Bluetooth-debug-menu-1-750x430.jpg?strip=all&lossy=1&ssl=1)](https://cdn.michaelkummer.com/wp-content/uploads/2015/10/Bluetooth-debug-menu-1.jpg?strip=all&lossy=1&w=2560&ssl=1)

Reset the Bluetooth module

1.  Hold the Shift and Option key on your keyboard and click on the Bluetooth icon in your Mac’s drop-down menu bar
2.  Select _Debug > Reset the Bluetooth module_

Additionally, you can also try “_Factory reset all connected Apple devices_.” It helps if you have a wired keyboard a mouse handy while you perform those tasks.

### **Disable Internal Bluetooth And Use a USB Bluetooth Adapter / Dongle**  

Some readers have also suggested that switching from internal Bluetooth to an external (USB) Bluetooth [dongle\*](https://amzn.to/2G2RIkN) may help. I haven’t tried that, but it may be worth giving that a shot.

### VMware Fusion: Disable Share Bluetooth Devices with Windows

If you are using VMware Fusion to run Windows applications on your Mac, you could also try disabling “share Bluetooth devices with Windows” as one reader has pointed out.

### Disable 2.4 GHz Band on Wi-Fi Router or Access Point

Mitchel, one of the readers of this blog has reported success with disabling the 2.4 GHz band of his Wi-Fi router. Similar to many wireless network access points, Bluetooth uses the ISM 2.4 GHz band frequency. So it’s possible that your Wi-Fi network interferes with the Bluetooth receiver in your Mac.

## Final words – Apple needs to fix that!

If you have found this article searching for “Bluetooth not available on Mac,” “how to reset Bluetooth on Mac” or something similar, I hope some of the tips mentioned above could help to resolve your issue.

Unfortunately, those pesky Bluetooth issues on the Mac do not always seem to have a simple solution. I guess that is because the underlying problem is not well-understood either – at least not by the Mac user community.

Ultimately, Apple needs to fix those issues in its devices via hardware, firmware, or software updates. It can’t be that connectivity issues, like the ones mentioned above, stick around for multiple generations of devices and macOS releases.

If any of the solutions presented in this article have helped fix your Mac Bluetooth issues – and even if they haven’t – please let me know by leaving a comment below!

![Michael Kummer - Health and Technology](https://cdn.michaelkummer.com/wp-content/uploads/2020/09/michael-kummer-featured-banner-grey-1_1_-removebg.png?strip=all&lossy=1&resize=100%2C100&ssl=1)

I’m a healthy living and technology enthusiast.  
On this blog, I share in-depth product reviews, actionable information and solutions to complex problems in plain and easy-to-understand language.