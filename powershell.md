# Powershell 

## Copy a file to the specified directory      

```powershell
PS C:\>Copy-Item "C:\Wabash\Logfiles\mar1604.log.txt" -Destination "C:\Presentation"
```

## Get help for commands

```powershell
C:\users\chad\Downloads> Get-Help Copy-Item -examples
```

## Download files with Powershell

```powershell
Import-Module BitsTransfer

Start-BitsTransfer -Source $url -Destination $output
```

## Save output to file

```powershell
Command | Out-File -FilePath file.txt
```
Ammed a file with the `-Amend` flag

```powershell
Command | Out-File -FilePath -Amend file.txt
```


### <img width="650" height="325" src=":/7007c20e30a549db8efe7b9eb3cb7431"/>

### PowerShell’s Path Environmental Variable

On this page I will show you how to view, and how to change the Path variable using PowerShell commands.

One benefit of the path variable is less typing; if you type just the name of an executable, the operating system locates the program by searching through the values stored in this variable.

### Topics for Windows PowerShell’s Env:Path

*   [List $Env:Path with PowerShell](#List_$Env:Path_with_PowerShell)
*   [Example: $Env:Path](#Example:_$Env:Path)
*   [Changing Environment Variable Values with PowerShell](#Problem_Changing_Environment_Variable_Values_with_PowerShell)
*   [Further Research on Env:Path](#Further_Research_on_Env:Path)

### <a id="List_$Env:Path_with_PowerShell"></a>List $Env:Path with PowerShell

You can also see path values in the Control Panel; navigate to the System section and then click on the link to ‘Advanced system settings’.  Our purpose is employing PowerShell to list these paths.

Remember that we are dealing with an Environmental Variable, hence **$**Env.

```

# List Paths
$Env:Path

```

```

#Sample Output for Path Environmental Variable
C:\Program Files\Common Files\Microsoft Shared\Windows Live;C:\Program Files (x86)\Common Files\Microsoft Shared\Windows Live;C:\Program Files\Common Files\Microsoft Shared\Microsoft Online Services;C:\Windows\System32\WindowsPowerShell\v1.0\

```

**Note 1:** You really do need that $dollar sign.  Plain Env:Path does not work.

**Note 2:** Observe a semi-colon between each item; this is valuable information if you need to append more Path values.

See here for a refresher on [PowerShell’s Environmental Variables’](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm) drive.

**\[Environment\] Method**  
Here is an alternative method which lists the path values, but employs the base .Net Framework elements.

```

# List PowerShell's Paths
Clear-Host
[Environment]::GetEnvironmentVariable("Path")

```

**Note 3:** My point is to plant the idea that you could modify the “Path” with the sister command SetEnvironmentalVariable.

### Guy Recommends:  [Network Performance Monitor **(FREE TRIAL)**](https://www.computerperformance.co.uk/go/solarwinds-network-performance-monitor-free-trial/l/header/)[![Review of Orion NPM v11.5](https://cdn.shortpixel.ai/client/q_glossy,ret_img,w_274,h_169/https://www.computerperformance.co.uk/images/win8/orion_npmsc2.jpg)](https://www.computerperformance.co.uk/go/solarwinds-network-performance-monitor-free-trial/l/image/)

[**SolarWinds Network Performance Monitor**](https://www.computerperformance.co.uk/go/solarwinds-network-performance-monitor-free-trial/l/inline/) (**NPM)** will help you discover what’s happening on your network.  This utility will also guide you through troubleshooting; the dashboard will indicate whether the root cause is a broken link, faulty equipment or resource overload.

What I like best is the way NPM suggests solutions to network problems.  Its also has the ability to monitor the health of individual VMware virtual machines.  If you are interested in troubleshooting, and creating network maps, then I recommend that you try NPM on a [30-day free trial](https://www.computerperformance.co.uk/go/solarwinds-network-performance-monitor-free-trial/l/cta/).

[SolarWinds Network Performance Monitor Download 30-day FREE Trial](https://www.computerperformance.co.uk/go/solarwinds-network-performance-monitor-free-trial/l/button/)

### <a id="Problem_Changing_Environment_Variable_Values_with_PowerShell"></a>Problem Changing Environment Variable Values with PowerShell

When you change the value of an environment variable using PowerShell commands, the changes only affect the current session. This behavior mimics using the Set command of previous Windows operating systems.

You can use PowerShell to make a persistent change, the technique involves making changes the registry values.  Firstly, we will display the Environment values in the registry, then we will append another location.

I have also seen suggestions for putting SetEnvironmentalVariable commands in the profile files, Microsoft.PowerShell\_profile, Microsoft.PowerShellISE\_profile or [profile.ps1](https://www.computerperformance.co.uk/powershell/env-path/powershell_profile_ps1.htm).

### Retrieving Path Info from the Registry

The solution to the temporary nature of PowerShell’s changes to the environmental variable values is to script persistent registry modifications.  This is the equivalent of making changes to the Advanced system settings in the Control Panel.

```

# List PowerShell's Paths
Clear-Host
$Reg = "Registry::HKLM\System\CurrentControlSet\Control\Session Manager\Environment"
(Get-ItemProperty -Path "$Reg" -Name PATH).Path

```

**Permanently Modifying the Env:Path**

```

Clear-Host
$AddedLocation ="D:\Powershell"
$Reg = "Registry::HKLM\System\CurrentControlSet\Control\Session Manager\Environment"
$OldPath = (Get-ItemProperty -Path "$Reg" -Name PATH).Path
$NewPath= $OldPath + ’;’ + $AddedLocation
Set-ItemProperty -Path "$Reg" -Name PATH –Value $NewPath

```

**Note 4:** The key command is Set-ItemProperty.

**Note 5:** Remember that you need a semi-colon to separate the values.

### System Properties GUI

Firstly, if there is a GUI that corresponds to my PowerShell script, then I like to examine its menus to check that my script is working, and to give me ideas to improve my code.  The screenshot below is taken from the Control Panel.

[![PowerShell Env:Path](:/533cbb0e67f84f7a8754f8bc756a0537)](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm)

The registry script (above) achieves the same result as pressing the ‘Edit…’ button in the Advanced tab of the System Properties.

### Function Add-Path

```

Function Global:Add-Path {
<#.SYNOPSIS
PowerShell function to modify Env:Path in the registry
.DESCRIPTION
Includes a parameter to append the Env:Path
.EXAMPLE
Add-Path -NewPath "D:\Downloads"
#>
Param (
[String]$NewPath ="D:\Powershell"
)
Begin {
Clear-Host
} # End of small begin section
Process {
Clear-Host
$Reg = "Registry::HKLM\System\CurrentControlSet\Control\Session Manager\Environment"
$OldPath = (Get-ItemProperty -Path "$Reg" -Name PATH).Path
$NewPath = $OldPath + ’;’ + $NewPath
Set-ItemProperty -Path "$Reg" -Name PATH –Value $NewPath -Confirm
    } #End of Process
}
# This is what you type to call the function.
Add-Path

```

**Note 5:** My function has a built-in value for $NewPath, you may wish to change “D:\\PowerShell” to the value required by your project; for example:  
Add-Path -NewPath “C:\\Project”

### Guy Recommends: [SolarWinds Engineer’s Toolset **(FREE TRIAL)![Engineer's Toolset v10](:/2b9ac330c3784aae8a01b1baf239258d)**](https://www.computerperformance.co.uk/go/solarwinds-engineers-toolset-free-trial/l/header/)

This **[Engineer’s Toolset](https://www.computerperformance.co.uk/go/solarwinds-engineers-toolset-free-trial/l/inline/)** provides a comprehensive console of 50 utilities for troubleshooting computer problems.  Guy says it helps me monitor what’s occurring on the network, and each tool teaches me more about how the underlying system operates.

There are so many good gadgets; it’s like having free rein of a sweetshop.  Thankfully the utilities are displayed logically: monitoring, network discovery, diagnostic, and Cisco tools.  Try the SolarWinds Engineer’s Toolset on a [14-day free trial](https://www.computerperformance.co.uk/go/solarwinds-engineers-toolset-free-trial/l/cta/) now!

[SolarWinds Engineer's Toolset Download 14-day FREE Trial](https://www.computerperformance.co.uk/go/solarwinds-engineers-toolset-free-trial/l/header/)

### <a id="Further_Research_on_Env:Path"></a>Further Research on Env:Path

Here are ideas to discover more about Environmental Variables.

**Env:PathExt  
**In addition to Env:Path, there is a variable called Env:PathExt

```

Clear-Host
$Env:PathExt

```

```

#Sample Env: extensions
.COM;.EXE;.BAT;.CMD;
.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC;.CPL

```

**Get-Member  
**In this instance, Get-Member provides more methods than properties.

```

Clear-Host
$Env:Path | Get-Member

```

**Help About\_Environment\_Variables  
**For find out more about Environmental Variables, PowerShell provides this Help About… file.

```

Clear-Host
Help About_Environment_Variables

```

**Note 6:** This shows that PowerShell considers Env: as a drive, similar to regular file system drives such as C:\\.

**List Environmental Variables  
**Change the location to the Env: drive and then call for GCI (Get-ChildItem).

```

# List PowerShell's Environmental Variables
Set-Location Env:
Get-ChildItem

```

There are other ways of listing the environmental variables, for example:  
Get-Item Env:

[See more about PowerShell’s Environmental Variables »](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm)

»

### Summary of PowerShell’s Env:Path

If you wish to add locations to the path environmental variable then you can use PowerShell rather than the GUI in the Control Panel.  If you type just the name of an executable, the operating system locates the program by searching through the values stored in the Path Variable.

If you like this page then please share it with your friends

* * *

### See more Windows PowerShell  examples of variables

• [Syntax](https://www.computerperformance.co.uk/powershell/env-path/index_syntax.htm)   • [PowerShell Variables](https://www.computerperformance.co.uk/powershell/env-path/powershell_variables.htm)   • [Get-PSProvider](https://www.computerperformance.co.uk/powershell/env-path/powershell_get_psprovider.htm)   • [PowerShell Env:Path](https://www.computerperformance.co.uk/powershell/env-path/powershell_env_path.htm)  • [Free WMI Monitor](https://www.computerperformance.co.uk/powershell/HealthCheck/wmi_monitor.htm)

• [PowerShell Functions](https://www.computerperformance.co.uk/powershell/env-path/powershell_functions.htm)   • [Get-PSDrive](https://www.computerperformance.co.uk/powershell/env-path/powershell_get_psdrive.htm)   • [PowerShell New-PSDrive](https://www.computerperformance.co.uk/powershell/env-path/powershell_new_psdrive.htm)   • [Remove-PSDrive](https://www.computerperformance.co.uk/powershell/env-path/powershell_remove_psdrive.htm)

• [PowerShell Home](https://www.computerperformance.co.uk/powershell/env-path/index.htm)   • [PowerShell Environmental Variable](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm)   • [PowerShell Dollar Variable](https://www.computerperformance.co.uk/powershell/env-path/powershell_dollar_variable.htm)

Please email me if you have a better example script.  Also please report any factual mistakes, grammatical errors or broken links, I will be happy to  correct the fault.
