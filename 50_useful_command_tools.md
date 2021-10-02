# Most Useful Command Line Tools: 50 Cool Tools to Improve Your Workflow, Boost Productivity, and More

__ Alexandra Altvater__ May 10, 2017[__ Developer Tips, Tricks & Resources][0]

Developers and those with engineering responsibilities are fond of calling terminal their home. Anyone with a Unix system has to frequently interact with the Terminal in one way or the other. And customization has always been a big part of how much the Terminal can be used to improve productivity, create unique experiences, and manage the system to improve the workflow. At Stackify, we're always up for quirky and innovative tools that help us become more productive developers. So no matter how you prefer to work, taking frequent breaks, relying on a lengthy task list, GTD methodology, with your favorite music playing in the background, you can make all of that and more happen from right within the Terminal with command line tools.

Command line tools are scripts, programs, and libraries that have been created with a unique purpose, typically to solve a problem that the creator of that particular tool had himself. Because of that, we have divided this roundup of the best command line tools to include different categories, like Web Development, Utilities, Productivity, and others. Beyond being categorized, note that the following 50 command line tools are listed in no particular order --- they're not ranked or rated, but are numbered simply to make a list easier to navigate.

These are all open-source projects, so everything is free to download, and you can become a contributor to any of the projects through GitHub, where most of these tools have been hosted. To check out command line tools in a particular category, click on a link below:

* [Web Development][1]
* [Productivity][2]
* [Utility][3]
* [Visual][4]
* [Entertainment][5]

## Web Development

## 1\. [is-up-cli][6]

[@**sindresorhus**][7]

[Sindre Sorhus][8] has done some great projects in the open-source community; the "is-up" is a small library that taps into the "isitup.org" API to deliver a seamless website status checking service from your terminal.

**Key Features:**

* Simple one-command way of checking whether a website is up or down.
* Has a separate library that shows how to tap into the API.

## **2\. [pageres-cli][9]**

[@**sindresorhus**][7]

As a developer, you will often find yourself needing to take website snapshots to present to your clients or work colleagues. The pageres-cli is capable of capturing up to 100 snapshots from 10 unique websites in less than 60 seconds, dramatically cutting down on the time and hassle of taking dozens of screenshots individually.

**Key Features:**

* You can specify the website address and include a particular resolution to capture.
* Capture multiple resolutions from multiple websites at the same time.

## **3\. [viewport-list-cli][10]**

[Kevin Mårtensson][11] is another brilliant coder for the Open Source community, and this time we're featuring one of his lesser-known libraries, albeit still useful, which can quickly return a viewport ratio for any device that you're building an interface for. If you have your style guide workflow, this might not be as helpful, but still, it's quite easy to use and could come in handy when you're doing some quick fixes on the go.

**Key Features:**

* Can fetch device sizes for single or multiple items.
* Results can be exported into a file.
* Results can also be formatted into a table.

## **4\. [Surge][12]**

[@**surge\_sh**][13]

Developers love the idea of static websites, more than they love the idea of having to host their WordPress website. Surge caters to front-end developers who need a quick method for publishing their HTML, CSS, and JavaScript content on the web. It takes a few seconds to type in the command and viola; your pages are up and running!

**Key Features:**

* Free and Premium models.
* Custom domain name for your site.
* Publish a whole folder with one command.

## **5\. [loadtest][14]**

[@**pinchito**][15]

The loadtest library is a fully capable project for load testing a website. With an extendable API, you can integrate loadtest into your tests environment. The number one reason for developers using loadtest is that it allows for custom configuration options that replicate a real-world scenario.

**Key Features:**

* Custom parameters for requests and concurrent clients.
* You can specify custom Cookie and Header values.
* Includes advanced features for in-depth server testing.

## **6\. [WP-CLI][16]**

[@**wpcli**][17]

WordPress is the world's most popular blogging software, though not everyone wants to use the WordPress dashboard to manage their site, especially not developers who have grown to love their terminal! The WP-CLI is a sophisticated command line solution for managing your WordPress website, including themes and plugins.

**Key Features:**

