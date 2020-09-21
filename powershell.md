# Powershell 

## Powershell Modules

__Installing__

Find the path of your modules by typing:

`$Env:PSModulePath`

__Listing__

`Get-Module -ListAvailable`

__Importing__

`Import-module -name ModuleName`


## Copy a file to the specified directory      

```powershell
PS C:\>Copy-Item "C:\Wabash\Logfiles\mar1604.log.txt" -Destination "C:\Presentation"
```

## List certain things about directories...

```powershell
Get-ChildItem . | ? { $_.PSIsContainer } | sort LastWriteTime | select name,lastwritetime
```

1. This does a `Get-ChildItem` in directory `.` 

2. then pipes to this `| ? { $_.PSIsContainer }`

> the `?` is short for `Where-Object` and `{ $_.PSIsContainer }` displays only directories

3. then pipes to `| sort LastWriteTime`

> `| sort LastWriteTime` sorts by when the directories were saved last

4. then pipes to `| select name,lastwritetime`

> `| select name,lastwritetime` displays it in the 2 columns of `name` and `lastwritetime`

### Another Example

```powershell
Get-ChildItem | where {!$_.PsIsContainer} | Select-Object Name > onlyFiles.txt
```

## Get help for commands

```powershell
C:\users\chad\Downloads> Get-Help Copy-Item -examples
```

## Listing Symbolic Links and Targets

```powershell
dir 'd:\Temp' -recurse -force | ?{$_.LinkType} | select FullName,LinkType,@{ Name = "Targets"; Expression={$_.Target -join "`t"} }
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

**Ammed a file with the `-Amend` flag**

```powershell
Command | Out-File -FilePath -Amend file.txt
```

## Write a Powershell Script (for Aliases)

Simple. For example...

Open a Windows PowerShell window and type:

```shell
nvim $profile
```

Then create a function, such as:

```powershell
function goSomewhereThenOpenGoogleThenDeleteSomething {
    cd C:\Users\
    Start-Process -FilePath "http://www.google.com"
    rm fileName.txt
}
```

Then type this under the function name:

```powershell
Set-Alias google goSomewhereThenOpenGoogleThenDeleteSomething
```

Now you can type the word "google" into Windows PowerShell and have it execute the code within your function!

### Another Example of writing a Powershell Script (for Aliases)

You will have to create a function first, that has your command in it. Then create an alias to that function.

**This is using the Powershell command line:**

```powershell
PS C:\Users\jpogran\code\git\scripts> function get-gitstatus { git status }

PS C:\Users\jpogran\code\git\scripts> get-gitstatus

# On branch master
nothing to commit (working directory clean)

PS C:\Users\jpogran\code\git\scripts> Set-Alias -Name gs -Value get-gitstatus

PS C:\Users\jpogran\code\git\scripts> gs

# On branch master
nothing to commit (working directory clean)
```

**This is inside the `$profile` file:**

```powershell
function get-gitstatus {
  git status
}

Set-Alias -Name gs -Value get-gitstatus
```
---

> Not quite sure what I pasted below this line but someday I'll check it out.

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

```powershell
# List Paths
$Env:Path

```

```powershell
#Sample Output for Path Environmental Variable
C:\Program Files\Common Files\Microsoft Shared\Windows Live;C:\Program Files (x86)\Common Files\Microsoft Shared\Windows Live;C:\Program Files\Common Files\Microsoft Shared\Microsoft Online Services;C:\Windows\System32\WindowsPowerShell\v1.0\

```

**Note 1:** You really do need that $dollar sign.  Plain Env:Path does not work.

**Note 2:** Observe a semi-colon between each item; this is valuable information if you need to append more Path values.

See here for a refresher on [PowerShell’s Environmental Variables’](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm) drive.

**\[Environment\] Method**  
Here is an alternative method which lists the path values, but employs the base .Net Framework elements.

```powershell
# List PowerShell's Paths
Clear-Host
[Environment]::GetEnvironmentVariable("Path")

```

**Note 3:** My point is to plant the idea that you could modify the “Path” with the sister command SetEnvironmentalVariable.

### Problem Changing Environment Variable Values with PowerShell

When you change the value of an environment variable using PowerShell commands, the changes only affect the current session. This behavior mimics using the Set command of previous Windows operating systems.

You can use PowerShell to make a persistent change, the technique involves making changes the registry values.  Firstly,
we will display the Environment values in the registry, then we will append another location.

I have also seen suggestions for putting SetEnvironmentalVariable commands in the profile files, Microsoft.PowerShell\_profile, Microsoft.PowerShellISE\_profile or [profile.ps1](https://www.computerperformance.co.uk/powershell/env-path/powershell_profile_ps1.htm).

### Retrieving Path Info from the Registry

The solution to the temporary nature of PowerShell’s changes to the environmental variable values is to script 
persistent registry modifications.  This is the equivalent of making changes to the Advanced system settings in the Control Panel.

```powershell
# List PowerShell's Paths
Clear-Host
$Reg = "Registry::HKLM\System\CurrentControlSet\Control\Session Manager\Environment"
(Get-ItemProperty -Path "$Reg" -Name PATH).Path

```

**Permanently Modifying the Env:Path**

```powershell
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

Firstly, if there is a GUI that corresponds to my PowerShell script, then I like to examine its menus to check that my 
script is working, and to give me ideas to improve my code.  The screenshot below is taken from the Control Panel.

[![PowerShell Env:Path](:/533cbb0e67f84f7a8754f8bc756a0537)](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm)

The registry script (above) achieves the same result as pressing the ‘Edit…’ button in the Advanced tab of the System Properties.

### Function Add-Path

```powershell
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

### Further Research on Env:Path

Here are ideas to discover more about Environmental Variables.

**Env:PathExt  
**In addition to Env:Path, there is a variable called Env:PathExt

```powershell
Clear-Host
$Env:PathExt

```

```powershell
#Sample Env: extensions
.COM;.EXE;.BAT;.CMD;
.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC;.CPL

```

**Get-Member  
**In this instance, Get-Member provides more methods than properties.

```powershell
Clear-Host
$Env:Path | Get-Member

```

**Help About\_Environment\_Variables  
**For find out more about Environmental Variables, PowerShell provides this Help About… file.

```powershell
Clear-Host
Help About_Environment_Variables

```

**Note 6:** This shows that PowerShell considers Env: as a drive, similar to regular file system drives such as C:\\.

**List Environmental Variables  
**Change the location to the Env: drive and then call for GCI (Get-ChildItem).

```powershell
# List PowerShell's Environmental Variables
Set-Location Env:
Get-ChildItem

```

---

There are other ways of listing the environmental variables, for example:  
Get-Item Env:

[See more about PowerShell’s Environmental Variables »](https://www.computerperformance.co.uk/powershell/env-path/powershell_environmental_variables.htm)

### Summary of PowerShell’s Env:Path

If you wish to add locations to the path environmental variable then you can use PowerShell rather than the GUI in the 
Control Panel.  If you type just the name of an executable, the operating system locates the program by searching 
through the values stored in the Path Variable.

