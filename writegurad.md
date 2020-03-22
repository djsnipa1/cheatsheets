# Writeguard

## Mediatemple Info

### Permissions

Rule of thumb for correct permissions:

*   Folders: 755
*   Static Content: 644
*   Dynamic Content: 700

**TIP:**
>Linux permissions can be represented with numbers, letters, or words. They also include an entry for Owner, Group, and Everyone.

| code | `ls`  |
|--------|-------|
| **755** | `drwxr-xr-x` |
|  **644** | `-rw-r--r--` |
| **700** | `-rwx------` |

*   **755** stands for Owner: read, write, execute; Group: read, execute; Everyone: read, execute
*   **644** stands for Owner: read, write; Group: read, Everyone: read
*   **700** stands for Owner: read, write, execute; Group: (none); Everyone: (none)

### Ownership

In Linux file structures, every file and folder is assigned to an Owner and a Group. The correct owner and group for your server are as follows, listed like this:

*   **Plesk server** - note that domainuser is the FTP user for that domain, and example.com is the specific domain in question:
    *   /var/www/vhosts/example.com/  - __root:root__
    *   /var/www/vhosts/example.com/httpdocs/ - __domainuser:psaserv__
    *   /var/www/vhosts/example.com/httpdocs/index.html - __domainuser:psacln__


## Changing website permissions

Got info from [here](https://www.reddit.com/r/cs50/comments/5055ti/403_forbidden_permissions_chmod_the_definitive/)

_This might have to be done like this:_

```bash
find . -name *.php -exec chmod 640 {} \;
```
_because the `xargs` pipe didn't work correctly for me..._

This command finds all php files and lists their permissions in the `ls -l` display

```bash
find . -name *.php | xargs ls -l
```
Changes all directories to 711 `drwx--x--x`

```bash
find . -type d | xargs chmod 711
```

Changes all php files to their correct permissions

```bash
find . -name *.php | xargs chmod 640
```

Change html, css, js, and images to the following

```bash
find . -name *.html | xargs chmod 644
```

__REFERENCE:__

```bash
cd ~/workspace/pset7
find . -type d | xargs chmod 711
find . -name *.php | xargs chmod 640
find . -name *.json | xargs chmod 640
find . -name *.html | xargs chmod 644
find . -name *.css | xargs chmod 644
find . -name *.png | xargs chmod 644
find . -name *.js | xargs chmod 644
chmod 644 ./public/fonts/*
```