* Well-documented and full of sample usage cases.
* Commands that can manage cache, user's, core, posts, etc,.
* Built by WordPress developers and the WordPress community.

## **7\. [diff2html-cli][18]**

[@**rtfpessoa**][19]

Diff to Html generates pretty HTML diffs from unified and git diff output in your terminal. Diff2HTML supports GitLab, GitHub, Bitbucket, and merge/pull requests. The main reason developers use this over any other library is that diff2html provides a clear overview of the changes.

**Key Features:**

* Highlights code syntax.
* Matches similar lines together for readability.
* Based on GitHub style-guide for a pleasant UI.

## **8\. [npm-home][20]**

[@**sindresorhus**][7]

This one is for Node.js devs! Save yourself a little bit of time by loading up the NPM page of a particular package directly from the terminal. Whether you're browsing the web with terminal and found a package you want to check or an old-memory strikes back, npm-home is handy to have.

**Key Features:**

* Simple one-line command to open the web page of an NPM project.

## **9\. [caniuse-cmd][21]**

[@**caniuse**][22]

When you're working on something special, the last thing you want is to be distracted from your workflow. But being a web developer means that you constantly have to check for errors and mistakes, especially when talking about function usage across different browsers. This neat little library is based on the CanIUse.com website.

**Key Features:**

* Checks for feature availability across all modern web browsers.
* Gives specific output as to how functional the feature is across those browsers.

## **10\. [npm-name-cli][23]**

[@**sindresorhus**][7]

Another one for you busy Node.js developers, this tool is useful for checking whether a particular package name has been taken on the NPM website. This lets you quickly push out project names that you know won't interfere or be confusing for other members of the community.

**Key Features:**

* Is more performance-oriented, and has a nice results output than the inbuilt search feature of npm's own CLI.

## **11\. [strip-css-comments-cli][24]**

[@**sindresorhus**][7]

Every byte matters, especially when you have to improve performance. If your app is finished and ready for production, use this efficient library to quickly strip away any comments on your CSS files.

**Key Features:**

* You can opt to preserve certain comments by regex input; likewise, you can specify not to preserve any comments.
* Works based on input-file and output-file, so the original file is never entirely destroyed.

## **12\. [HTTPie][25]**

[@**clihttp**][26]

HTTPie is like Internet Explorer; only it doesn't have a UI. Instead, it works directly from the terminal. the isn't just another weekend project either. HTTPie has 30,000 stars on GitHub, and among the features, you will find JSON support, code highlighting, plugins, an intuitive User Interface, a custom interface for downloads, and much more.

**Key Features:**

* Massive documentation explaining how you can turn HTTPie in your primary web browsing choice.
* Supports many custom settings for most frequently used HTTP input variations: headers, cookies, authentication, etc,.
* Works with Windows, Linux, and MacOS platforms.

## **13\. [icdiff][27]**

The terminal can process a lot of information, but not all of the tools tap into that power. The icdiff library can show you the small tweaks and differences between two files of similar nature. It highlights the values that have been changed, added, and shows what has been removed from the second file.

**Key Features:**

* Extensive option capabilities for creating custom output layouts.
* You can target specific lines of the files that include the code you want to compare, such as the header alone.

## **14\. [Pandoc][28]**

Getting your files to work across multiple devices is essential. With the personalized preferences for systems that developers use, you never know when you might need to convert your TXT documentation into an HTML presentation.

**Key Features:**

* Easily converts HTML files into slideshows.
* Convert web pages into markdown files.
* Custom code syntax highlighting.

## **15\. [Babun][29]**

[@**babunshell**][30]

As per the reviews of the users themselves, Babun is a Linux shell that Windows users are going to enjoy using. If you thought Cygwin was great, then you will adore the extended functionality of Babun.

**Key Features:**

* Custom package manager called "pact."
* Built with a plugin back-end for customization.
* Custom shell built for user experience.

## **Productivity**

## **16\. [Moro][31]**

[@**omidfi**][32]

Keeping track of yourself is a good way to prioritize your workflow and improve your productivity based on the amount of work you get done in a specific time frame. While Moro is a simple tool, it can turn out to be useful to understand your work performance.

**Key Features:**

