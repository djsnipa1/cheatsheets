# Pastery

Pastery includes a very simple API that you can use for integration with editors and other programs.

## Duration for "never"

I found this [here](https://github.com/maximeplante/vscode-pastery/issues/2#issue-319908389)

> **`26280000`**

> According to the developer the pastery api does not have an option for never expire. What may work is using the parameter duration: 26280000, this results in a paste of about 50 years.

## Creating a paste

```shell
POST https://www.pastery.net/api/paste/
    ?api_key=<api_key>
    &duration=<duration>
    &title=<title>
    &language=<language>
    &max_views=<max_views>
```

The text to be pasted should be included in the raw POST body, and encoded as UTF-8. The trailing slash in the URL **is important**!

Parameters:

* **api_key**: The API key of the user whom the paste will belong to. You can get this from your account page.
* **duration** [optional]: The duration, in minutes, that this paste will live for. After `duration` minutes, the paste is deleted. The default duration is 30 days.
* **title** [optional]: The title of the paste (max 200 chars).
* **language** [optional]: The alias of the programming language that the paste is written in. A list of languages is below. If this is omitted or invalid, the language will be autodetected.
* **max_views** [optional]: The number of views allowed before the paste expires. Set it to 0 or omit it for no view-based expiration.

### Command-line example

Here's how you can upload a paste from a file called `data.txt` using `curl`:

```shell
$ curl -X POST https://www.pastery.net/api/paste/?title=Sample+data&api_key=mykey --data-binary @data.txt
{"url": "https://www.pastery.net/yfbfgg/", "duration": 1440, "title": "Sample data", "language": "python"}
```

or:

```shell
$ curl https://www.pastery.net/api/paste/ -F file=@data.txt
{"url": "https://www.pastery.net/yfbfgg/", "duration": 1440, "title": "Sample data", "language": "python"}
```


## Retrieving your pastes

```shell
GET https://www.pastery.net/api/paste/
    ?api_key=<api_key>
```

Parameters:

* **api_key** [optional]: The API key of the user whom the paste will belong to. This may become mandatory at some point, so it'd be best to pass one in any case. You can get this from your [account page](https://www.pastery.net/account/).

**Command-line example**

Here's how you can get a list of all your pastes using `curl`:

```shell
$ curl https://www.pastery.net/api/paste/?api_key=mykey
{
    "pastes": [
        {
            "duration": 800, 
            "id": "api", 
            "language": "markdown", 
            "title": "API documentation", 
            "url": "https://www.pastery.net/api/"
        },
        {
            "duration": 800, 
            "id": "about", 
            "language": "markdown", 
            "title": "About", 
            "url": "https://www.pastery.net/about/"
        }
    ]
}

```

## Retrieving a single paste

### API Description

```shell
GET https://www.pastery.net/api/paste/<id>/
    ?api_key=<api_key>
```

Parameters:

* **api_key** [optional]: The API key of the user whom the paste will belong to. This may become mandatory at some point, so it'd be best to pass one in any case. You can get this from your [account page](https://www.pastery.net/account/).

**Command-line example**

Here's how you can get a single paste using `curl`:

```shell
$ curl https://www.pastery.net/api/paste/about/?api_key=mykey
{
    "pastes": [
        {
            "duration": 800, 
            "id": "about", 
            "language": "markdown", 
            "title": "About", 
            "url": "https://www.pastery.net/about/"
        }
    ]
}

```

## Deleting a paste

```shell
DELETE https://www.pastery.net/api/paste/<id>/
    ?api_key=<api_key>
```

Parameters:

* **api_key** [optional]: The API key of the user whom the paste will belong to. This may become mandatory at some point, so it'd be best to pass one in any case. You can get this from your [account page](https://www.pastery.net/account/).

Here's how you can delete a paste using `curl`:

```shell
$ curl -X DELETE https://www.pastery.net/api/paste/sanwhh/?api_key=mykey
{"result": "success"}

```

## Language list

* autodetect
* bash
* c
* cpp
* csharp
* css
* html
* java
* js
* json
* lua
* markdown
* objective-c
* perl
* php
* python
* swift
* text
* autodetect
* abap
* ada
* agda
* ahk
* alloy
* antlr
* antlr-as
* antlr-cpp
* antlr-csharp
* antlr-java
* antlr-objc
* antlr-perl
* antlr-python
* antlr-ruby
* apacheconf
* apl
* applescript
* as
* as3
* aspectj
* aspx-cs
* aspx-vb
* asy
* at
* autoit
* awk
* basemake
* bat
* bbcode
* befunge
* blitzbasic
* blitzmax
* boo
* brainfuck
* bro
* bugs
* c-objdump
* ca65
* cbmbas
* ceylon
* cfc
* cfengine3
* cfm
* cfs
* chai
* chapel
* cheetah
* cirru
* clay
* clojure
* clojurescript
* cmake
* cobol
* cobolfree
* coffee-script
* common-lisp
* console
* control
* coq
* cpp-objdump
* croc
* cryptol
* css+django
* css+erb
* css+genshitext
* css+lasso
* css+mako
* css+mozpreproc
* css+myghty
* css+php
* css+smarty
* cucumber
* cuda
* cypher
* cython
* d
* d-objdump
* dart
* delphi
* dg
* diff
* django
* docker
* dpatch
* dtd
* duel
* dylan
* dylan-console
* dylan-lid
* ebnf
* ec
* ecl
* eiffel
* elixir
* erb
* erl
* erlang
* evoque
* factor
* fan
* fancy
* felix
* fortran
* foxpro
* fsharp
* gap
* gas
* genshi
* genshitext
* glsl
* gnuplot
* go
* golo
* gooddata-cl
* gosu
* groff
* groovy
* gst
* haml
* handlebars
* haskell
* haxeml
* html+cheetah
* html+django
* html+evoque
* html+genshi
* html+handlebars
* html+lasso
* html+mako
* html+myghty
* html+php
* html+smarty
* html+twig
* html+velocity
* http
* hx
* hybris
* hylang
* i6t
* idl
* idris
* iex
* igor
* inform6
* inform7
* ini
* io
* ioke
* ipython2
* ipython3
* ipythonconsole
* irc
* isabelle
* jade
* jags
* jasmin
* javascript+mozpreproc
* jlcon
* js+cheetah
* js+django
* js+erb
* js+genshitext
* js+lasso
* js+mako
* js+myghty
* js+php
* js+smarty
* jsonld
* jsp
* julia
* kal
* kconfig
* koka
* kotlin
* lagda
* lasso
* lcry
* lean
* lhs
* lidr
* lighty
* limbo
* liquid
* live-script
* llvm
* logos
* logtalk
* lsl
* make
* mako
* maql
* mask
* mason
* mathematica
* matlab
* matlabsession
* minid
* modelica
* modula2
* monkey
* moocode
* moon
* mozhashpreproc
* mozpercentpreproc
* mql
* mscgen
* mupad
* mxml
* myghty
* mysql
* nasm
* nemerle
* nesc
* newlisp
* newspeak
* nginx
* nimrod
* nit
* nixos
* nsis
* numpy
* objdump
* objdump-nasm
* objective-c++
* objective-j
* ocaml
* octave
* ooc
* opa
* openedge
* pan
* pawn
* perl6
* pig
* pike
* plpgsql
* postgresql
* postscript
* pot
* pov
* powershell
* prolog
* properties
* protobuf
* psql
* puppet
* py3tb
* pycon
* pypylog
* pytb
* python3
* qbasic
* qml
* racket
* ragel
* ragel-c
* ragel-cpp
* ragel-d
* ragel-em
* ragel-java
* ragel-objc
* ragel-ruby
* raw
* rb
* rbcon
* rconsole
* rd
* rebol
* red
* redcode
* registry
* resource
* rexx
* rhtml
* robotframework
* rql
* rsl
* rst
* rust
* sass
* scala
* scaml
* scheme
* scilab
* scss
* shell-session
* slim
* smali
* smalltalk
* smarty
* sml
* snobol
* sourceslist
* sp
* sparql
* spec
* splus
* sql
* sqlite3
* squidconf
* ssp
* stan
* swig
* systemverilog
* tads3
* tcl
* tcsh
* tea
* tex
* textile
* todotxt
* trac-wiki
* treetop
* ts
* twig
* urbiscript
* vala
* vb.net
* vctreestatus
* velocity
* verilog
* vgl
* vhdl
* vim
* xml
* xml+cheetah
* xml+django
* xml+erb
* xml+evoque
* xml+lasso
* xml+mako
* xml+myghty
* xml+php
* xml+smarty
* xml+velocity
* xquery
* xslt
* xtend
* xul+mozpreproc
* yaml
* yaml+jinja
* zephir



