# Windows Driver Store

Windows 10 has a concept of the **Driver Store**. It is a write-protected directory where Windows keeps many drivers it has sourced from&hellip; *wherever*, because&hellip; *reasons*.

The **Driver Store** is located at:

```Shell
C:\Windows\System32\DriverStore\FileRepository
```

I learned about it during the first attempt to enable the Windows 10 **Core Isolation** feature. There was a handful of drivers, most likely left-overs from my experiments with the embedded systems, which were not even loaded by Windows, but whose mere *presence* in the **Driver Store** would not let Windows enable **Core Isolation**.


* To **list** the drivers in the **Driver Store**, use `driverquery`.
* To **remove** a driver from the **Driver Store**, `dism` is used.


References:

* [Where does Windows 10 Store Device Drivers][1]
* [How to see and Export All Installed Windows 10 Drivers][2]
* [Cleaning Up Driver Store][3]

[1]: https://www.faceofit.com/where-does-windows-10-store-device-drivers/
[2]: https://www.faceofit.com/how-to-see-and-export-all-installed-windows-10-drivers/
[3]: https://medium.com/@iced_burn/clean-filerepository-folder-in-driverstore-windows-10-622d3c79f58b