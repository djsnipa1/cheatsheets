---
title: replit Node.JS 24/7 Project Hoster
created: 2022-05-15 21:33
modification date: 2022-05-15 21:33
tags: 
---
# replit Node.JS 24/7 Project Hoster

## Applying
Open your main repl file (example: index.js, app.js, main.js etc...) and at the top and the end of the code, paste this simple code inside:

Top of the code:
```js
const keepAlive = require(`./server`);
```

End of the code:
```js
keepAlive();
```

After that, create a new file named `server.js` and copy paste this code inside the file:

```js
const express = require('express');
const server = express();

server.all(`/`, (req, res) => {
    res.send(`Please connect me to a hosting website in-order to work 24/7.`);
});

function keepAlive() {
    server.listen(3000, () => {
        console.log(`Creator: ItzNexus`);
    });
}

module.exports = keepAlive;
```

Finally, connect the web address given at top right corner to a hosting website. I use [freshping](https://app.freshping.io) the most.

source: [NotNexuss/NodeJS-Project-Hoster: Host your repl.it project 24/7 with this code!, compatible with Node.JS.](https://github.com/NotNexuss/NodeJS-Project-Hoster)

*This code is only compatible for node.js. For python, [click me](https://github.com/ItzSidhan/Python-Project-Hoster)!*

