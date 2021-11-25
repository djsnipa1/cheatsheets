# Replacing Postlight’s Mercury scraping service with your self-hosted copy

![Replacing Postlight’s Mercury scraping service with your self-hosted copy](https://live.staticflickr.com/205/512285332_7a85b8fded_o.jpg)

[Mercury](https://mercury.postlight.com) by [Postlight](https://postlight.com) is a tool for scraping web pages. It “transforms web pages into clean text. Publishers and programmers use it to make the web make sense, and readers use it to read any web article comfortably.”

This was a fast, free web-based service, accessible via an API which worked rather beautifully, without a fuss.

Then, in February 2019, Postlight announced they were discontinuing the hosted service and open-sourcing [the code](https://github.com/postlight/mercury-parser). A mixed blessing, as, to keep using the service, this now required users of the service to set up their own version of Mercury, on their own, or Amazon’s servers.

[Some guidance](https://gitter.im/postlight/mercury) was provided, but few of those posting in the discussion group were (easily?) able to resolve the issues surrounding setting up their own instance. For me, Mercury using technology I’m not very familiar with, this was a bit of a hit-and-miss process that, eventually, did pay off.

Stephen Bradley wrote up [a guide on how to get Mercury running on an Amazon server](https://www.evernote.com/l/AAPoJR49OThHu5lBZLt8b1fyKomly8gRz6Q), but I like to stay clear from Amazon.

Here’s what I did to get Mercury running on my own server. Your mileage may vary.

01. I’m using[DreamHost](https://dreamhost.com/). When setting up a (sub-)domain, I can select the option ‘Passenger’, which is for running Ruby, NodeJS and Python apps.
02. SSH to the new domain and install NVM as described[here](https://github.com/creationix/nvm/blob/master/README.md).  Specifically:

    `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash`
03. After running that script, a message claims that you only have to close and open the terminal to have nvm running. That did not work for me and I had to run this (in the terminal):

    `export NVM_DIR="$HOME/.nvm"<br/>
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm<br/>
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion`
04. Update nvm to the minimum required version, in the terminal (based on[this post](https://davidwalsh.name/nvm)):

    `nvm install 8.10`
05. This did not result in the installed version of node sticking between sessions. I had to edit my bash profile and add a line to it.

    To edit my bash profile:

    `nano ~/.bash_profile`

    Adding the following line:

    `source ~/.bashrc`
06. Install the mercury parser in the terminal (based on[this](https://github.com/postlight/mercury-parser)):

    `npm install @postlight/mercury-parser`
07. Create a javascript file, for example with `myfile.js`:

    `const Mercury = require('@postlight/mercury-parser');<br/>
    const url = 'https://en.wikipedia.org/wiki/John_von_Neumann';<br/>
    Mercury.parse(url).then(result => { console.log(result); } );`
08. Execute the file from the command line with:

    `node myfile.js`

    But, this does not make the result available through the web.
09. Install expressjs as detailed[here](https://expressjs.com/en/starter/installing.html).
10. Create /myapp/app.js with this:

    `const express = require('express') ;<br/>
    const app = express() ;<br/>
    const port = 8888  ;<br/>
    app.get('/myapp/', function (req, res) {<br/>
    const Mercury = require('@postlight/mercury-parser');<br/>
    const url = req.query.url;<br/>
    Mercury.parse(url).then(result => {  res.send(result);  } );  })<br/>
    app.listen(port)`
11. Run the app from the command line:

    `node app.js`
12. Visit the page in the browser:

    `http://mysite.com:8888/myapp/?url=https://en.wikipedia.org/wiki/John_von_Neumann`
13. But, you want this app to run forever.[Install forever](https://riptutorial.com/node-js/example/21462/process-mangement-with-forever):

    `npm install forever -g`
14. Start forever:

    `forever start app.js`

Now, I can replace this:

`$postlightUrl = "https://mercury.postlight.com/parser?url=".$url;`

With this:

`$postlightUrl = "https://mysite.com:8888/myapp/?url=".$url;`

**Somewhat broken**

This worked, but, a few weeks later, it no longer did. The version of node, nvm, did not persist between sessions. This was resolved by adding what is now step 5, above.

I also threw together a quick PHP-based solution that essentially does the same as the Mercury parser: extracting basic details from a webpage.
