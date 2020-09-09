# How to use Git.io to shorten GitHub URLs and create vanity URLs 

[How to use Git.io to shorten GitHub URLs and create vanity URLs – 049 – Sara Ford's Blog](https://saraford.net/2017/02/18/how-to-use-git-io-to-shorten-github-urls-and-create-vanity-urls-049/)

Suppose you want to shorten the URL to a particular location on GitHub. Or perhaps you want to create a vanity URL that goes directly to your GitHub profile, e.g. [https://git.io/saraford](https://git.io/saraford). You can use [Git.io: GitHub URL Shortener](https://github.com/blog/985-git-io-github-url-shortener).

**To shorten a URL,** open your favorite command prompt (via Git Shell) and type in

```shell
 curl -i https://git.io -F "url=https://github.com/saraford/your-moment-of-github-zen/issues"
```

in the response, you’ll see your shorten URL!

```shell
Location: https://git.io/vMdeF
```

**To create a vanity URL** for your GitHub profile,

```shell
curl -i https://git.io -F "url=https://github.com/saraford" -F "code=saraford"
```

in the response, you’ll see a new way to refer to your GitHub profile!

```shell
Location: https://git.io/saraford
```

