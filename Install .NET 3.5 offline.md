# Install .NET 3.5 offline



https://windowsloop.com/download-net-framework-3-5-offline-installer/

Windows 10 by default comes preinstalled with .net framework 4.5. One of the best things about different .net framework versions are that they are backward compatible. That means, a vast majority of Windows 10 users never need to install older versions manually. However, some old software, especially the ones designed for Windows Vista or 7, might require you to install .net framework 3.5.

## Install .net framework 3.5 with DISM command

If you want to, you can also plug-in the Windows 10 installation media and use the DISM command to install dot net framework 3.5. This is particularly helpful if you cannot download the online or offline installer. Here is how you can do it.



1. First, plug in the Windows 10 USB drive. Alternatively, if you have a Windows 10 ISO, double-click on the ISO. It will automatically mount it in File Explorer.

2. Now, open the Start menu and search for “Command Prompt.” Next, right-click on the Command Prompt and select the “Run as administrator” option. This action will open Command Prompt as admin.

3. In the Command Prompt window, copy the below command, paste it in the command window, and press Enter. Don’t forget to replace “X” in the below command with the actual drive letter of the Windows 10 installation USB drive.

```
Dism /online /enable-feature /featurename:NetFX3 /All /Source:X:\sources\sxs /LimitAccess
```

4. As soon as you execute the above command, Windows will extract and enable the .net framework 3.5 in your system.

That is it. It is that simple to download dot net framework 3.5 offline installer for Windows 10.

I hope that helps. If you are stuck or need some help, comment below and I will try to help as much as possible