* You can set custom notes each time you run the 'moro' command, allowing you to track the amount of time it takes to get a particular project done.
* Moro tracks all your data for detailed reports.

## **17\. [Terjira][33]**

JIRA is without a doubt one of the world's leading platform for issue and bug tracking, and with Terjira you can bring the JIRA functionality straight into your terminal. This is an ultra-optimized library that gives you a simple JIRA interface from your terminal shell.

**Key Features:**

* You can sort, edit, create and delete issues.
* Custom commands for boards, sprints, and projects.

## **18\. [Timetrap][34]**

[@**\_SamG**][35]

Timetrap is a time tracking tool with a slightly more complex capabilities, perfect for freelance developers and designers who are constantly relying on their performance to manage projects. The best way to improve yourself is to learn how to manage yourself, and time tracking is a good place to start.

**Key Features:**

* You can switch between custom entries whenever you change your work routine.
* All records can be output in a concise table of data, showing precise details of how much time you've spent on each task.

## **19\. [Taskwarrior][36]**

[@**taskwarrior**][37]

Taskwarrior is an open-source library that integrates a fully functional TODO list management application into your terminal. It's clean, with excellent performance and more than 350+ custom plugin extensions created by other developers. Taskwarrior scales to fit your workflow. Use it as a simple app that captures tasks, shows you the list, and removes tasks from that list.

**Key Features:**

* Tasks can be added with one line of command, including product description and the due date.
* Taskwarrior supports Pomodoro and GTD so you can create even more depth for your productivity workflow.
* Has a large community that's open to helping and suggestions on ways to use this library for the best results.

## **20\. [geeknote][38]**

[@**VitaliyRodnenko**][39]

Taking notes is an essential aspect of being a developer, an engineer, or even a designer. While Linux systems have the capacity to provide locally hosted note management platforms, nowadays it's quite popular to use a platform such as Evernote to capture notes and have them readily available across multiple devices. Geeknote gives you a stellar UI for using Evernote within your terminal.

**Key Features:**

* Geeknote lets you create new notes, tags, and notebooks from the shell.
* Edit your existing notes using your favorite editor: vim, emacs, nano, etc.
* Custom sync options for local/external files.

## **21\. [imgur-uploader-cli][40]**

Imgur is one of the world's most popular image sharing platforms, with millions of daily active users, and a performance optimized image sharing interface that can deal with any demand. Most of all it is simple to use, and efficient in getting your images seen by anyone quickly.

**Key Features:**

* Lets you upload images to Imgur without you having to leave your terminal interface.
* You can specify your image titles.

## **22\. [doing][41]**

[@**ttscoff**][42]

Doing is a basic CLI for adding and listing "what was I doing" reminders in a TaskPaper-formatted text file. It allows for multiple sections/categories and flexible output formatting. Never again will you question yourself and the actions that you performed during any given day.

**Key Features:**

* Extensive management of each task, their timelines, and the amount of time they've taken up during their lifetime.

## **23\. [Uber-cli][43]**

Uber CLI is obviously a bit of a jab at productivity geeks, but that hasn't stopped thousands of developers from switching their Uber access workflow permanently. With Uber CLI you can quickly get a price and time to destination estimates with a simple command.

**Key Features:**

* You can input a starting address and ending address.
* The output is a neatly organized table that shows prices for different Uber car variations.

## **24\. [jq][44]**

JQ is an easy to use and a lightweight processor for JSON files. JQ primarily acts as a filter that can take your input, and then produce a settings-based output. Filters can be combined in various ways -- you can pipe the output of one filter into another filter, or collect the output of a filter into an array.

**Key Features:**

* Supports basic and advanced requirements.
* Can be optimized with mathematical equations.

## **25\. [autojump][45]**

[@**\_wting**][46]

This neat library creates a more streamlined workflow for the directories that you access on a consistent basis. It can save into its memory the folders that you visit the most, and give you a more flexible way of navigating to them with simple commands. Being productive is all about methods for minimizing your need to exit the terminal for any reason at all.

**Key Features:**

* Works across Linux, Windows, and MacOS.

## **26\. [ranger][47]**

