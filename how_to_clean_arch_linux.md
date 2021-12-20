# How to clean Arch Linux

**Every system becomes cluttered sooner or later and Arch Linux is not the exception. So, in this post, you will learn how to clean your Arch Linux system.**

## INTRODUCTION

Although Arch Linux takes little of disk space right after the installation, as the time passes it grows quite a lot. So, if you do not have any free space left on your computer or you just would like to keep your Arch Linux system clean, this post is all you need.

In this post, you will learn how to:

[Clean package cache](#1-clean-package-cache)
1.  [Clean package cache](#1-clean-package-cache)
2.  [Remove unused packages (orphans)](#2-remove-unused-packages-orphans)
3.  [Clean the cache in your /home directory](#3-clean-the-cache-in-your-home-directory)
4.  [Remove old config files](#4-remove-old-config-files)
5.  [Remove duplicates, empty files, empty directories and broken symlinks](#5-remove-duplicates-empty-files-empty-directories-and-broken-symlinks)
6.  [Find the largest files and directories](#6-find-the-largest-files-and-directories)
7.  [Disk cleaning programs that can do most of the steps above automatically](#7-disk-cleaning-programs-that-can-do-most-of-the-steps-above-automatically)
8.  [Clean Systemd journal](#8-clean-systemd-journal)

*NOTE that I would like to warn you that you may damage your system if you do a mistake during these procedures. So, please [back up all your files](http://averagelinuxuser.com/backup-and-restore-your-linux-system-with-rsync/) before doing anything to your system.*

## VIDEO

[SUBSCRIBE for more Linux Videos](https://www.youtube.com/AverageLinuxUser?sub_confirmation=1)

## Steps to Clean Arch Linux

### 1\. Clean package cache

Pacman, a package manager of Arch Linux, stores all downloaded packages in `/var/cache/pacman/pkg/` and it does not remove the old or uninstalled versions automatically. You might think this is a mistake, but this is done deliberately. This allows downgrading a package without the need to retrieve the previous version through the Arch Linux Archive. Or if you uninstall a program, you can easily reinstall it without a new download. If you have a slow internet connection, this may be useful. For example, you can simply install a package from this directory using the command below.

```
sudo pacman -U /var/cache/pacman/pkg/packagename

```

However, this `/var/cache/pacman/pkg/` folder can grow indefinitely in size.

![Showing the size of downloaded packages in my Arch Linux](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/1-show-the-cache-size-on-Arch-Linux-min.jpg)

Showing the size of downloaded packages in my Arch Linux

So, you need to clean it from time to time. There are two ways you can do that: **manually** and **automatically**.

#### Cleaning the cache manually

You can clean the cache manually. For example, I usually move these files to my old hard drive that I use only to store data. This way I can always access these files but they do not take valuable space on my system.

However, if you do not have extra space to store these packages, you can remove them without a backup. One option is to remove cached packages that are not currently installed:

```
sudo pacman -Sc

```

The other option is to remove all the package from the cache, including those that are installed:

```
sudo pacman -Scc

```

![Delete the PKG cache to save space](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/3-removing-all-cache-packages-min-800x531.jpg)

Delete the PKG cache to save space

And if you happen to need some of these packages after you removed them, you can go to [Arch Package Archive](https://archive.archlinux.org/) and download them manually. This is not an optimal solution if you need to download many packages because downloading them manually will take quite some time, but it is still possible.

#### Cleaning the cache Automatically

Another way to clean the `/var/cache/pacman/pkg/` directory is to **use a script** that automatically deletes all cached versions of installed and uninstalled packages, except for the most recent 3 versions. The script is called `paccache`. You can install it with the `pacman-contrib` package.

```
sudo pacman -S pacman-contrib

```

For available, options check the help menu of `paccache`.

```
paccache -h

```

![Showing the Paccache help](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/6-paccache-help-min-800x447.jpg)

Showing the Paccache help

For example, you can run it in the dry mode to see how many packages will be removed using the `-d` option. Then, you can run a real clean by using the `-r` option.

![Running paccache](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/7-running-paccache-min-800x149.jpg)

Running paccache

**Run** `paccache` **monthly**

A very useful way to use this script is to have it run automatically once a month using the [systemd timer](https://wiki.archlinux.org/index.php/Systemd/Timers#Timer_units). Basically, you need to create the file `paccache.timer` in `/etc/systemd/system/`, which will trigger `/usr/lib/systemd/system/paccache.service`.

So, you create a `paccache.timer` file with nano:

```
sudo nano /etc/systemd/system/paccache.timer

```

Then, to run this script monthly, paste the following content into this file:

```
[Unit]
Description=Clean-up old pacman pkg

[Timer]
OnCalendar=monthly
Persistent=true

[Install]
WantedBy=multi-user.target

```

After that, start the systemd service:

```
sudo systemctl enable paccache.timer
sudo systemctl start paccache.timer

```

Finally, you can check the service status.

```
sudo systemctl status paccache.timer

```

![The paccache status in systemd is active](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/9-min-1-800x279.jpg)

The paccache status in systemd is active

So, you should see the message that it is active. Now, `paccache` will run every month and clean the cache of your old and uninstalled packages.

**Run** `paccache` **after** `pacman`

Alternatively to this timer, you can also run `paccache` every time after you run `pacman`. So, you need to [create a Hook](https://wiki.archlinux.org/index.php/Pacman#Hooks) for that. Just create a file `/usr/share/libalpm/hooks/paccache.hook`.

```
sudo nano /usr/share/libalpm/hooks/paccache.hook

```

After that, add this content on the file.

```
[Trigger]
Operation = Upgrade
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
Description = Cleaning pacman cache with paccache …
When = PostTransaction
Exec = /usr/bin/paccache -r

```

Now, if I remove a package using `pacman`, `paccache` will also be executed.

![Now paccache will run after pacman](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/11-min-1-800x399.jpg)

Now paccache will run after pacman

Did not you know this way to clean up Arch Linux?

### 2\. Remove unused packages (orphans)

When you install and remove packages in Arch Linux, some unused orphans packages may remain on your system. To find them you need to run this command:

```
sudo pacman -Qtdq

```

![Showing the orphan packages](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/12-min-800x762.jpg)

Showing the orphan packages

As you can see, by executing the above command, you will be able to know which packages are orphans. To remove them, you need to modify the command with the remove action:

```
sudo pacman -Rns $(pacman -Qtdq)

```

![Removing the orphan packages](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/13-min-800x468.jpg)

Removing the orphan packages

Now, you know how to clean Arch Linux system files by removing the pkg cache and removing the orphan packages. However, there are still more things to do in your home folder.

### 3\. Clean the cache in your /home directory

In this step, I will show you how to clean Arch Linux by removing the cache files in your `/home/user` folder.

As we use our system, the cache will fill up and take up a lot of space. So, the first thing you probably would want to do is to clean cache in your user directory. If you want to check the size of your cache folder, you can do it with this command:

```
sudo du -sh ~/.cache/

```

![Show the cache folder size in the home directory](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/14-min-800x162.jpg)

Show the cache folder size in the home directory

To clean it, you need to remove all files inside it:

```
rm -rf ~/.cache/*

```

And that is it.

### 4\. Remove old config files

The configuration files of different programs are stored in `~/.config/`. You can enter it from your file manager and check if there any config files left from the programs you uninstalled. Just select those folders and delete them. But before you remove any file, I would also remind you that it is better to [have a backup of all your files](http://averagelinuxuser.com/backup-and-restore-your-linux-system-with-rsync/) before you remove anything.

![The .config folder is where the configuration files are](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/15-min-800x467.jpg)

The configuration files in ~/.config

Some old files may also be lying in `~/.local/share/`. Check it too and delete some files and folders if necessary.

### 5\. Remove duplicates, empty files, empty directories and broken symlinks

You can do even more cleaning by removing duplicated and empty files and directories. To keep some order in your system, I also recommend removing broken symlinks, e.i. links that lead to non-existing filer or folders. They do not take much space, but they clutter your system. To remove such things, you can use the program `rmlint`.

Install it:

```
sudo pacman -S rmlint

```

If you check all its options with `--help`, you will see there are pretty many. I recommend to explore them.

![rmlint has many options](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/18-min-800x411.jpg)

rmlint has many options

However, using this application is quite simple, you can run it by specifying the directory you want to check for duplicated files. For example:

```
rmlint /home/alu

```

![Using rmlint on the home folder](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/20-min-800x467.jpg)

Using rmlint on the home folder

This program will list everything it finds and creates a shell script to remove this lint. The script can be found in the home folder. Open it using a text editor, scroll down and check what files it will remove.

![rmlint generates a script file](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/19-min-800x359.jpg)

rmlint generates a script file

You can remove some of these files manually, or if you agree with suggested remove action you can go back to the terminal and execute this script. Again, make sure you [have a backup of all files](http://averagelinuxuser.com/backup-and-restore-your-linux-system-with-rsync/) before you run this script. This action will be irreversible.

```
sh -c rmlint.sh

```

![Removing duplicates file using rmlint](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/22-min-800x467.jpg)

Removing duplicates file using rmlint

Now, your system is cleaner. But it is not the end, there are still a few things you can do to clean it even further.

## 6\. Find the largest files and directories

You can check what the largest files in your system are and maybe you do not need them. To accomplish this task, you can use some command line tools or graphical programs. For **the command line tool**, I use `ncdu`.

To install it, run this command:

```
sudo pacman -S ncdu

```

Search for the largest directories and then go inside those directories and find the largest files and remove them if you do not need them.

![Using ncdu to find the largest folder on the system](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/24-min-800x467.jpg)

Using ncdu to find the largest folder on the system

If you prefer **a graphical program** you can use `filelight` **for Plasma 5**. It shows a graphical summary for all hard-drives and you can go inside and check the directories, then go inside the largest directories and so on until.

![Using filelight](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/25-min-800x467.jpg)

Using filelight

If you are using **Gnome**, you ca install `baobab`. There are some other tools listed in [Arch Wiki](https://wiki.archlinux.org/index.php/List_of_applications/Utilities#Disk_usage_display). Pick whatever you like.

![Others disk usage display tools](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/26-min-800x298.jpg)

Others disk usage display tools

## 7\. Disk cleaning programs

There are also some disk cleaning programs that can do many of the tasked listed above automatically. Nevertheless, since you use Arch Linux, I do not recommend using these programs. It is not always obvious what exactly will be done and you do not have full control of your system. Besides, you can very easily delete some configuration files you did not want to delete.

But I still would like to share with you this option as some user may still prefer all-in-one package for system cleaning.

![Disk cleaning tools available on Arch Linux](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/27-min-800x204.jpg)

Disk cleaning tools available on Arch Linux

Among all automatic cleaning programs in Arch Linux, *Bleachbit* is probably the most popular. It has a nice graphical interface and it can do most of the things I have shown above. For example, you can clean your system cache. Just select it, and click on the clean button.

![How to clean Arch Linux using Bleachbit](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/28-min-800x573.jpg)

How to clean Arch Linux using Bleachbit

In the end, you will see something like this.

![Cleaning the cache using Bleachbit](https://averagelinuxuser.com/assets/images/posts/2019-02-14-clean-arch-linux/29-min-800x467.jpg)

Cleaning the cache using Bleachbit

Which means your system cache has been cleaned.

Check out the other options of Bleachbit. I believe most of them are self-explanatory.

## Update

Thanks to the comments on [YouTube](https://www.youtube.com/AverageLinuxUser?sub_confirmation=1) and below this post, I can improve this post by extending this list. Below, you will find a few more things you can do to clean your Arch Linux system.

### 8\. Clean Systemd journal

Systemd stores its logs in `/var/log/journal/` and these logs can be very useful as I described in my post on [10 Things to do first after installing Arch Linux](https://averagelinuxuser.com/10-things-to-do-first-in-arch-linux). However, these log files can take up to 10% of your system size by default. There are two solution to limit this size.

1.  You can clean these log files manually when you run out of space. You can keep only the latest logs by size limit (e.g. keep only 50Mb of the latest logs):

```
sudo journalctl --vacuum-size=50M

```

Or by time limit (e.g. last 4 weeks):

```
sudo journalctl --vacuum-time=4weeks

```

1.  You can also set such limit as permanent and never worry about cleaning the logs. Just edit the file `/etc/systemd/journald.conf` by uncommenting `SystemMaxUse=` and setting the size limit:

```
SystemMaxUse=50M

```

This is what I choose to do and that is why I missed this point when I originally wrote this article. I simply never experienced large journalctl files.

I would like to acknowledge **Sebastian** for [pointing this out in the comments section](https://averagelinuxuser.com/clean-arch-linux/#jc6b5f4424-c30a-4f1a-9881-084224ce2249).

## CONCLUSION

Now that you know how to clean Arch Linux, so there are no excuses not to do it on your system :-) Remember that lack of free space may slow down your system, so in some sense, these things help to maintain a stable and fluid system.

However, I cannot know everything. If there is something you would add, please comment below.
