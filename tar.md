# `tar`

## Make a `.tar.gz` file of each directory

```bash
find . -maxdepth 1 -mindepth 1 -type d -exec tar cvzf {}.tar.gz {}  \;
```

---
## Backing up the current user's HOME

An approach to backing up the current user's HOME, using `tar(1)` and Gzip compression. Permissions (modes) will be preserved. The filename format will be: `UID:GID_DATE.tgz`

Replace 'DEVICE' with whichever device is applicable to you, but note that it must be in the `/media/USER` (where `USER` is the username) directory, else this won't work, unless you edit the formatting section of `printf`.

```bash
tar -czvpf "$(printf '/media/%s/%s/%d:%d_%(%F)T.tgz' "$USER" 'DEVICE' ${UID:-`id -u`} ${GID:-`id -g`} -1)" "$HOME"
```
---
## How to Backup a specific user's home directory?

Use the following command to take a backup of a user's home directory:

In this example, we will backup our test user – **`'2daygeek`**'s home directory, and the output file will be saved in the ** `'/backup'`** directory.

```
# tar -zcvpf /backup/2daygeek-backup-$(date +%d-%m-%Y).tar.gz /home/2daygeek
```
Due to some reason, if you would like to exclude some folders from backing up, then use the following format:

Note: The below example will exclude the entire ** `'demo'`** directory and archive the rest of the files and folders.

```
tar --exclude='/home/2daygeek/demo' -zcvpf /backup/2daygeek-backup-$(date +%d-%m-%Y).tar.gz /home/2daygeek
```

Similarly, if you would like to exclude some of the pattern files or group of files, then use the following format:

Note: The below example will exclude the ** `'.mp3 & .avi'`** files from ** `'demo'`** directory and archive the rest of the files.

```
tar -- **exclude**={'*.mp3','*.avi'} '/home/2daygeek/ **demo**/' -zcvpf /backup/2daygeek-backup-$(date +%d-%m-%Y).tar.gz /home/2daygeek
```

## How to Backup a single user's home directory using shell script?

This shell script allows you to backup the given user's home directory.

To do so, add the following shell script in a file:

```
#!/bin/bash
DATE=$(date +%d-%m-%Y)
BACKUP_DIR="/backup"

#To backup 2daygeek's home directory
tar -zcvpf $BACKUP_DIR/$USER-$DATE.tar.gz /home/$USER

#To delete files older than 10 days
find $BACKUP_DIR/* -mtime +10 -exec rm {} \;
```

---
## `tar` commands

```bash
tar -zcvpf /[Backup_File_Location]/[Backup_Filename] /[User's_Home_Directory_Location]

z : Compress the backup file with ‘gzip’ to make it small size.
c : Create a new backup archive.
v : verbosely list files which are processed.
p : Preserves the permissions of the files put in the archive for later restoration.
f : use archive file or device ARCHIVE.
```

To extract an uncompressed archive:
`tar -xvf /path/to/foo.tar`

To extract a .tar in specified directory:
`tar -xvf /path/to/foo.tar -C /path/to/destination/`

To create an uncompressed archive:
`tar -cvf /path/to/foo.tar /path/to/foo/`

To extract a .tgz or .tar.gz archive:
`tar -xzvf /path/to/foo.tgz`
`tar -xzvf /path/to/foo.tar.gz`

To create a .tgz or .tar.gz archive:
`tar -czvf /path/to/foo.tgz /path/to/foo/`
`tar -czvf /path/to/foo.tar.gz /path/to/foo/`

To list the content of an .tgz or .tar.gz archive:
`tar -tzvf /path/to/foo.tgz`
`tar -tzvf /path/to/foo.tar.gz`