Ranger is a dynamic User Interface for complete system file management needs. It supports VI binds for easier access across the whole of your system. The interface is focused on a minimal design, emphasizing the structure of each directory. Additionally, you can customize Ranger with external plugins, or build your own.

**Key Features:**

* Supports file management operations.
* File and directory previews.
* Filetype detection and automated execution.

## Utility

## **27\. [battery-level][48]**

[@**hynden**][49]

This is a rather straightforward utility tool for those of you who live in the complete absence of a GUI on your system. Just type in the battery-level command, and it will give you a clear percentage indication of how much juice is left in your system.

**Key Features:**

* Great for minimalism enthusiasts.

## **28\. [brightness-cli][50]**

Love to code at night, but don't love the bright screen? Sure, there are tons of ways to adjust brightness on your system, and some laptops have integrated buttons that do it. But if you're feeling like geeking out a bit -- why not adjust the percentage with a simple command line syntax?

**Key Features:**

* Enables you to change the value of screen brightness from within your terminal.

## **29\. [GoTTY][51]**

[@**i\_yudai**][52]

GoTTY can transform your terminal into a web application. If you are running some extensive tools from the terminal and want to have access to them on the go, simply run a GoTTY instance and have a web address available to monitor the process.

**Key Features:**

* You can specify custom web address and port numbers.
* You can enable clients to write commands.
* Enable user credentials for authentication protection.
* You can specify custom certifications for additional security layer.

## **30\. [web-search-cli][53]**

[@**zquestz**][54]

If terminal is your home, why not add an additional layer of web search capabilities. The Web-Search-CLI library is ideal for searching the web based on custom inputs. Apart from Google, there are ~100 other supported providers, such as: Imgur, GitHub, Wikipedia, and many other developer-friendly websites.

**Key Features:**

* Providers are keyword-based so that you can type 's $provider $term'.
* You can add your custom providers.
* Server mode for enabling a web interface.

## **31\. [aria2][55]**

[@**tatsuhiro\_t**][56]

Aria2 is a flexible download utility software with multi-protocol and multi-source support. It's capable of understanding protocols like BitTorrent, FTP, HTTP(S), SFTP, and others. There are also ways to transform Aria2 into a web-based UI using an external plugin.

**Key Features:**

* All file management can be done from the command line.
* Downloads can be queued up in segments.
* Custom Header and Proxy support.

## **32\. [remote-share-cli][57]**

[@**marionebl**][58]

Remote Share CLI was created to enable developers and Unix system users such as yourself to quickly share important files with the world, presumably your co-workers or friends you're collaborating on a project with. The first version of this tool could only share files locally; however, with the CLI version, you can share with anyone.

**Key Features:**

* One-step file upload to the web.
* Automated activity monitoring that closes the app based on inactivity and/or download signals.

## **33\. [hub][59]**

[@**github**][60]

Hub is your friendly git wrapper that boosts your GitHub experience, whether you are a contributor or someone who maintains their own project. Hub makes the GitHub code-sharing experience much more enjoyable and straightforward, letting you focus on things that are important; like writing more code!

**Key Features:**

* Hub strives to create a more pleasant user experience for standard GitHub commands.
* Integrated support for GitHub Enterprise.

## **34\. [tmux][61]**

The tmux tool is what's known as a terminal multiplexer. This program allows developers to run multiple terminals at once, but manage them all from one terminal instance. It's commonly known as a solid alternative to the popular GNU Screen. Tmux runs on most Unix systems.

**Key Features:**

* Extensive key bindings for a smooth experience.
* Custom options and appearance for each terminal.
* Well-organized documentation that shows how to make tmux a part of your permanent productivity workflow.

## **35\. [Metadelta-cli][62]**

[@**metadeltamath**][63]

Metadelta CLI is an effective way to solve your math problems in the terminal, without the need to load up your Python or seek an external website. Metadelta can do derivative math simply and quickly.

**Key Features:**

* Supports arithmetic, as well as symbolic math problem inputs.

## Visual

## **36\. [gifgen][64]**

[@**lukechilds123**][65]

