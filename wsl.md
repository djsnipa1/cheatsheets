# WSL Cheatsheet

## [Mounting USB drives in Windows Subsystem for Linux](https://www.scivision.dev/mount-usb-drives-windows-subsystem-for-linux/)

Windows Subsystem for Linux can use (mount):

*   SD card
*   USB drives
*   CD drives (CDFS)
*   Network drives
*   UNC paths


### Local storage / drives

Drives formatted as FAT, ExFAT or NTFS can be mounted in WSL. For this example, we assume the drive shows in Windows as `F:\` If Windows changes the USB drive letter on a subsequent session, you need to repeat this process.

The commands are typed into the Windows Subsystem for Linux Terminal.

Create a mount location in WSL:

```sh

mkdir /mnt/f

```

Mount the drive in WSL:

```sh

mount -t drvfs f: /mnt/f

```

After this one\-time setup, one can create and manipulate files from both Windows and WSL on the same drive.


### network storage

Here we assume:

*   networked storage is already showing in Windows under `\\server\share`
*   we want to access this network storage from WSL as `/mnt/share`

Create a mount location in WSL:

```sh

mkdir /mnt/share

```

Mount the network share in WSL:

```sh

mount -t drvfs '\\server\share' /mnt/share

```

---
