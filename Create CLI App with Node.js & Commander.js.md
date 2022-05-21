---
title: Create CLI App with Node.js & Commander.js
created: 2022-01-19 18:46
modification date: "2022-01-19 18:46"
tags: node tutorial article
link: "https://javascript.plainenglish.io/how-to-create-a-command-line-npm-module-cli-using-commander-js-1073e616aee7"
modified: 2022-02-10 21:53
---
# [How to create your command-line program (CLI) with NodeJS and Commander.js | by Duc N. | JavaScript in Plain English](https://javascript.plainenglish.io/how-to-create-a-command-line-npm-module-cli-using-commander-js-1073e616aee7)
Create your own command line

This post will show you how to create a command-line npm module (CLI) using Commander.js module.

[Commander.js](https://github.com/tj/commander.js/) is a very popular module that lets you create your own CLI program.

First, start your new project — let’s say my project name is “json-now”

```
$ git clone https://github.com/yourname/json-now.git$ cd json-now
```

Now, create your package.json file:

```
{  "name": "json-now",  "version": "0.0.1",  "bin": {    "json-now": "./bin/index.js"  },  "dependencies": {    "commander": "^3.0.1"  }}
```

Then, install dependencies:

```
$ npm install
```

The “bin” section specifies your command line name. As you see, go ahead and create a “bin” directory with “index.js” file there:

```
#!/usr/bin/env nodeconst program = require('commander');const ver = require('../lib/ver');program  .usage('[options] <file>')  .option('-v, --version', 'show version', ver, '')  .option('-p, --port <port>', 'use custom port')  .option('-f, --flag', 'boolean flag', false)  .action((file, options) => {    console.log('file name: ', file);    // more hanlder: require('../lib/moreHandler')(options);  })  .parse(process.argv);
```

Let’s create the very first option called “-v” or “ — version” which shows version number. Create a directory named “lib” and a new file “ver.js” there:

```
const package = require('../package.json')module.exports = () => {    console.log(package.version);};
```

So far, it looks straight forward. You created a commander “program” which handles option like “-v” by running “ver.js”

Open Terminal and try it out:

```
$ node bin/index.js -v0.0.1$ node bin/index.js sample.jsonfile name: sample.json
```

Now, it’s time to publish your command line for the world to use!

```
$ npm login$ npm publishTry out your shiny new command:$ npm install json-now -g$ json-now -v
```

The above code is located here for your reference: [GitHub - ngduc/json-now: $ json-now - Launch an API Server to serve data from a JSON, JS file or faker data with HTTPS support. Based on json-server.](https://github.com/ngduc/json-now)