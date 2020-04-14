# Writeguard

## Other Email Issue

![ss1](https://i.imgur.com/4ovsuHX.png)

![ss2](https://i.imgur.com/Szt3tYf.png)

![ss3](https://i.imgur.com/noOlzzu.png)

## Email blocking by Barracuda

> ## Request Received
> 
> Thank you for submitting your request. If this is your first request,
>  your IP address will have its reputation increased to "normal" for 48 
> hours while we investigate. It may take up to 1 hour for the reputation 
> increase to propagate to all Barracuda Spam Firewalls globally. We 
> appreciate your patience and apologize for any inconvenience.
> 
> **Your confirmation number is BBR21586894740-10107-515.**
> 
> One way to avoid having your email inadvertently blocked is by registering your domain and IP addresses at [EmailReg.org](http://www.emailreg.org/). Emails from domain names and IP addresses that are properly registered on [EmailReg.org](http://www.emailreg.org/) can be automatically exempted from spam filtering defense layers on Barracuda Spam Firewalls and other anti-spam solutions, preventing your email from 
> being accidentally blocked.
> 
> http://www.emailreg.org/index.cgi?p=register

![screenshot](https://i.imgur.com/L4FnLF9.png)

## Issues as of 4/1/2020

## **Krista said:**

> SQL Syntax

## **Customer said:**

> Add to cart

> 1064 You have an error in your SQL Syntax check

> **Manual Deposit Ticket DT15-C**

- - -

## Mediatemple Info

### Permissions

Rule of thumb for correct permissions:

* Folders: 755
* Static Content: 644
* Dynamic Content: 700

**TIP:**

> Linux permissions can be represented with numbers, letters, or words. They also include an entry for Owner, Group, and Everyone.

| code    | `ls`         |
| ------- | ------------ |
| **755** | `drwxr-xr-x` |
| **644** | `-rw-r--r--` |
| **700** | `-rwx------` |

* **755** stands for Owner: read, write, execute; Group: read, execute; Everyone: read, execute
* **644** stands for Owner: read, write; Group: read, Everyone: read
* **700** stands for Owner: read, write, execute; Group: (none); Everyone: (none)

### Ownership

In Linux file structures, every file and folder is assigned to an Owner and a Group. The correct owner and group for your server are as follows, listed like this:

* **Plesk server** - note that domainuser is the FTP user for that domain, and example.com is the specific domain in question:
  * /var/www/vhosts/example.com/  - __root:root__
  * /var/www/vhosts/example.com/httpdocs/ - __domainuser:psaserv__
  * /var/www/vhosts/example.com/httpdocs/index.html - __domainuser:psacln__

## Changing website permissions

Got info from [here](https://www.reddit.com/r/cs50/comments/5055ti/403_forbidden_permissions_chmod_the_definitive/)

_This might have to be done like this:_

```bash
find . -name *.php -exec chmod 640 {} \;
```

_because the `xargs` pipe didn't work correctly for me..._

This command finds all php files and lists their permissions in the `ls -l` display

```bash
find . -name *.php | xargs ls -l
```

Changes all directories to 711 `drwx--x--x`

```bash
find . -type d | xargs chmod 711
```

Changes all php files to their correct permissions

```bash
find . -name *.php | xargs chmod 640
```

Change html, css, js, and images to the following

```bash
find . -name *.html | xargs chmod 644
```

__REFERENCE:__

```bash
cd ~/workspace/pset7
find . -type d | xargs chmod 711
find . -name *.php | xargs chmod 640
find . -name *.json | xargs chmod 640
find . -name *.html | xargs chmod 644
find . -name *.css | xargs chmod 644
find . -name *.png | xargs chmod 644
find . -name *.js | xargs chmod 644
chmod 644 ./public/fonts/*
```

- - -

## I think this is what fixed the problem when we switched to DV server

[Solving 403 Forbidden on Port 443 (HTTPS) for Apache 2.4](https://medium.com/@xvista/solving-403-forbidden-on-port-443-https-for-apache-2-4-40bab9296315)
