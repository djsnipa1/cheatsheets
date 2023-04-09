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
## `tar` commands

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


