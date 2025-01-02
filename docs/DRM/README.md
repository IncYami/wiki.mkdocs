## Prerequisites

[Python](https://www.python.org/downloads/ "Python") *Make sure to check "add to path" option when installing.*

[ADB](https://dl.google.com/android/repository/platform-tools-latest-windows.zip "ADB Minimal Install")

An Android 7-14 device that is able to be rooted / is rooted.

# Step 1: Enable ADB and connect to device.

Connect to your android device via ADB. There is a guide on how to install the ADB files above and connect to your device by XDA-developers [here](https://www.xda-developers.com/install-adb-windows-macos-linux/ "here").

**To enable ADB / USB Debugging follow these steps**
1. Open your device's Settings and tap About phone or About tablet. 
2. Tap Build number repeatedly until you see a notification that reads "You are now a developer." 
3. Go back to the main System menu, then tap Developer options. 
4. Tap the toggle switch in the top-right corner to enable developer options (if it's not already enabled). 
5.  Tap OK to confirm. 
6.  Tap the USB debugging toggle switch. 
7.  Tap OK to confirm. 
8. The next time you plug your device into a computer, you'll receive a prompt asking if you want to authorize USB debugging for that computer. Tap OK to confirm. 

You may now connect to your device 

`adb connect <device-ip-address>`
or if using USB
`adb devices`

On your device you should receive a notification to accept the adb connection, checkmark trust this device and then click allow.

# Step 2: Installing / Running Frida-Server

**Option 1:**

Install the [Magisk Frida Module](https://github.com/ViRb3/magisk-frida "Magisk Frida Module") via the Magisk app if rooted via Magisk

**Option 2:**

Push [Frida-Server](https://github.com/frida/frida/releases/ "Frida-Server") for android. Unzip the xz file and extract Frida-Server file. 

Change directory to where you extracted the file and enter the command `adb push frida-server-XX.X.XX-android-arm /sdcard/`

Once it has been pushed open up a shell with `adb shell`

Move the server to the tmp directory `mv /sdcard/frida-server-XX.X.XX-android-arm /data/local/tmp/`

> You may get an error about chown permission, this is negligible

Login as super user and create a new environment `su -`

 Give execute privileges to frida-server `chmod +x  /data/local/tmp/frida-server-XX.X.XX-android-arm`
 
 Start the server `/data/local/tmp/frida-server-XX.X.XX-android-arm`
 
 **When you start the server command prompt will hang, this is normal and means the program is running, do not close out and continue to step 2**
 
#  Step 3: Extracting the CDM

Download, extract and run [KeyDive](https://cdm-project.com/Android-Tools/KeyDive "KeyDive") 

Now play some widevine encrpyed content on your Android device. I suggest using [https://bitmovin.com/demos/drm](https://bitmovin.com/demos/drm "https://bitmovin.com/demos/drm") playing over google chrome.

Once you have played the content your keys should be dumped and should be named `client_id.bin` and `private_key.pem`

Make a copy of these for safekeeping wherever you like but DO NOT LOSE THEM

*You can now close out of running frida server if you are running it over adb, you may also close dumper once you have verified successful dumping.*
