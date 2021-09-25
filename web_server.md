# Web Server

## Start webserver on localhost

If project is in node, usually start like this:

```shell
npm run
```

If not using a framework, the easiest way is 
the following command: 

```shell
python -m http.server 8888 
```
I have it aliased to `webserver`

## Connecting to the outside

There are different ways to do this. I'll list the 2 that I like. 

### using `ngrok`

```shell
ngrok http 4040
```

### localtunnel

You can use `npx` if you don't want to actually install localtunnel.









```shell
npx localtunnel --port 4040 
```

or install localtunnel like this:

```shell
npm install -g localtunnel 
```

Now you can use it like this:

```shell
lt --port 4040 
```