It's not uncommon knowledge that FFMPEG encoded GIFs come out a little choppy, largely because FFMPEG uses a limited color palette which doesn't have the capacity to cover the full range of colors. GifGen differs in that it does multiple encodes for the GIF. It analyzes colors for pixels individually, and then uses that palette to encode the actual GIF.

**Key Features:**

* Custom color palette based on the colors within the visual file.
* You can specify the framerate for the final GIF.
* Works for Linux and MacOS.

## **37\. [Gifsicle][66]**

[@**xexd**][67]

Gifsicle is a universal CMD tool for all your GIF management needs. Gifsicle can create, edit, and organize information about your GIF files. Gifsicle can combine multiple animations into a single GIF, it can customize single frames, and do lots of color customization for individual aspects of a GIF.

**Key Features:**

* Extensive color management options.
* Custom color maps depending on a situation.
* Animation optimization for performance.

## **38\. [ttygif][68]**

[@**icholy**][69]

If you're a developer who actively develops programs for the Open Source community, then chances are you will eventually want to provide your README files with animated explanations of how your programs work in the terminal or outside of it. TTYGIF enables you to convert any terminal screen recordings into smooth GIF files.

**Key Features:**

* Lets you create animated documentations and walk-throughs for your programs.

## **39\. [SVGO][70]**

[@**deepsweet**][71]

SVG is the new king of visual content on the web, but there's still more that can be done to improve the graphics files based on their origins. If you edit your SVG files using certain software, there's a high chance that the final files are going to be stuffed with useless data like comments, metadata, and other useless values that will only add extra weight to the final piece.

**Key Features:**

* Plugin-oriented structure, so anyone can create their optimization patterns, or choose the ones from the community.

## **40\. [pipes.sh][72]**

[@**Foggalong**][73]

Ever thought about giving your terminal a makeover in the form of a screensaver? Well, it turns out that someone cape up with the idea to do just that, so we couldn't resist including this little visual wonder. All you need to get this to work is Bash V4+, and you have yourself a way to hibernate your own terminal with a colorful pipes screensaver.

**Key Features:**

* For personalization, you can define custom settings for the way that the pipes appear on the screen.

## **41\. [WOPR][74]**

[@**YaronNaveh**][75]

WOPR is a custom-built markup for your terminal that can turn markup data into presentations, reports, and infographics directly within the terminal window. WOPR relies strictly on the blessed-contrib library (from the same author) which creates dashboards in ASCII format.

**Key Features:**

* You can convert the graphs into a web-friendly format and host them online.

## Entertainment

## **42\. [pockyt][76]**

[@**Pocket**][77]

Pocket is one of the most well-known bookmarking apps that you can find, and it's extremely reliable for saving and storing your most favorite links on the web. The pockyt library helps you manage your Pocket account right from the terminal. This command-line client interfaces the Pocket API and provides a way to interact with your pocket collection.

**Key Features:**

* You can fetch links and their excerpts and save them in a local file.
* You can search using custom tags and open those links in your browser.
* You can upload a new list of links from a TXT file.

## **43\. [movie-cli][78]**

[@**Mayank\_chd**][79]

Tired of writing code? Need to take a break? Just learned about a new hacker movie release you want to check out? Why not do it in the traditional fashion of running a command from your terminal? The Movie-CLI lets you quickly fetch information about a movie; just type in the name and you'll get all the juicy data output.

**Key Features:**

* You can compare two movies to see their main technical differences.

## **44\. [itunes-remote][80]**

[@**mkuehnel**][81]

iTunes-Remote uses JXA (Node.js) to create a terminal-based iTunes experience. It's simple enough to let you navigate music folders, and includes all the native music management functions.

**Key Features:**

* Play music on your MacOS without leaving the terminal.

## **45\. [cmus][82]**

[@**flyingmutant**][83]

Obviously iTunes is only for Mac computers, but what if you want something that works alongside all Unix based systems? The answer is C\* Music Player (cmus). This nifty little program creates a musical enterprise right in your terminal, letting you navigate and manage your music folders.

**Key Features:**

* You can use plugins to manage input and output file types.
* MP3 and Ogg streaming (SHOUTcast/Icecast).
* Instant startup, even with thousands of tracks.

