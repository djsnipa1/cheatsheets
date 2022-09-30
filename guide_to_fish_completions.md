![](https://miro.medium.com/max/1400/1*XFhvIc8AUGsCN1vgoY2lQw.png)

# A guide for fish shell completions

Fish shell is great and if you are reading this is because you already know that. So I’m assuming that you are familiar with all the fish shell greatness.

Completions, right that’s the topic. Fish completions don’t come out of the box for most of the tools so you either find them yourself by searching for some open source completions done by someone, or you create your own. There’s also a third option which is you ignore all of that and live your life without completions, but let’s skip this option.

A bit of context, recently I have started doing a lot of work around `aws` using terraform, to help us manage access to our developers we use `okta`. To run commands against our infrastructure we would run something like:

```shell
aws-okta exec some-profile -- aws s3 ls
```

The challenge of not having any completions is that firstly my memory sucks so I need to constantly do reverse searches secondly, I don’t remember all of the names of the profiles we have, as we have multiple profiles for each environment, a lot of environments and last but not least we also lose `aws-cli` completions. Now writing completions can be hard, see for yourself the [git completions](https://github.com/fish-shell/fish-shell/blob/master/share/completions/git.fish) provided by fish. That’s because although they seem simple there are tons of edge cases that can generate false positives and false negatives. In this guide we won’t try to solve every single possible scenario instead, we will provide completions for the happy paths which make 99% of the use cases.

Let’s start with the most basic scenario when we type `aws-okta` and press tab we should be getting completions for the available `aws-okta` commands. So how do we start with completions? We just create a file in our fish completions folder, the default is `~/.config/fish/completions/`. If you don’t have a `completions` directory, create one. We then create a file inside that folder with the name of the command, in this case, `aws-okta.fish`.

If we run `aws-okta — help` we get this:

```shell
aws-okta allows you to authenticate with AWS using your okta credentials
Usage:
  aws-okta [command]
Available Commands:
  add         add your okta credentials
  exec        exec will run the command specified with aws credentials set in the environment
  help        Help about any command
  login       login will authenticate you through okta and allow you to access your AWS environment through a browser
  version     print version
Flags:
  -b, --backend string   Secret backend to use [keychain file]
  -d, --debug            Enable debug logging
  -h, --help             help for aws-okta
Use "aws-okta [command] --help" for more information about a command.
```

Let’s just add completions for these 5 commands, and for the purpose of this guide we will ignore the flags. On our `~/.config/fish/completions/aws-okta.fish` we will add the following:

```shell
set -l okta_commands add exec help login version
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a $okta_commands
```

On the first line, we create a list of our commands, on the second line we just provide completions for our `aws-okta` command. If you have never seen the `complete` command before, don’t panic, you can find the full list of the available options [here](https://fishshell.com/docs/current/commands.html#complete).

Let’s breakdown the options we are passing to our `complete` command. The `-f` or `--no-files` mean that we don’t want to provide any filenames of the current directory, as options for the autocomplete. The `-c` or `-- command` is to specify the command we want to provide completions for. So far pretty simple, let’s skip the `-n` for now and let’s go to the `-a` or `-- arguments`. This option represents the arguments we want to pass to our completion and in this case, we pass our list of commands `$okta_commands`. The `-n` or `—- condition` flag is something that allows us to enable and disable completions based on the condition. The condition can be any shell command but it must return `0` if we want to apply completions. We can be super creative with it and do whatever we want, in our very simple example we use an existing helper function from fish. So this is where things start to get a bit complicated and if you get this part you get completions sorted out for life.

With this `-n “not __fish_seen_subcommand_from $okta_commands”` what we are saying is, if any of the commands that are specified in our list `$okta_commands` have not been seen, then we want to provide completions. Confused? Don’t worry this example is going to make things clear, nothing like a good example. If we didn’t specify that condition and had something like: `complete -f -c aws-okta -a “$okta_commands”` if we typed our `aws-okta` command and press tab, we would get our list`$okta_commands` displayed. The problem is that after we get our first command completed, we end up with something like this: `aws-okta add`. If we press tab again what do we get? The same list again. This is problematic because we want to add more completions and if we don’t create conditions for our completions, then our options will just stack on top of each other and we will be also providing wrong completions. Our condition `-n “not __fish_seen_subcommand_from $okta_commands”` is not bullet proof. If we type `aws-okta yolo` and then press tab we will get our list and that’s because our condition it’s only doing one thing, it checks if any of the `$okta_commands` has been typed, if not then those are the options we want to provide.

We are almost over with the first part. Let’s add descriptions for all of our `$okta_commands`

```shell
set -l okta_commands add exec help login version
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a add -d 'add your okta credentials'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a exec -d 'exec will run the command specified with aws credentials set in the environment'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a help -d 'help about any command'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a login -d 'login will authenticate you through okta and allow you to access your AWS environment through a browser'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a version -d 'print version'
```

So now we have exactly the same completions as before, except now each command has a beautiful description. As you can see the only difference between each line is the argument and the description.

![](https://miro.medium.com/max/540/1*IE-rPHqj3a7-UZKDDzZwCA.png)
Completions without description

![](https://miro.medium.com/max/1400/1*OfIqcbpgTU2R-GwHLbn8bQ.png)
Completions with description

Great so we did our first step, now we are able to provide completions for the first part of our command with meaningful descriptions.

Side note. The best way to approach completions is by starting small and then slowly iterate over and fix edge cases. In the next section, we will be learning how to fix some of the edge cases and using some of the common practices.

## Adding dynamic and nested completions

We were a bit lazy and just decided to provide our list as an option. But we can be a bit more elegant. This means extra work but it also makes completions more useful.

The next step is to provide completions to any of the `okta_commands`, for the sake of simplicity let’s just focus on the `exec` command. But before we progress if you want to follow along. You can copy some of the commands and work on your local machine. You don’t need to actual install `aws-okta` you can create a dummy function, by just creating a file in `~/.config/fish/functions/aws-okta.fish`. If the directory `functions` doesn’t exist, create it, and paste the following:

```shell
function aws-okta
  echo $argv
end
```

This is a dummy function that just echoes its arguments, but it’s enough to play around with our completions.

Still with me? Hopefully everything has been making sense. Getting back to the initial command:

```shell
aws-okta exec some-profile -- aws s3 ls
```

We now want to provide auto completions to the `exec` command. These completions are going to be generated dynamically, don’t worry it’s simpler than it sounds.
j
To give you some context, `aws-okta` reads your aws `.config` file, you then provide the name of profile you want to use.

Here’s what a file looks like:

```
[okta]
aws_saml_url = home/amazon_aws/0ac4qfegf372HSvKF6a3/965
[profile okta-dev]
role_arn = arn:aws:iam::<account-id>:role/<okta-role-name>
region = <region>
[profile okta-staging]
role_arn = arn:aws:iam::<account-id>:role/<okta-role-name>
region = <region>
[profile okta-prod]
role_arn = arn:aws:iam::<account-id>:role/<okta-role-name>
region = <region>
```

So if you would like to login into prod you would need to type `aws-okta exec okta-prod`

So ideally what we would like is to type `aws-okta exec` press tab and get `okta-dev`, `okta-staging` and `okta-prod` as options for completions. So how would we do that? Well, you do remember on our first example when we provided a list to our `-a` flag and it magically populated our completions with the options. We just have to the same. We can either just hardcore the profiles as list or we can read them from the file. Let’s do it the hard way and get those profiles from the file. Without getting in too much detail about the `__fish_okta_complete_profiles` function, it greps all the lines that start with `[` but not the first one `[okta]` and then using `awk` we extract the name of the profiles. Behold the final result:

```fish
function __fish_okta_complete_profiles
  cat ~/.aws/config | grep -e "\[[^(okta)]" | awk -F'[] []' '{print $3}'
end

set -l okta_commands add exec help login version
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a add -d 'add your okta credentials'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a exec -d 'exec will run the command specified with aws credentials set in the environment'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a help -d 'help about any command'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a login -d 'login will authenticate you through okta and allow you to access your AWS environment through a browser'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a version -d 'print version'

complete -f -c aws-okta -n "__fish_seen_subcommand_from exec; and not __fish_seen_subcommand_from (__fish_okta_complete_profiles)" -a "(__fish_okta_complete_profiles)"
```

Let’s break line 12.
Our condition to provide completions is:
if we have seen the `exec` command typed and if we haven’t seen any of the existing profiles in our file also typed, then we want to provide the profiles as completion. Again these conditions that we have been using are pretty basic, but they will suffice for 99% of the cases and sometimes 99% is more than enough (At least is way better than 0%). Just a small note, in our condition and in the `-a` flag we are calling our function, that’s why we need to wrap it with `()`.

Simple, right? We are almost finished, just two more steps. Oh and by the way if you want to test this bit on your computer feel free to copy the `okta` profiles, create a file in `~/.aws/config` and just paste the profiles above. Or if you prefer creating a file in another directory remember to also update our function with the correct path.

The next completion is quite simple and its solely existence is due to my laziness, that’s right the next completion just adds the `--`.

```fish
function __fish_okta_complete_profiles
  cat ~/.aws/config | grep -e "\[[^(okta)]" | awk -F'[] []' '{print $3}'
end

set -l okta_commands add exec help login version
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a add -d 'add your okta credentials'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a exec -d 'exec will run the command specified with aws credentials set in the environment'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a help -d 'help about any command'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a login -d 'login will authenticate you through okta and allow you to access your AWS environment through a browser'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a version -d 'print version'

complete -f -c aws-okta -n "__fish_seen_subcommand_from exec; and not __fish_seen_subcommand_from (__fish_okta_complete_profiles)" -a "(__fish_okta_complete_profiles)"

complete -f -c aws-okta -n "__fish_seen_subcommand_from (__fish_okta_complete_profiles); and not __fish_seen_subcommand_from --" -a "--"
```

By now you should have started seeing a pattern in our conditions, we want to provide `—-` if we have seen any of the profiles that exist on our file and we haven’t seen a `—-` typed, then we provide that option. Because this our only completion for this specific condition then fish will insert `--` automatically. Remember when I said these completions work for 99% the cases, if by any chances you decide to type `aws-okta okta-prod` and then press tab can you guess what would happen? I will give you little hint.

Our condition for the `--` says that if we have typed a profile that exists in the file and if there’s no `--` typed then we provide `--` as completion. It’s not that bad, but! if we look on our previous completions which have a description, their condition is: if we haven’t typed any of the `$okta_commands` then we provide the `$okta_commands` which is also a valid condition, so as you may have guessed our completions will be all the `$okta_commands` plus the `--`.

We are almost finished, we just need the last bit which to be honest is the most important one. One of the drawbacks of using `aws-okta` is that I lose my autocompletions for `terraform` and `aws-cli`. Because we run those after the `okta` `exec` if I press tab, nothing happens. Let’s fix that! Our last bit is if we type `aws` or `terraform` after the `--` we want to get the original completions for those commands, and everything after `aws s3` should also show completions. In fact we should show completions for any arbitrary command that we run, either be it `aws`, `terraform` or even a custom function with completions created by us. Let’s break this into two parts, firstly we need to get everything after `--`. Secondly, regardless of what we have typed we just need to get completions for it.

So without further ado, our final version:

```fish
function __fish_okta_complete_profiles
  cat ~/.aws/config | grep -e "\[[^(okta)]" | awk -F'[] []' '{print $3}'
end

function __fish_complete_okta_subcommand
  set -l tokens (commandline -opc) (commandline -ct)
  set -l index (contains -i -- -- (commandline -opc))
  set -e tokens[1..$index]
  complete -C"$tokens"
end

set -l okta_commands add exec help login version
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a add -d 'add your okta credentials'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a exec -d 'exec will run the command specified with aws credentials set in the environment'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a help -d 'help about any command'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a login -d 'login will authenticate you through okta and allow you to access your AWS environment through a browser'
complete -f -c aws-okta -n "not __fish_seen_subcommand_from $okta_commands" -a version -d 'print version'

complete -f -c aws-okta -n "__fish_seen_subcommand_from exec; and not __fish_seen_subcommand_from (__fish_okta_complete_profiles)" -a "(__fish_okta_complete_profiles)"

complete -f -c aws-okta -n "__fish_seen_subcommand_from (__fish_okta_complete_profiles); and not __fish_seen_subcommand_from --" -a "--"

complete -c aws-okta -n "contains -- -- (commandline -opc)" -x -a "(__fish_complete_okta_subcommand)"
```

There’s a lot to digest, let’s start with our condition:

```shell
contains -- -- (commandline -opc)
```

This is basically saying if `--` is present in the entire command the user has typed, then we want to do some completions. Note that we pass `--` twice, that’s because we don’t want `contains` to think that we are trying to pass an option.

As for the completion itself, we are providing the options for whatever is after `--`, for that we have created the following function:

```shell
function __fish_complete_okta_subcommand
  set -l tokens (commandline -opc) (commandline -ct)
  set -l index (contains -i -- -- (commandline -opc))
  set -e tokens[1..$index]
  complete -C"$tokens"
end
```

Inside this function what we are actually doing is creating a variable `$tokens`, which is a list with all the tokens inserted by the user until the cursor. So if our cursor is at the end of the line, then our tokens are basically the entire command except for the character under our cursor which is what `(commandline -opc)` does. Then `(commandline -ct)` gets the character under our cursor. Now we have our entire command tokenised. That’s pretty much useless since we wanted everything after `--`, not the entire command. So we use the command `contains`, but this time with `-i` flag which returns the index of the thing we are trying to find, the `--`. Since we know what’s the index, we just need to delete everything in our list of `$tokens` until the index. That’s what this command `set -e tokens[1..$index]` does, deletes everything from the first token until the index of `--`. Phew!! all this work just to get the bit after `--`. Now that we have that part, things get pretty easy as we just need to run completions on our list of`$tokens` using the `-C` flag, `complete -C”$tokens”` (**Note** there’s **no space** between the flag `-C`and the quotes). With all of this we are basically saying to fish, “Hey! can we get completions for anything that we type after the `--`?”. In fact you can try this on your shell by doing `complete -C"git checkout "` (note there’s a space after `checkout)`.

# Conclusion

I hope that you found this post useful and that it answered some of the questions you had about fish completions. I tried to be as thorough as I could, so even if you don’t have any experience with fish and fish scripting you could follow along.

I would like to thank all the fish community and the contributors, especially **faho** for answering all of my questions related to fish scripting. You for reading all of this, I really hope that you found it useful, if not I’m sorry that I have wasted your time. Last but not least, my brother who showed me fish 6 years ago, thanks ***puto!***

