# Downloading a Tarball from GitHub

## 1. Overview

GitHub allows us to fetch a repository in two ways:

1. Using `git clone`
2. Download as a `zip` or `tar`file

Although `git clone` is the most used method, it requires a Git installation on the machine. If Git is not available, we can [download the repository](https://docs.github.com/en/rest/reference/repos#download-a-repository-archive-tar) in tar format and unpack the contents on the file system.

**In this tutorial, we'll look at some Linux commands to download the GitHub repository tarball and unpack it on the file system**.

## 2. Using `curl` Command

We can access any HTTP URL by using the ` [curl](/curl-rest)` command. And since GitHub allows us to download the repository archive over HTTP, we can download this tarball using `curl:`

```bash
curl -L  https://github.com/Baeldung/kotlin-tutorials/tarball/master -o dummy.tgz
```

We used the `-L` flag to allow `curl` to follow redirects. This is necessary because GitHub redirects all download requests to an [archive location](https://raw.githubusercontent.com/Baeldung/kotlin-tutorials/tarball/master). **If we skip this flag, we'll get a 302 HTTP status code with redirect headers**.

The above command will download the `.tgz` file to the same location where the `curl` command was executed. Later, we can unpack this file by using the `[tar](/linux/tar-command)` command.

We can also unpack inline:

```bash
curl -L https://github.com/Baeldung/kotlin-tutorials/tarball/master | tar -xz
```

In most cases, `curl` can handshake the HTTPS connection with GitHub. **However, if this connection fails, we can use the insecure option in** `**curl**:`

```bash
curl -L -k https://github.com/Baeldung/kotlin-tutorials/tarball/master | tar -xz
```

## 3. Using `wget` Command

Apart from the `curl` command, which is a general-purpose command to execute HTTP requests, Linux also provides a ` [wget](/linux/curl-wget)` command which is a dedicated non-interactive network downloader.

**It supports HTTP and FTP protocols and thus can also be used to download repository archives from GitHub**:

```bash
wget https://github.com/Baeldung/kotlin-tutorials/tarball/master -O dummy.tgz
```

Likewise, the above command will download the `.tgz` file to the same location where the command is executed.

Similar to the `curl`command, we can unpack the archive file inline:

```bash
wget https://github.com/Baeldung/kotlin-tutorials/tarball/master -O - | tar -xz
```

The command `-O` option redirects the archive content to the standard output and acts as an input to the `tar` command.

**Again, similar to the `curl` command, we can skip the HTTPS certificate verification in** `**wget using**` **–no-check-certificate** `:`

```bash
wget --no-check-certificate https://github.com/Baeldung/kotlin-tutorials/tarball/master -O - | tar -xz
```

## 4. Downloading From Private Repositories

The commands we have discussed so far are useful for downloading archives from a public repo. **However, in the case of a private repository, we need to provide GitHub access tokens**:

```bash
curl -L -k -u token:x-oauth-basic https://github.com/Baeldung/kotlin-tutorials/tarball/master | tar -xz
```

Here, the token is an alphanumeric OAuth token which we need to add to the GitHub account.