## **46\. [facebook-cli][84]**

[@**tknomad**][85]

How about ditching the web UI of Facebook, and using FB only from the command line? Well, thanks to Facebook's openness towards developers, it is possible, and the usability is far greater than you'd expect. The Facebook-CLI is an all-in-one solution for using Facebook from your shell. All you need to do is create a new app for the Facebook API so that you can connect to the site using your credentials.

**Key Features:**

* Includes commands like events, photos, videos, post new stuff, feeds, likes, and more.

## **47\. [oysttyer][86]**

[@**atomicules**][87]

Likewise, Oysttyer is a terminal-interface for Twitter users, and it seems that these days devs are more keen towards using Twitter to discuss development than Facebook. Similarly to the above situation, you will need to create a Twitter App to authorize your own account for access to the site through your CMD.

**Key Features:**

* It covers all of the Twitter API features, so you can fully take control of your Twitter account.

## **48\. [youtube-dl][88]**

[@**romeogolf3**][89]

YouTube-DL is a Python-built program that allows you to download videos from YouTube without having to leave your terminal. It is a convenient piece of software if you ever stumble across an important, or relevant, talk that you like, letting you download it instantly to your computer and save for future use.

**Key Features:**

* You can specify a proxy for downloading.
* Playlist support means you can download full playlists at once. Download videos with a particular title (regex based).
* Lots of options for downloading.

## **49\. [medium-cli][90]**

[@**dheerajhere**][91]

Medium is a growing blogging platform that's gaining popularity within the developer community. It provides a beautiful UI for publishing stories that get views, and has the option for users to leave comments and highlight individual paragraphs of stories. Now, you can bring the Medium experience to your favorite place on the planet: the terminal!

**Key Features:**

* Some of the available commands include listing the top stories, reading, opening URLs with a browser, and searching based on custom input.

## **50\. [hget][92]**

[@**nzgb**][93]

This simple tool gives you the functionality to convert any HTML-based website into plain-text format. It's great if you wish to fetch the individual links to latest stories from your favorite news platform, or want to avoid any type of JavaScript/HTML operations in general. Either way, it all happens from within the command line, and the interface is kept to a minimum.

**Key Features:**

* Custom HTML parser that you can use to fetch a specific content output from the given website.

* [__ About the Author][94]
* [__ Latest Posts][95]

