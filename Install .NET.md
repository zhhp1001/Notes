# Install .NET



**Error Info**

```
windows couldn't find required files to complete the requested changes make sure you're connected to internet...
```



**Solution**

```
In an elevated command prompt, type the following (replacing the drive letter for your media)

dism /online /add-package /packagepath:D:\sources\sxs\microsoft-windows-netfx3-ondemand-package.cab
```

