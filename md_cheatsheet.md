Sample Markdown Cheat Sheet
===========================

This is a sample markdown file to help you write Markdown quickly :)

If you use the fabulous [Sublime Text 2/3
editor](http://sublimetext.com) along with the [Markdown Preview
plugin](https://github.com/revolunet/sublimetext-markdown-preview), open
your ST2 Palette with `CMD+⇧+P` then choose
`Markdown Preview in browser` to see the result in your browser.

Text basics
-----------

this is *italic* and this is **bold** . another *italic* and another
**bold**

this is `important` text. and percentage signs : % and `%`

This is a paragraph with a footnote (builtin parser only). \[^note-id\]

Insert `[ TOC ]` without spaces to generate a table of contents (builtin
parsers only).

Indentation
-----------

> Here is some indented text
>
> > even more indented

Titles
------

Big title (h1)
==============

Middle title (h2)
-----------------

### Smaller title (h3)

#### and so on (hX)

##### and so on (hX)

###### and so on (hX)

Example lists (1)
-----------------

-   bullets can be `-`, `+`, or `*`
-   bullet list 1
-   bullet list 2
    -   sub item 1
    -   sub item 2

        with indented text inside

-   bullet list 3
-   bullet list 4
-   bullet list 5

Links
-----

This is an [example inline link](http://lmgtfy.com/) and [another one
with a title](http://lmgtfy.com/ "Hello, world").

Links can also be reference based : [reference 1](http://revolunet.com)
or [reference 2 with title](http://revolunet.com "rich web apps").

References are usually placed at the bottom of the document

Images
------

A sample image :

![revolunet
logo](http://www.revolunet.com/static/parisjs8/img/logo-revolunet-carre.jpg "revolunet logo")

As links, images can also use references instead of inline links :

![revolunet
logo](http://www.revolunet.com/static/parisjs8/img/logo-revolunet-carre.jpg "revolunet logo")

Code
----

It's quite easy to show code in markdown files.

Backticks can be used to `highlight` some words.

Also, any indented block is considered a code block. If
`enable_highlight` is `true`, syntax highlighting will be included (for
the builtin parser - the github parser does this automatically).

    <script>
        document.location = 'http://lmgtfy.com/?q=markdown+cheat+sheet';
    </script>

Math
----

Math can be displayed in the browser using MathJax or Katex. The feature
can be enabled by correctly configuring the `"js"`, `"css"`, and
`"markdown_extensions"` configuration fields. This allows for inline
math to be included \\(\\frac{\\pi}{2}\\) $\pi$.

Alternatively, math can be written on its own line:

$$F(\omega) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} f(t) \, e^{ - i \omega t}dt$$

\\\[\\int\_0^1 f(t) \\mathrm{d}t\\\]

\\\[\\sum\_j \\gamma\_j^2/d\_j\\\]

GitHub Flavored Markdown
------------------------

If you use the Github parser, you can use some of [Github Flavored
Markdown](https://help.github.com/articles/github-flavored-markdown/)
syntax :

-   User/Project@SHA:
    revolunet/sublimetext-markdown-preview@7da61badeda468b5019869d11000307e07e07401
-   User/Project\#Issue: revolunet/sublimetext-markdown-preview\#1
-   User : @revolunet

Some Python code :

``` python
import random

class CardGame(object):
    """ a sample python class """
    NB_CARDS = 32
    def __init__(self, cards=5):
        self.cards = random.sample(range(self.NB_CARDS), 5)
        print 'ready to play'
```

Some Javascript code :

``` js
var config = {
    duration: 5,
    comment: 'WTF'
}
// callbacks beauty un action
async_call('/path/to/api', function(json) {
    another_call(json, function(result2) {
        another_another_call(result2, function(result3) {
            another_another_another_call(result3, function(result4) {
                alert('And if all went well, i got my result :)');
            });
        });
    });
})
```

The Github Markdown also brings some [nice Emoji
support](http://www.emoji-cheat-sheet.com/) : :+1: :heart: :beer:

Parsers and Extensions
----------------------

Markdown Preview comes with **Python-Markdown** preloaded.

### *Python-Markdown*

The [Python-Markdown
Parser](https://github.com/Python-Markdown/markdown) provides support
for several extensions.

#### Extra Extensions

-   `abbr` --
    [Abbreviations](https://python-markdown.github.io/extensions/abbreviations)
-   `attr_list` -- [Attribute
    Lists](https://python-markdown.github.io/extensions/attr_list)
-   `def_list` -- [Definition
    Lists](https://python-markdown.github.io/extensions/definition_lists)
-   `fenced_code` -- [Fenced Code
    Blocks](https://python-markdown.github.io/extensions/fenced_code_blocks)
-   `footnotes` --
    [Footnotes](https://python-markdown.github.io/extensions/footnotes)
-   `tables` --
    [Tables](https://python-markdown.github.io/extensions/tables)
-   `smart_strong` -- [Smart
    Strong](https://python-markdown.github.io/extensions/smart_strong)

You can enable them all at once using the `extra` keyword.

    extensions: [ 'extra' ]

If you want all the extras plus the `toc` extension, your settings would
look like this:

    {
        ...
        parser: 'markdown',
        extensions: ['extra', 'toc'],
        ...
    }

#### Other Extensions

There are also some extensions that are not included in Markdown Extra
but come in the standard Python-Markdown library.

-   `code-hilite` --
    [CodeHilite](https://python-markdown.github.io/extensions/code_hilite)
-   `header-id` --
    [HeaderId](https://python-markdown.github.io/extensions/header_id)
-   `meta_data` --
    [Meta-Data](https://python-markdown.github.io/extensions/meta_data)
-   `nl2br` -- [New Line to
    Break](https://python-markdown.github.io/extensions/nl2br)
-   `sane_lists` -- [Sane
    Lists](https://python-markdown.github.io/extensions/sane_lists)
-   `smarty` --
    [Smarty](hhttps://python-markdown.github.io/extensions/smarty)
-   `toc` -- [Table of
    Contents](https://python-markdown.github.io/extensions/toc)
-   `wikilinks` --
    [WikiLinks](https://python-markdown.github.io/extensions/wikilinks)

#### 3rd Party Extensions

*Python-Markdown* is designed to be extended.

Some included ones are:

-   `delete` -- github style delte support via `~~word~~`
-   `githubemoji` -- github emoji support
-   `tasklist` -- github style tasklists
-   `magiclink` -- github style auto link conversion of http\|ftp links
-   `headeranchor` -- github style header anchor links
-   `github` -- Adds the above extensions in one shot
-   `b64` -- convert and embed local images to base64. Setup by adding
    this `b64(base_path=${BASE_PATH})`

There are also a number of others available:

Just fork this repo and add your extensions inside the
`.../Packages/Markdown Preview/markdown/extensions/` folder.

Check out the list of [3rd Party
extensions](https://github.com/waylan/Python-Markdown/wiki/Third-Party-Extensions).

#### Default Extensions

The default extensions are:

-   `footnotes` --
    [Footnotes](https://python-markdown.github.io/extensions/footnotes)
-   `toc` -- [Table of
    Contents](https://python-markdown.github.io/extensions/toc)
-   `fenced_code` -- [Fenced Code
    Blocks](https://python-markdown.github.io/extensions/fenced_code_blocks)
-   `tables` --
    [Tables](https://python-markdown.github.io/extensions/tables)

Use the `default` keyword, to select them all. If you want all the
defaults plus the `definition_lists` extension, your settings would look
like this:

    {
        ...
        parser: 'markdown',
        extensions: ['default', 'definition_lists'],
        ...
    }

Examples
--------

### Tables

The `tables` extension of the *Python-Markdown* parser is activated by
default, but is currently **not** available in *Markdown2*.

The syntax was adopted from the [php markdown
project](http://michelf.ca/projects/php-markdown/extra/#table), and is
also used in github flavoured markdown.

| Year | Temperature (low) | Temperature (high) |
|------|-------------------|--------------------|
| 1900 | -10               | 25                 |
| 1910 | -15               | 30                 |
| 1920 | -10               | 32                 |

### Wiki Tables

If you are using *Markdown2* with the `wiki-tables` extra activated you
should see a table below:

\|\| *Year* \|\| *Temperature (low)* \|\| *Temperature (high)* \|\|  
\|\| 1900 \|\| -10 \|\| 25 \|\|  
\|\| 1910 \|\| -15 \|\| 30 \|\|  
\|\| 1920 \|\| -10 \|\| 32 \|\|

### Definition Lists

This example requires *Python Markdown*'s `def_list` extension.

Apple : Pomaceous fruit of plants of the genus Malus in the family
Rosaceae.

Orange : The fruit of an evergreen tree of the genus Citrus.

About
-----

This plugin and this sample file is proudly brought to you by the
[revolunet team](http://revolunet.com)
