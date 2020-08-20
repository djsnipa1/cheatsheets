# Windows Command Line

## Mounting and Using Network Drives

use `net use`

example:

```shell
net use X: \\SERVER\Share
```

Where `X:` is the drive letter you wish to map the share to, and `\\SERVER\Share` is the UNC path to the share. This should make the share visible in `My Computer` and the command line as well like all other shares mapped through the GUI.

In order to later disconnect the share, you would use

```shell
net use X: /delete
```

> if you want to keep this mapping you can add the switch `/persistent:yes`
> Also, sometimes when you try to assign to something that is already assigned you may have to first `/delete` the mapping.
> This is the case for printers mapped to LPT ports at least, and if you can't seem to get it working, try that.

> Answer taken from [this link](https://superuser.com/questions/52220/how-do-i-connect-to-a-network-share-via-the-windows-command-prompt)
