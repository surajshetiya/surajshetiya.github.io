---
layout: post
title: Fixing time windows , linux dual boot
---

I ocasionaly use both Windows and Linux in my machine. The end up is that every time I login to Windows and switch back to Linux or vice versa the system time seems to off.  

This issue occurs because of the two operating system fiddling with the system clock every time they find that the system clock's time does not match the NTP times. But then why would the times not match ?  

The issue lies in the format in which both the operating systems store time. Windows stores the time as local time while Linux stores the time as UTP. I prefer UTP times as these are independent of day light savings and are consistent. So, we need to fix Windows in roder to write the time to the system in UTC format.  

This has a simple fix in Windows by adding a registry entry to store the time as UTC. To achieve this, let us create a new registry file with extension **<name>.reg**.  
To this file add the contents below and save the file.  

```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
     "RealTimeIsUniversal"=dword:00000001
```

Now let us run the file and update the time to internet time(NTP). A simple fix indeed.