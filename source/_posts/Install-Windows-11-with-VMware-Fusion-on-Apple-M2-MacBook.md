---
title: Install Windows 11 with VMware Fusion on Apple M2 MacBook
date: 2023-09-02 14:54:02
tags:
---

## The Problem

- Microsoft is only providing intel version ISO file for Windows 11.
- For Windows 11 Insider Preview, the arm version is provided only in VHDX format.

## Workaround

Luckily, we can get the ESD file and then convert it into ISO file which can be used in VMware.

## Steps

Go to the website of [Parallels](https://www.parallels.com/ca/products/desktop/) to download their Mac app. Alternatively, you can get the DMG link from [Homebrew API](https://formulae.brew.sh/api/cask/parallels.json)

The link looks like [this](https://download.parallels.com/desktop/v19/19.0.0-54570/ParallelsDesktop-19.0.0-54570.dmg). After downloading, double click the DMG file but don't install the Parallels. You just need to mount the DMG file.

Then open the terminal and run the following commands:

```bash
sudo ditto /Volumes/Parallels\ Desktop\ 19/Parallels\ Desktop.app/Contents/MacOS/prl_esd2iso /usr/local/bin/prl_esd2iso
sudo ditto /Volumes/Parallels\ Desktop\ 19/Parallels\ Desktop.app/Contents/Frameworks/libwimlib.1.dylib /usr/local/lib/libwimlib.1.dylib
```

We can thank Parallels for providing these amazing tools later. Unmount and delete the DMG file.

To figure out the download link for Windows 11 ESD file:

```bash
cd ~/Downloads/ && curl -L "https://go.microsoft.com/fwlink?linkid=2156292" -o products_Win11.cab && tar -xf products_Win11.cab products.xml && cat products.xml | cat products.xml | grep ".*_CLIENTCONSUMER_RET_A64FRE_en-us.esd" | sed -e s/"<FileName>"//g -e s/"<\/FileName>"//g -e s/\ //g -e s/"<FilePath>"//g -e s/"<\/FilePath>"//g -e s/\ //g | head -n 2
```

By the way, I assume your current working directory is ~/Downloads/. If not, please change it accordingly.

Use curl to download the ESD file:

```bash
curl http://dl.delivery.mp.microsoft.com/filestreamingservice/files/f16733c5-e9f8-4613-9fe6-d331c8dd6e28/22621.1702.230505-1222.ni_release_svc_refresh_CLIENTCONSUMER_RET_A64FRE_en-us.esd --output win11.esd
```

Convert the ESD file into ISO file.

```bash
prl_esd2iso ~/Downloads/win11.esd ~/Downloads/win11.iso
```

Now you can insert the ISO file into VMware Fusion which is free to use with a [personal license](https://www.vmware.com/go/get-fusionplayer-key) You can find the license key after you register/login on the their website.

Install the vmware fusion with Homebrew. Yes, you need have Homebrew installed, but I guess you already done it.

```bash
brew install --cask vmware-fusion
```

If you run into the chown issue like:

```bash
Chown /Applications/VMware Fusion.app: Operation not permitted
```

Please double check if the Full Disk Access is granted for the Terminal.app in system settings Privacy & Security.

Drag and drop the Windows 11 ISO file into vmware. You can go with UEFI and also the default values with the rest of the settings.

Pay attention to the message on the screen, if it is saying press any key to continue, don't wait. You only have five seconds to hit the key, so be fast. I will not talk about the basic steps of installing Windows 11, I trust you can install the operating system with the GUI.

When you reach the setup step of internet connection, press shift + fn + F10 to invoke the CMD. Input:

```bash
OOBE\BYPASSNRO
```

It will auto restart the setup steps and this time you choose the option I don't have internet (Yup, actually you don't.) Continue with limited setup. If everything goes well. In the end, you get into Windows 11 Desktop

Run PowerShell as Administrator and type:

```bash
Set-ExecutionPolicy RemoteSigned
```

Insert the VMware Tools CD image into the virtual machine. Run the setup script with PowerShell.

In case you want to set the Execution Policy back:

```bash
Set-ExecutionPolicy Restricted
```

If the VMware Tools are successfully installed, the internet connection is working inside the virtual machine. Adjust settings as you wish. For example, set the display resolution to 2880 x 1800 and Scale to 200%.

A fully operational Windows 11 on Mac is all yours.

Enjoy.
