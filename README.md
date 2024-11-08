
# 🍁EDR--Fox : The Ultimate DFIR tool
This Lab is going to cover How we create and configure Virustotal-api app in Splunk SOAR.The motive of this lab is to reduce manual efforts and increase productivity.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue)](https://www.linkedin.com/in/nikhil--chaudhari/)
[![Medium](https://img.shields.io/badge/Medium-Writeups-black)](https://medium.com/@nikhil-c)

## 🍁Introduction
This Project contains multiple PowerShell scripts that can help you respond to cyber attacks on Windows Devices.


## 🍁Prequiresites
- Familiarity with commandline-interface.
- Moderate knowledge of Powershell.

## 🍁Requirements
- Windows machine.
- Vmware or Virtualbox.
- Admin permissions for better performance.

## 🍁Project Overview
The following Incident Response scripts are included:
- [DFIR Script](./DFIR-Script.ps1): Collects all items as listed in section [DFIR Script](#dfir-script).
- [CollectWindowsEvents](./Scripts/CollectWindowsEvents.ps1): Collects all Windows events and outputs it as CSV.
- [CollectWindowsSecurityEvents](./Scripts/CollectWindowsSecurityEvents.ps1): Collects all Windows security events and outputs it as CSV.
- [CollectPnPDevices](./Scripts/CollectPnPDevices.ps1): Collects all Plug and Play devices, such as USB, Network and Storage.
- [DumpLocalAdmins](./Scripts/DumpLocalAdmins.ps1): Returns all local admins of a device.
- [LastLogons](./Scripts/LastLogons.ps1) - List the last N successful logins of a device.
- [ListInstalledSecurityProducts](./Scripts/ListInstalledSecurityProducts.ps1) - List the installed security products and their status.
- [ListDefenderExclusions](./Scripts/ListDefenderExclusions.ps1) - List the FolderPath, FileExtension, Process and IP exclusions that are defined.

## 🍁DFIR Script
The [DFIR script](./DFIR-Script.ps1) collects information from multiple sources and structures the output in the current directory in a folder named 'DFIR-_hostname_-_year_-_month_-_date_'. This folder is zipped at the end, so that folder can be remotely collected. This script can also be used within Defender For Endpoint in a Live Response session (see below). The DFIR script collects the following information when running as normal user:
- Local IP Info
- Open Connections
- Aautorun Information (Startup Folder & Registry Run keys)
- Active Users
- Local Users
- Connections Made From Office Applications
- Active SMB Shares
- RDP Sessions
- Active Processes
- Active USB Connections
- Powershell History
- DNS Cache
- Installed Drivers
- Installed Software
- Running Services
- Scheduled Tasks
- Browser history and profile files

For the best experience run the script as admin, then the following items will also be collected:
- Windows Security Events
- Remotely Opened Files
- Shadow Copies

## 🍁DFIR Commands
The [DFIR Commands page](./DFIR-Commands.md) contains invidividual powershell commands that can be used during your incident response process. The follwing catagories are defined:
- Connections
- Persistence
- Windows Security Events
- Processes
- User & Group Information
- Applications
- File Analysis
- Collect IOC Information

## 🍁Project Usage

1. Start Windows machine and also open Powershell with Admin privileges, So the script can provide better output.

2. The script can be excuted by running the following command.
```PowerShell
.\DFIR-Script.ps1
```

3. The script is unsigned, that could result in having to use the -ExecutionPolicy Bypass to run the script.
```PowerShell
Powershell.exe -ExecutionPolicy Bypass .\DFIR-Script.ps1
```


## 🍁DFIR Script | Defender For Endpoit Live Response Integration
It is possible to use the DFIR Script in combination with the Defender For Endpoint Live Repsonse. Make sure that Live Response is setup  (See DOCS). Since my script is usigned a setting change must be made to able to run the script.

There is a blog article available that explains more about how to leverage Custom Script in Live Response: [Incident Response Part 3: Leveraging Live Response](https://kqlquery.com/posts/leveraging-live-response/)

### To run unsigned scripts live Response:
- Security.microsoft.com
- Settings
- Endpoints
- Advanced Features
- Make sure that Live Response is enabled
- If you want to run this on a server enable live resonse for servers
- Enable Live Response unsigened script execution

### Execute script:  
 **Step 1 :** Go to the device page  
**Step 2 :** Initiate Live Response session  
**Step 3 :** Upload File to library to upload script  
**Step 4 :** After uploading the script to the library, use the ***run*** command to run the script

To collect the output of the DFIR script perform the following actions:
```PowerShell
getfile "C:\windows\DFIR-TestDevice-2024-08-03.zip" &	
```
## 🍁References
- [Microsoft Documentation Live Response](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/live-response?view=o365-worldwide)
- [DFE User permissions](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/user-roles?view=o365-worldwide)
- [Defender For Endpoint Settings Live Response](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/advanced-features?view=o365-worldwide#live-response)



## 🍁Conclusion

Finally, we have created the DFIR project, where we learned about using PowerShell in EDR, how we can integrate with it, and how to collect artifacts with automation.

In the future release, I have some ideas in mind that I will surely implement in this project.

Hope you enjoyed Project creation and if you want more information on Project message me on linkedin. 

 Happy Learning !!!!!
 
 If you like my project make it star in your github and also follow for upcoming content.