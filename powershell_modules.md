# Powershell Modules

## 7zip4Powershell

Powershell module for creating and extracting 7-Zip archives supporting Powershell's `WriteProgress` API.

![Screenshot](https://raw.githubusercontent.com/thoemmi/7Zip4Powershell/master/Assets/compression.gif)


> # Note
> Please note that this repository is not maintained anymore. I've created it a couple
> of years ago to fit my own needs (just compressing a single folder). I love that lots
> of other users find my package helpful.
>
> I really appreciated if you report issues or suggest new feature. However,
> I don't use this package myself anymore, and I don't have the time to
> maintain it appropriately. So please don't expect me to fix any bugs. Any Pull
> Request is welcome though.

### Usage

The syntax is simple as this:

```powershell

Expand-7Zip
    [-ArchiveFileName] <string>
    [-TargetPath] <string>
    [-Password <string>] | [-SecurePassword <securestring>]
    [<CommonParameters>]

Compress-7Zip
    [-ArchiveFileName] <string>
    [-Path] <string>
    [[-Filter] <string>]
    [-OutputPath] <string>
    [-Format <OutputFormat> {Auto | SevenZip | Zip | GZip | BZip2 | Tar | XZ}]
    [-CompressionLevel <CompressionLevel> {None | Fast | Low | Normal | High | Ultra}]
    [-CompressionMethod <CompressionMethod> {Copy | Deflate | Deflate64 | BZip2 | Lzma | Lzma2 | Ppmd | Default}]
    [-Password <string>] | [-SecurePassword <securestring>]
    [-CustomInitialization <ScriptBlock>]
    [-EncryptFilenames]
    [-VolumeSize <int>]
    [-FlattenDirectoryStructure]
    [-SkipEmptyDirectories]
    [-PreserveDirectoryRoot]
    [-DisableRecursion]
    [-Append]
    [<CommonParameters>]

Get-7Zip
    [-ArchiveFileName] <string[]>
    [-Password <string>] | [-SecurePassword <securestring>]
    [<CommonParameters>]

Get-7ZipInformation
    [-ArchiveFileName] <string[]>
    [-Password <string>] | [-SecurePassword <securestring>]
    [<CommonParameters>]
    
```

## Customization

`Compress-7Zip` accepts a script block for customization. The script block gets passed the current
`SevenZipCompressor` instance. E.g. you can set the multithread mode this way:

```powershell
$initScript = {
    param ($compressor)
    $compressor.CustomParameters.Add("mt", "off")
}

Compress-7Zip -Path . -ArchiveFileName demo.7z -CustomInitialization $initScript
```

A list of all custom parameters can be found [here](https://sevenzip.osdn.jp/chm/cmdline/switches/method.htm).

---


