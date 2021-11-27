# [Adding a swapfile after a clean installation without swap partition](https://arcolinuxforum.com/viewtopic.php?p=5712&sid=9c311c4bdea37b9fc69b13ae3d64a9c2#p5712)

One of the advantages is that you can make the swapfile on the spot and delete it again. Make it bigger or make it smaller.

You can do the same with partitions via gparted but it is a bit more technical.

How to set up a swapfile on ArcoLinux or Arch Linux? of 8G = 8 Gigabyte \- make bigger if needed

Code:

```
sudo fallocate -l 8G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

Now reboot and check with

Code:

```
cat /proc/meminfo
cat /proc/swaps
swapon -s
```

[YouTube - Adding swapfile to ArcoLinux](https://www.youtube.com/embed/bE0-4Dt6lrM)
