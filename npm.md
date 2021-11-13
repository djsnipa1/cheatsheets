# NPM

Delete all unwanted or not needed `.node_modules` folders!

```shell
npx npkill
```

---

## NVM

Install with this script:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

After Installation:

To install current version of node:

`nvm install node`

To install a specific version of node:

`nvm install 6.14.4 # or 10.10.0, 8.9.1, etc`

To get a listing of all the versions:

`nvm ls-remote`

After node installation, open a _new shell_ and run:

`nvm use node`

---

[Don’t Use `sudo` with `npm` …still | by Andrew Crites | Medium](https://medium.com/@ExplosionPills/dont-use-sudo-with-npm-still-66e609f5f92)

## Summary
To summarize, you can use the following steps to update your local OS X machine to allow you to use global Node.js modules and different versions of node without using sudo.
brew install node, or apt-get install node or whatever you need to do to get node up on your machine. This should include executables npm and yarn.
Set your prefix for global installs, e.g. npm config set prefix ~/.npm
Update your PATH to include ~/.npm/bin. For example: echo 'export PATH="$HOME/.npm/bin:$PATH"' >> ~/.zshrc if you’re using zsh.
At this point you’re good to go for installing global modules. I think it’s good to avoid installing global modules except for commands that you will use frequently that won’t be installed to a corresponding project. For one-off commands such as initiating projects that you will only do every once in a while, you can use npx.
Next, use yarn global add n which should create ~/.npm/bin/n.
Do the equivalent of echo 'export N_PREFIX="$HOME/.n"' >> ~/.zshrc for your shell configuration
Now you can run n to install different versions of node to a directory that you control.
On build / production environments you should avoid global installs of modules as they are generally not needed. If they’re required, you can still do a similar setup with a user who only has permissions to install global node modules to a particular directory using --prefix and so on.

