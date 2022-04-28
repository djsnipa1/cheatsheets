# Shell Scripts

## One-liner `install.sh` from github

```bash
wget -O - https://raw.githubusercontent.com/<username>/<project>/<branch>/<path>/<file> | bash
```
Here is my current one-liner that I've been using to install deps on [gitpod.io](https://gitpod.io)
```bash
wget -O - https://raw.githubusercontent.com/djsnipa1/psytrance-new-releases/master/install.sh | bash
```
## Multiline strings

The string after << indicates where to stop.

```bash
cat << EndOfMessage
This is line 1.
This is line 2.
Line 3.
EndOfMessage
```

To send these lines to a file, use:
```bash
cat > $FILE <<- EOM
Line 1.
Line 2.
EOM
```
