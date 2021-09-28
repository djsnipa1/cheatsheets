# The curl guide to HTTP requests

## curl is an awesome tool that lets you create network requests from the command line

_Published Oct 06, 2018_

curl is a a command line tool that allows to transfer data across the network.

It supports lots of protocols out of the box, including HTTP, HTTPS, FTP, FTPS, SFTP, IMAP, SMTP, POP3, and many more.

When it comes to debugging network requests, curl is one of the best tools you can find.

It’s one of those tools that once you know how to use you always get back to. A programmer’s best friend.

It’s universal, it runs on Linux, Mac, Windows. Refer to the [official installation guide](https://curl.haxx.se/docs/install.html) to install it on your system.

Fun fact: the author and maintainer of curl, swedish, was awarded by the king of Sweden for the contributions that his work (curl and libcurl) did to the computing world.

Let’s dive into some of the commands and operations that you are most likely to want to perform when working with HTTP requests.

Those examples involve working with HTTP, the most popular protocol.

*   [Perform an HTTP GET request](#perform-an-http-get-request)
*   [Get the HTTP response headers](#get-the-http-response-headers)
*   [Only get the HTTP response headers](#only-get-the-http-response-headers)
*   [Perform an HTTP POST request](#perform-an-http-post-request)
*   [Perform an HTTP POST request sending JSON](#perform-an-http-post-request-sending-json)
*   [Perform an HTTP PUT request](#perform-an-http-put-request)
*   [Follow a redirect](#follow-a-redirect)
*   [Store the response to a file](#store-the-response-to-a-file)
*   [Using HTTP authentication](#using-http-authentication)
*   [Set a different User Agent](#set-a-different-user-agent)
*   [Inspecting all the details of the request and the response](#inspecting-all-the-details-of-the-request-and-the-response)
*   [Copying any browser network request to a curl command](#copying-any-browser-network-request-to-a-curl-command)

## Perform an HTTP GET request

When you perform a request, curl will return the body of the response:

```bash
curl https://flaviocopes.com/

```

## Get the HTTP response headers

By default the response headers are hidden in the output of curl. To show them, use the `i` option:

```bash
curl -i https://flaviocopes.com/

```

## Only get the HTTP response headers

Using the `I` option, you can get *only* the headers, and not the response body:

```bash
curl -I https://flaviocopes.com/

```

## Perform an HTTP POST request

The `X` option lets you change the HTTP method used. By default, GET is used, and it’s the same as writing

```bash
curl -X GET https://flaviocopes.com/

```

Using `-X POST` will perform a POST request.

You can perform a POST request passing data URL encoded:

```bash
curl -d "option=value&something=anothervalue" -X POST https://flaviocopes.com/

```

In this case, the `application/x-www-form-urlencoded` Content\-Type is sent.

## Perform an HTTP POST request sending JSON

Instead of posting data URL\-encoded, like in the example above, you might want to send JSON.

In this case you need to explicitly set the Content\-Type header, by using the `H` option:

```bash
curl -d '{"option": "value", "something": "anothervalue"}' -H "Content-Type: application/json" -X POST https://flaviocopes.com/

```

You can also send a JSON file from your disk:

```bash
curl -d "@my-file.json" -X POST https://flaviocopes.com/

```

## Perform an HTTP PUT request

The concept is the same as for POST requests, just change the HTTP method using `-X PUT`

## Follow a redirect

A redirect response like 301, which specifies the `Location` response header, can be automatically followed by specifying the `L` option:

```bash
curl http://flaviocopes.com/

```

will not follow automatically to the HTTPS version which I set up to redirect to, but this will:

```bash
curl -L http://flaviocopes.com/

```

## Store the response to a file

Using the `o` option you can tell curl to save the response to a file:

```bash
curl -o file.html https://flaviocopes.com/

```

You can also just save a file by its name on the server, using the `O` option:

```bash
curl -O https://flaviocopes.com/index.html

```

## Using HTTP authentication

If a resource requires Basic HTTP Authentication, you can use the `u` option to pass the user:password values:

```bash
curl -u user:pass https://flaviocopes.com/

```

## Set a different User Agent

The user agent tells the server which client is performing the request. By default curl sends the `curl/<version>` user agent, like: `curl/7.54.0`.

You can specify a different user agent using the `--user-agent` option:

```bash
curl --user-agent "my-user-agent" https://flaviocopes.com

```

## Inspecting all the details of the request and the response

Use the `--verbose` option to make curl output all the details of the request, and the response:

```bash
curl --verbose -I https://flaviocopes.com/

```

```text
*   Trying 178.128.202.129...
* TCP_NODELAY set
* Connected to flaviocopes.com (178.128.202.129) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate: flaviocopes.com
* Server certificate: Let's Encrypt Authority X3
* Server certificate: DST Root CA X3
> HEAD / HTTP/1.1
> Host: flaviocopes.com
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 200 OK
HTTP/1.1 200 OK
< Cache-Control: public, max-age=0, must-revalidate
Cache-Control: public, max-age=0, must-revalidate
< Content-Type: text/html; charset=UTF-8
Content-Type: text/html; charset=UTF-8
< Date: Mon, 30 Jul 2018 08:08:41 GMT
Date: Mon, 30 Jul 2018 08:08:41 GMT
...

```

## Copying any browser network request to a curl command

When inspecting any network request using the [Chrome Developer Tools](https://flaviocopes.com/browser-dev-tools/), you have the option to copy that request to a curl request:

![copy-as-curl-in-devtools](https://flaviocopes.com/http-curl/copy-as-curl-in-devtools.png)

```bash
curl 'https://github.com/curl/curl' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' \
-H 'Upgrade-Insecure-Requests: 1' -H 'DNT: 1' -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) | \
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36' -H 'Accept: \
text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8' -H 'Referer: https://www.google.it/' \
-H 'Accept-Encoding: gzip, deflate, br' -H 'Accept-Language: en-US,en;q=0.9,it;q=0.8' -H |
'Cookie: _octo=GH1.1.933116459.1507545550; _ga=GA1.2.643383860.1507545550; tz=Europe%2FRome; user_session=XXXXX; \
__Host-user_session_same_site=YYYYYY; dotcom_user=flaviocopes; logged_in=yes; has_recent_activity=1; _gh_sess=ZZZZZZ' \
--compressed
```

---

#### Sign up to one of my Premium Online Courses 📚

*   [JavaScript Course](https://thejscourse.com)
*   [React Course](https://thereactcourse.com)
*   [Node.js Course](https://thenodecourse.com)
*   [Web Platform Course](https://webplatformcourse.com)
*   [Vue.js Course](https://vuecourse.com)
*   [Svelte Course](https://club.flaviocopes.com/svelte)
*   [Next.js Course](https://nextjscourse.com)

[follow @flaviocopes](https://twitter.com/flaviocopes)

[CLI](https://flaviocopes.com/tags/cli/) [CSS](https://flaviocopes.com/tags/css/) [Database](https://flaviocopes.com/tags/database/) 
[DevTools](https://flaviocopes.com/tags/devtools/) [Express](https://flaviocopes.com/tags/express/)
[Git](https://flaviocopes.com/tags/git/) [Go](https://flaviocopes.com/tags/go/) [GraphQL](https://flaviocopes.com/tags/graphql/) 
[HTML](https://flaviocopes.com/tags/html/) [JavaScript](https://flaviocopes.com/tags/js/) [Lab](https://flaviocopes.com/tags/lab/) 
[Network](https://flaviocopes.com/tags/network/) [Next.js](https://flaviocopes.com/tags/next/) 
[Node.js](https://flaviocopes.com/tags/node/) [React](https://flaviocopes.com/tags/react/) 
[Services](https://flaviocopes.com/tags/services/) [Svelte](https://flaviocopes.com/tags/svelte/) 
[Vue.js](https://flaviocopes.com/tags/vue/) [Web Platform](https://flaviocopes.com/tags/browser/)

© 2019 Flavio Copes

🔥 Join one of my [**Premium Online Courses**](https://flaviocopes.com/courses/) 🔥
