# Command Line

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
-------------------------

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

(Also, on many systems, when you download the tar.gz from a web browser, an unpacker will open, and you can just use that.)

### For just .gz (.gzip)

In some cases the file is just a gzip format, not tar. Then you can use:

```shell
gunzip rebol.gz
```

In order to execute it, you will need to add execute permissions to the file:

```shell
chmod +x rebol
```

---

#  Command Line Notes

_September 3,2019_

[Courses Dashboard | Wes Bos](https://courses.wesbos.com/account/access/5cdc7ba285f96c03c1e44b42/view/195975829)

`take` - makes an new directory and puts you in it

**History**
Example `git ` and <kbd>⇧</kbd> goes through all `git ` command history 

**zsh**

<kbd>CTRL</kbd> + <kbd>R</kbd> lets you search through recent commands