![](https://secure.gravatar.com/avatar/99e0459a6d11f4f510127934dfd98b94?s=80&d=retro&r=g)

#### About Alexandra Altvater

* [What to Do About Java Memory Leaks: Tools, Fixes, and More][96] - September 3, 2021
* [What is Load Testing? How It Works, Tools, Tutorials, and More][97] - February 5, 2021
* [Americaneagle.com and ROC Commerce stay ahead with Retrace][98] - September 25, 2020
* [Stackify's New Pricing: Everything you need to know][99] - September 9, 2020
* [INNOVATORS VS COVID 19 Matt Watson, the CEO at Stackify, advises Entrepreneurs to focus on the things that make them happy, regardless if work is a giant dumpster fire][100] - September 2, 2020



[0]: https://stackify.com/developers/ "View all posts in: “Developer Tips, Tricks & Resources”"
[1]: #WebDevelopment
[2]: #Productivity
[3]: #Utility
[4]: #Visual
[5]: #Entertainment
[6]: https://github.com/sindresorhus/is-up-cli
[7]: https://twitter.com/sindresorhus
[8]: https://github.com/sindresorhus
[9]: https://github.com/sindresorhus/pageres-cli
[10]: https://github.com/kevva/viewport-list-cli
[11]: https://github.com/kevva
[12]: https://surge.sh/
[13]: https://twitter.com/surge_sh
[14]: https://github.com/alexfernandez/loadtest
[15]: https://twitter.com/pinchito
[16]: https://github.com/wp-cli/wp-cli
[17]: https://twitter.com/wpcli
[18]: https://github.com/rtfpessoa/diff2html-cli
[19]: https://twitter.com/rtfpessoa
[20]: https://stackify.com/telemetry-tutorial/
[21]: https://github.com/sgentle/caniuse-cmd
[22]: https://twitter.com/caniuse
[23]: https://github.com/sindresorhus/npm-name-cli
[24]: https://github.com/sindresorhus/strip-css-comments-cli
[25]: https://httpie.org/
[26]: https://twitter.com/clihttp
[27]: http://www.jefftk.com/icdiff
[28]: http://pandoc.org/
[29]: https://babun.github.io/
[30]: https://twitter.com/babunshell
[31]: https://github.com/omidfi/moro
[32]: https://twitter.com/omidfi
[33]: https://github.com/keepcosmos/terjira
[34]: https://github.com/samg/timetrap
[35]: https://twitter.com/_SamG
[36]: https://taskwarrior.org/
[37]: https://twitter.com/taskwarrior
[38]: https://github.com/VitaliyRodnenko/geeknote
[39]: https://twitter.com/VitaliyRodnenko
[40]: https://github.com/kevva/imgur-uploader-cli
[41]: http://brettterpstra.com/projects/doing/
[42]: https://twitter.com/ttscoff
[43]: https://github.com/jaebradley/uber-cli
[44]: https://stedolan.github.io/jq/
[45]: https://github.com/wting/autojump
[46]: https://twitter.com/_wting
[47]: http://ranger.nongnu.org/
[48]: https://github.com/gillstrom/battery-level
[49]: https://twitter.com/hynden
[50]: https://github.com/kevva/brightness-cli
[51]: https://github.com/yudai/gotty
[52]: https://twitter.com/i_yudai
[53]: https://github.com/zquestz/s
[54]: https://twitter.com/zquestz
[55]: https://github.com/aria2/aria2
[56]: https://twitter.com/tatsuhiro_t
[57]: https://github.com/marionebl/remote-share-cli
[58]: https://twitter.com/marionebl
[59]: https://hub.github.com/
[60]: https://twitter.com/github
[61]: https://tmux.github.io/
[62]: https://github.com/metadelta/mdlt
[63]: https://twitter.com/metadeltamath
[64]: https://github.com/lukechilds/gifgen
[65]: https://twitter.com/lukechilds123
[66]: https://github.com/kohler/gifsicle
[67]: https://twitter.com/xexd
[68]: https://github.com/icholy/ttygif
[69]: https://twitter.com/icholy
[70]: https://github.com/svg/svgo
[71]: https://twitter.com/deepsweet
[72]: https://github.com/pipeseroni/pipes.sh
[73]: https://twitter.com/Foggalong
[74]: https://github.com/yaronn/wopr
[75]: https://twitter.com/YaronNaveh
[76]: https://github.com/arvindch/pockyt
[77]: https://twitter.com/Pocket
[78]: https://github.com/mayankchd/movie
[79]: https://twitter.com/Mayank_chd
[80]: https://github.com/mischah/itunes-remote
[81]: https://twitter.com/mkuehnel
[82]: https://github.com/cmus/cmus
[83]: https://twitter.com/flyingmutant
[84]: https://github.com/specious/facebook-cli
[85]: https://twitter.com/tknomad
[86]: https://github.com/oysttyer/oysttyer
[87]: https://twitter.com/atomicules
[88]: https://rg3.github.io/youtube-dl/
[89]: https://twitter.com/romeogolf3
[90]: https://github.com/djadmin/medium-cli
[91]: https://twitter.com/dheerajhere
[92]: https://github.com/bevacqua/hget
[93]: https://twitter.com/nzgb
[94]: #wpautbox_about
[95]: #wpautbox_latest-post
[96]: https://stackify.com/java-memory-leaks-solutions/
[97]: https://stackify.com/what-is-load-testing/
[98]: https://stackify.com/americaneagle-com-and-roc-commerce-stay-ahead-with-retrace/
[99]: https://stackify.com/stackifys-new-pricing-everything-you-need-to-know/
[100]: https://stackify.com/innovators-vs-covid-19-matt-watson-the-ceo-at-stackify-advises-entrepreneurs-to-focus-on-the-things-that-make-them-happy-regardless-if-work-is-a-giant-dumpster-fire/