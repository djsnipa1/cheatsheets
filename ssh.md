# SSH

If you use a SSH config file to connect, you can embed a startup command that will only execute when you connect the host.

For this insert / edit the following into your `~/.ssh/config` on your client machine:

```
Host myhost
  HostName *.*.*.*
  User root
  RequestTTY force
  RemoteCommand cd / && bash -i
```

Put the appropriate hostname and append a new line `Port XX` if the port differs from 22. The sample will `cd` in the root of the server. `&& bash -i` and `RequestTTY force` are essential to continue usage of the remote terminal.

To connect to your host you have to install your public key on the target machine that you can retrieve like so:

```bash
cat ~/.ssh/id_rsa.pub
```

And install on the remote like so:

```bash
mkdir -p ~/.ssh 
chmod 700 ~/.ssh 
touch ~/.ssh/authorized_keys 
chmod 644 ~/.ssh/authorized_keys 
echo "YOUR_PUBLIC_KEY" >> ~/.ssh/authorized_keys
```

Then you can simply connect the machine like so:

```bash
ssh myhost
```

And it will connect and execute the `RemoteCommand`.

---

## `fissh` script
source: [ssh - How to use fish on remote servers that have it installed without changing login shell? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/476107/how-to-use-fish-on-remote-servers-that-have-it-installed-without-changing-login)

```bash
#!/bin/sh
ssh "$@" -t "sh -c 'if which fish >/dev/null ; then exec fish -li; else exec \$SHELL -li; fi'"
```

`"$@"` forwards all arguments passed to ssh
`-t` forces the allocation of a tty (otherwise ssh defaults to no tty when a command is specified)
`sh -c` is required because we don't know what shell we may have on the other side - on my personal machines I do have fish as default shell, which would break on the different if syntax;
`which fish` succeeds if it finds an executable `fish`; in that case, it is exec-ed (asking for an interactive and login shell);
otherwise, we fall back to `$SHELL`, which is the default shell for the current user (`$` is escaped otherwise it gets expanded by `sh` "on this side").
`-li` is passed in either case, to make sure that we actually get a login interactive shell. While `-i` is mandated by POSIX for any shell, `-l` is "just" a common extension, but not putting it in is likely to result in bad surprises.

Notice that `stdout` of which is hidden (as in the normal case we don't care about where `fish` was found), but `stderr` (where the error message that `fish` couldn't be found) is intentionally left intact as a warning to the user that, despite our best intentions, `fish` couldn't be found.

To complete the experience, on my machines with `fish` I add the support for customized completion by creating a `~/.config/fish/completions/fissh.fish` file containing

```fish
complete -c fissh -w ssh
```
to instruct `fish` that fissh has the exact same valid completions as ssh.
