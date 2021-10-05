# Command Line

## Cleaning and clearing logfiles

### journal

Clearing out logs older than 10 days

```shell
journalctl --vacuum-time=10d
```

Clearing out journal more than 2 gigs

```shell
journalctl --vacuum-size=2G
```

### Any log files

Get sizes 

```shell
du -h /var/log/
```

Clear logs that are huge

```shell
cat /dev/null > whatever_log.log 
```

## Setting up webservers

See [web_servers.md](web_servers.md)

## `diff` files in vim

```shell
nvim -d file1.txt file2.txt`
```

`diff` **online** files in vim

```shell
nvim -d <(curl -sL "https://crap.com/file1.txt") \
<(curl -sL "https://crap.com/file2.txt")
```

## `curl`

See [curl.md](curl.md)

## Showing Key Codes

```shell
xev -event keyboard
```

-

## Find text in a file

```shell
find . -type f -exec grep "example" '{}' \; -print
```

`f` = file

## Encrypt and Decrypt

**Encrypt:**
**EASIEST OPTION**

```bash
gpg -c file.txt
```

Alternative method:

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -in file .txt -out file.enc
```

**Decrypt:**

```bash
gpg -d file.gpg
```

Alternative Method:
add `-d` to the above command

---

## Adding to $PATH

Simply add **`/place/with/the/file`** to the **`$PATH`** variable with the following command:

```bash
export PATH=$PATH:/place/with/the/file
```

---

## Finding directories over/under a certain size

```shell
du -sm * | awk '$1 > 1000'
```

This shows directories larger than 1 gig

---


## Star Wars Asciimation

```shell
telnet towel.blinkenlights.n
```

---

## Umcompress & Compress

### 7zip

#### Unzip zip file

```shell
7z.exe e *.zip
```

#### List files in archive

```shell
7z.exe l -r filename.zip
```

### For tar.gz

To unpack a tar.gz file, you can use the **tar** command from the shell. Here's an example:

```shell
tar -xzf rebol.tar.gz
```

The result will be a new directory containing the files.

### For just .gz (.gzip)

In some cases the file is just a gzip format, not tar. Then you can use:

```shell
gunzip rebol.gz
```

---

## Command Line Notes

**September 3,2019**

[Courses Dashboard | Wes Bos](https://courses.wesbos.com/account/access/5cdc7ba285f96c03c1e44b42/view/195975829)

**zsh**
<kbd>CTRL</kbd> + <kbd>R</kbd> lets you search through recent commands

**History**
Example `git ` and <kbd>⇧</kbd> goes through all `git` command history 

