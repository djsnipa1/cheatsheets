# `ish` (iOS)

## Installing Alpine Linux `apk` Package Manager

```shell
wget -qO- http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86/apk-tools-static-2.10.5-r1.apk | tar -xz sbin/apk.static && ./sbin/apk.static add apk-tools && rm sbin/apk.static && rmdir sbin 2> /dev/null
```

## Mounting Filesystem

```shell
mkdir mnt
mount -t ios . mnt 
```

select any location
## Mounting an iOS Files location into `ish`

The following example mounts the location you specify, in the iOS Files popup that happens after the conmand is run. It places that location in the `filez` directory as specified.

```shell
mount -t ios filez /mnt
```

## Using clipboard (when "paste" button isn't working)

This will put clipboard contents to `stdout`. 
```shell
cat /dev/clipboard

# save clipboard to a file
cat /dev/clipboard > file.txt
```

