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



