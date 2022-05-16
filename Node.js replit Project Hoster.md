---
title: replit Node.JS 24/7 Project Hoster
created: 2022-05-15 21:33
modification date: 2022-05-15 21:33
tags: 
---
# replit Node.JS 24/7 Project Hoster

source: [NotNexuss/NodeJS-Project-Hoster: Host your repl.it project 24/7 with this code!, compatible with Node.JS.](https://github.com/NotNexuss/NodeJS-Project-Hoster)

### This code is only compatible for node.js. For python, [click me](https://github.com/ItzSidhan/Python-Project-Hoster)!
<br>

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

<br>
</br>
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

<br>
</br>

Finally, connect the web address given at top right corner to a hosting website. I use [freshping](https://app.freshping.io) the most.

<br>
</br>

### Contact me: 

[<img align="left" alt="ItzSidhan | YouTube" width="22px" src="https://cdn4.iconfinder.com/data/icons/logos-and-brands/512/395_Youtube_logo-128.png" />](https://bit.ly/ItzSidhanYT)
<a href="https://dsc.gg/itzsidhan">
  <img align="left" alt="Discord" width="23px" src="https://raw.githubusercontent.com/peterthehan/peterthehan/master/assets/discord.svg" />
</a>
<a href="https://twitter.com/ItzSidhan">
  <img align="left" alt="Twitter" width="23px" src="https://raw.githubusercontent.com/peterthehan/peterthehan/master/assets/twitter.svg" />
</a>

</br>

### Languages and Tools: 

[<img align="left" alt="JavaScript" width="26px" src="https://cdn4.iconfinder.com/data/icons/logos-and-brands/512/187_Js_logo_logos-128.png" />](https://www.javascript.com/)
[<img align="left" alt="Node.js" width="26px" src="https://cdn4.iconfinder.com/data/icons/logos-and-brands/512/233_Node_Js_logo-128.png" />](https://nodejs.org/en/)
[<img align="left" alt="GitHub" width="26px" src="https://cdn4.iconfinder.com/data/icons/socialcones/508/Github-128.png" />](https://github.com/)
[<img align="left" alt="Visual Studio Code" width="26px" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/visual-studio-code/visual-studio-code.png" />](https://code.visualstudio.com/)
<br />
<br />
