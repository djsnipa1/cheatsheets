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
