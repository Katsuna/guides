# Katsuna OS for the Nexus 6P

### Device important info

* **name**: Nexus 6P
* **board/device name**: angler
* **arm architecture**: arm64

### Contents
1. [Set up the environment](#env)
2. [Before installing Katsuna OS for the first time](#first)    
    2.1. [Format Data partition](#format)    
    2.2. [Install a custom recovery partition (TWRP)](#recovery)
3. [Update to the correct stock Nexus image](#stock)
4. [Install Katsuna OS](#install)       
    4.1. [Install the Katsuna OS ROM](#flash)   
    4.2. [Install Google Apps](#gapps)
5. [Update Katsuna OS](#update)     
    5.1. [Update to a Katsuna OS update (feature revision: x.x.X - > x.x.Y)](#feature-update)     
    5.2. [Upgrade to a new Android / Katsuna OS version (major revision: X.x.x - > Y.x.x)](#major-update)     
    5.3. [Update to a new Katsuna Security Update (minor revision: x.X.x -> x.Y.x)](#minor-update)


<a name="env"></a>
## 1. Set up the working environment (for Windows)

Installing Katsuna OS is a unofficial modification to your device. Every time you want to install, update and/or factory reset it, make sure you have your working environment ready. You are going to need:

##### 1.1. **Open CMD.exe** (Command Prompt)
by searching for it in Windows Start.

##### 1.2. **Download Android SDK Tools**     
> Go [here](https://developer.android.com/studio/index.html#download) to download the Android SDK, which will give you most updated version of adb and fastboot. Scroll to the bottom of the page and find Other Download Options>SDK Tools Only, and grab the right version for your OS. While it's downloading create a folder in C:\ called SDK (C:\SDK). Once you've downloaded the zip you can extract it into your C:\SDK folder. Navigate to C:\SDK\android-sdk-windows and open SDK Manager.exe. In SDK Manager you need to install the following packages:

* Tools - Android SDK Tools, Android SDK Platform-tools
* Extras - Android Support Library, Google USB Driver     

##### 1.3. **Enable Developer Settings** in Android OS        
> Go into Settings/About Phone, scroll down and click on “build number” continuously until you see a toast notification telling you that you've enabled Developer Options. Go back to your Settings menu and enter Developer Options, scroll down and click on the **Enable OEM Unlock** (or "Enable OEM Unlocking") checkbox, also make sure you enable **USB Debugging** while you're in the Developer Options menu. Unplug and re-plug your device until the "ADB accept key" dialog is shown.

##### 1.4. **Test your adb/fastboot commands**          
Type these commands in the CMD window:
```
cd C:\SDK\platform-tools
adb devices
```
It should return your device **serial** number, if so, adb is working.

Next, power off your device. Turn it on again by pressing **(power + volume down)** and type this command in the CMD window.
```
fastboot devices
```
It should return your device **serial** number, if so, fastboot is working.

##### 1.5. **An Unlocked Bootloader**      
The bootloader screen will show you if the device's bootloader is unlocked. If it isn't, you will need to unlock it by typing this command:

**This will erase all user data from the device!**
```
fastboot flashing unlock
```
It will ask you for confirmation using the volume buttons and the power menu at this point, do it.

<a name="first"></a>
## 2. Before installing Katsuna OS for the first time

If you are here, this is your first time installing Katsuna OS! After [setting up the working environment as described in the previous step](#env), you will also need to do the following **BEFORE** installing Katsuna OS:

2.1. Format Data partition     
2.2. Install a custom recovery partition (TWRP)     
2.3. **DO NOT** reboot to Android OS after any step     

<a name="format"></a>
#### 2.1. Format Data partition
Power off your device. Turn it on again by pressing **(power + volume down)** and type this command in the CMD window:

  **Please note: this will erase all user data from the device!**       
```
fastboot format userdata
```
<a name="recovery"></a>
#### 2.2. Install a custom recovery partition (TWRP)
The recovery partition in your device is used to apply software updates to the device, e.g. OTA updates, and to erase user data and cache, e.g. for troubleshooting or preparing the device for resale (factory reset). For installing Katsuna OS, you are going to need to install a popular alternative, TWRP Recovery.

1. Download [TWRP Recovery 3.3.0-0](https://dl.twrp.me/angler/)
2. Copy the downloaded file inside:
```
C:\SDK\platform-tools\
```
3. Power off your device. Turn it on again by pressing **(power + volume down)** and type this command in the CMD window:
```
fastboot flash recovery twrp-3.3.0-0-angler.img
```

**BE CAREFUL!** From now on, don't reboot into the stock Android at any part of the process, or the custom TWRP will be overwritten by the stock recovery and you will have to start over!

<a name="stock"></a>
## 3. Update to the correct stock Nexus image

Katsuna OS is based on the official version of Android 8.1 (December security update: OPM7.181205.001). To ensure the best compatibility with Katsuna OS for your device, you will need to install the bootloader, radio, and the vendor partition of this version.

##### 3.1. Download the [OPM7.181205.001 stock nexus image for 6P](https://dl.google.com/dl/android/aosp/angler-opm7.181205.001-factory-b75ce068.zip)
after reading and agreeing with Google's [Terms & Conditions](https://developers.google.com/android/images#legal)
##### 3.2. Extract the zip file
Find the **bootloader-angler-angler-03.84.img**, **radio-angler-angler-03.88.img** and **image-angler-opm7.181205.001.zip** files. Extract the **image-angler-opm7.181205.001.zip** and find the **vendor.img** file.
##### 3.4. Copy all the above mentioned files inside:
```
C:\SDK\platform-tools\
```
##### 3.5. Power off your device. Turn it on again by pressing **(power + volume down)** and type these commands in the CMD window:
```
fastboot flash bootloader bootloader-angler-angler-03.84.img
fastboot flash radio radio-angler-angler-03.88.img
fastboot flash vendor vendor.img
```

##### 3.6. If everything finishes successfully, reboot the device into the RECOVERY mode.
You can do that by using the volume buttons to select "Recovery mode". Use the power button to confirm the selection.

<a name="install"></a>
## 4. Install Katsuna OS

Every time you want to install Katsuna OS:

* Make sure you have [already updated to the correct stock nexus image](#stock).
* [Install](#flash).

<a name="flash"></a>
### 4.1. Install the Katsuna OS ROM file

1. Download the ROM from [here](http://updater.katsuna.com/files/angler/latest).
2. **Remember, don't boot into Android yet!**
3. Power off your device. Turn it on again by pressing **(power + volume down)**. Use the volume buttons to select "recovery mode". Use the power button to confirm the selection.
4. Perform a full wipe      
```
* Select the wipe option from the TWRP home screen.
* Select advanced wipe.
* Check the system, data, cache, and dalvik cache options.
* Swipe to wipe.
```       
5. Copy the downloaded file inside:     
```
C:\SDK\platform-tools\
```     
6. Push the ROM file to the device by typing this command in the CMD window (replace FILENAME with the name of the downloaded file):        
```
adb push FILENAME.zip /sdcard/
```     
7. Install the ROM file     
```
* Select the install option from the TWRP home screen.
* Select the ROM zip
* Swipe to install
```     
7. (Optional): [Install Google Apps](#gapps)    
8. Select "Reboot System" and wait for Katsuna OS to load for the first time.

<a name="gapps"></a>
### 4.2. Install Google Apps (Optional)
*Open-GApps is an independent third party GApps (Google Apps) distribution service that Katsuna has no affiliation with. Use at your own discretion.*

You can use the Google Play Store and Google Apps with your Katsuna OS installation with an extra step. During [installation](#flash):

1. Download [Nano Open-GApps package](http://opengapps.org/) **for Android 8.1 & arm64**    
2. Copy the downloaded file inside:
```
C:\SDK\platform-tools\
```
3. Push the file to the device by typing this command in the CMD window (replace FILENAME with the name of the downloaded file):
```
adb push FILENAME.zip /sdcard/
```
4. Install the Google Apps file
```
* Select the install option from the TWRP home screen.
* Select the GApps zip
* Swipe to install
```

<a name="update"></a>
## 5. Update Katsuna OS

Katsuna OS can be updated:

* Manually, by using the [installing procedure](#install).        
If you choose this method, there are no extra steps.

* Through the Updater App inside Katsuna OS.        
If you update the ROM through the Updater app:

<a name="feature-update"></a>
##### 5.1. Update to a Katsuna OS update (feature revision: x.x.X - > x.x.Y)
The Updater app will let you know automatically if a new update has been found, and you will be able to download the update and apply it with a few taps with no PC involved.

#### There may be extra steps to be executed in the following cases:

<a name="major-update"></a>
##### 5.2. Upgrade to a new Android / Katsuna OS version (major revision: X.x.x - > Y.x.x)
The Updater app can't handle a major Katsuna OS update seamlessly. In order to install the update through it, you will need to:

* Download the ROM file using the Updater app but **DO NOT TRIGGER THE UPDATE**.
* [Make sure you have the latest TWRP recovery partition installed](#recovery)
* [Install the correct stock nexus image files for the new update](#stock)
* [Install the ROM file downloaded through the Updater app](#flash). This time, the file can be found at:
```
/sdcard/updates/
```

<a name="minor-update"></a>
##### 5.3. Update to a new Katsuna Security Update (minor revision: x.X.x -> x.Y.x)
After a new Katsuna [Security update](https://source.android.com/security/bulletin/), you will need to [download the relevant stock nexus image and install ONLY the vendor.img file again](#stock).
