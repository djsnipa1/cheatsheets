# Installing Arch Linux

```shell
iwctl
```

```shell
device list
```
Remember name of the device. For example `wlan0`

```shell
station wlan0 scan
station wlan0 get-networks
station wlan0 connect MODEMRNA-VACCINE
```

Enter password and you're done!

```shell
exit

ip a
ping google.com
```

---

## Setting the clock

View clock by typing 'timedatectl'

To change the timezone:

```shell
timedatectl set-timezone America/Indianapolis
```

