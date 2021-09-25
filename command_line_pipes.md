[Know Your Pipes and Filters. Pipes and filters are everywhere. Not… | by Piyush Kochhar | The Startup | Aug, 2020 | Medium](https://medium.com/swlh/know-your-pipes-and-filters-1f1039b0577d)

# Know Your Pipes and Filters

## Pipes and filters are everywhere. Not just in your homes but also in the terminal.

![Image for post](https://miro.medium.com/max/2306/1*zevJOoH3COUwqhhj0R_fBA.png)
l

## What is a Filter? ䷜

A filter takes input from one command, does some processing, and gives output.

## Why filter data? 🗂

Filtering is useful when you want to extract specific information from large amounts of data. It doesn’t remove or modify any data; it just displays a subset of data on the screen. Sometimes we use **pipes** to filter complex data.

## What is a Pipe? 🚰

The symbol ‘|’ denotes a pipe. It is a command that takes an output of one command and feeds it as an input to the second command. You can combine two or more commands and run them consecutively with pipes.

Syntax:
```shell
$ command 1 | command 2 |… command n
```
Suppose we have a sample.txt file with the following data:

```shell
Adriaens Dishman  
Anna Tichner  
Bank Guerro  
Phil Cuniam  
Reagen Dobrovolny  
Cicily Veale  
Coop Joysey  
kendrick Liggons  
micheal Fray  
benn Cork  
Micheal Fray
```

## ***Let’s filter some data!***

**😸 `cat` :** Displays the contents of the file.

```plain
$ cat sample.txt

Adriaens Dishman
Anna Tichner
Bank Guerro
Phil Cuniam
Reagen Dobrovolny
Cicily Veale
Coop Joysey
kendrick Liggons
micheal Fray
benn Cor
Micheal Fray
```

---

**⫷ `less`**: Shows you only one scroll length of content at a time.

```shell
$ cat sample.txt | less

Adriaens Dishman
Anna Tichner
Bank Guerro
Phil Cuniam
Reagen Dobrovolny
Cicily Veale:
```
---

**⥱ `grep`**: Takes an argument as string and will find the matching string, if found it will return the matching string else will return nothing.

Following options can be used with grep command:

_`-v` →_ Shows all the lines that do not match the searched string

_`-c` →_ Displays only the count of matching lines

_`-n` →_ Shows the matching line and its number

_`-i` →_ Match both (upper and lower) case

_`-A(num)`_ → Print _NUM_ lines of trailing context after matching lines.

_-`B(num)`_ → Print _NUM_ lines of leading context before matching lines.

_`-C(num)`_ → Print _NUM_ lines of output context.

> **_-v_**

```shell
$ cat sample.txt | grep -v “Anna Tichner"

Adriaens Dishman
Bank Guerro
Phil Cuniam
Reagen Dobrovolny
Cicily Veale
Coop Joysey
kendrick Liggons
micheal Fray
benn Cork
Micheal Fray
```

> **_-c_**

```shell
$ cat sample.txt | grep -c "Anna Tichner" 

1
```

> **_-n_**

```shell
$ cat sample.txt | grep -n "Anna Tichner" 

2:Anna Tichner
```

> **_-i_**

```shell
$ cat sample.txt | grep -i "aNNa TiCHner"

Anna Tichner
```

> **_-A(num)_**

```shell
$ cat sample.txt | grep -A2 “Anna Tichner”

Anna Tichner
Bank Guerro
Phil Cuniam
```

> **_-B(num)_**

```shell
$ cat sample.txt | grep -B1 "Anna Tichner"
Adriaens Dishman
Anna Tichner
```

> **_-C(num)_**

```shell
$ cat sample.txt | grep -C1 "Anna Tichner"
Adriaens Dishman
Anna Tichner
Bank Guerro
```

---

**⋛ `sort`**: Sorts out the contents of a file.

```shell
$ cat sample.txt | sort

Adriaens Dishman
Anna Tichner
Bank Guerro
Cicily Veale
Coop Joysey
Micheal Fray
Phil Cuniam
Reagen Dobrovolny
benn Cork
kendrick Liggons
micheal Fray
```

Following options can be used with sort command:

**_`-r`_** → Reverse sorting

**_`-n`_** → Numerical sorting

**_`-f`_** → Case insensitive sorting

> **_-r_**

```shell
$ cat sample.txt | sort -r

micheal Fray
kendrick Liggons
benn Cork
Reagen Dobrovolny
Phil Cuniam
Micheal Fray
Coop Joysey
Cicily Veale
Bank Guerro
Anna Tichner
Adriaens Dishman
```

> **_-n_**

```shell
$ cat sample.txt | sort -n

Adriaens Dishman
Anna Tichner
Bank Guerro
Cicily Veale
Coop Joysey
Micheal Fray
Phil Cuniam
Reagen Dobrovolny
benn Cork
kendrick Liggons
micheal Fray
```

> **_-f_**

```shell
$ cat sample.txt | sort -f

Adriaens Dishman
Anna Tichner
Bank Guerro
benn Cork
Cicily Veale
Coop Joysey
kendrick Liggons
Micheal Fray
micheal Fray
Phil Cuniam
Reagen Dobrovolny
```

---

**👓 `uniq`:** Omits repeated lines.

```shell
$ cat sample.txt | uniq

Adriaens Dishman
Anna Tichner
Bank Guerro
Phil Cuniam
Reagen Dobrovolny
Cicily Veale
Coop Joysey
kendrick Liggons
micheal Fray
benn Cork
Micheal Fray
```

Following option can be used with uniq command:

> **_`-c`_** → Indicates the number of occurrences of a line.

```shell
$ cat sample.txt | uniq -c

1 Adriaens Dishman
1 Anna Tichner
1 Bank Guerro
1 Phil Cuniam
1 Reagen Dobrovolny
1 Cicily Veale
1 Coop Joysey
1 kendrick Liggons
1 micheal Fray
1 benn Cork
1 Micheal Fray
```

---

**☕️ `tee`:** Reads from the standard input and writes to both standard output and one or more files at the same time.

```shell
$ echo "New text here" | tee newfile.txt newfile2.txt

New text here
```

The above command creates `newfile1.txt` and `newfile2.txt` with the text `“New text here”`.

Following option can be used with `tee` command:

> **_`-a`_** → Appends the output to a file instead of overwriting it.

```shell
$ echo "New text here" | tee -a newfile.txt

New text here
```

Use _`/dev/null`_ to hide the standard output

```shell
$ echo "New text here" | tee -a newfile.txt 

/dev/null
```

---

**✂️ cu`cut`:** Slices a line and extracts the text. It is necessary to specify option with command otherwise it gives error.

Following options can be used with `cut` command

**_`-b` →_** Extracts specific bytes

**_`-c`_** → Cuts the characters by column

**_`-f`_** → Cuts the character to the delimiter character with the specified field number

**_`-d`_** → delimiter, mostly used in conjunction with -f

> Filter the text to get 1st, 4th & 8th character using **_-b_**

```shell
$ cat sample.txt | cut -b 1,4,8

Ais
Aac
Bke
Pln
RgD
CiV
Cpy
kdk
mh
bnr
Mh
```

> Filter the text to get characters in range \[1–4\] & \[9–11\] using **_-b_**

```shell
$ cat sample.txt | cut -b 1-4,9-11

Adri Di
Annahne
Bankrro
Philiam
Reagobr
Cicieal
Coopsey
kend Li
michFra
bennk
MichFra
```

> Filter text to get characters in column \[1–3\] using **_-c_**

```shell
$ cat sample.txt | cut -c 1-3

Adr
Ann
Ban
Phi
Rea
Cic
Coo
ken
mic
ben
Mic
```

> Filter text to get last name using **_-d_**

```shell
$ cat sample.txt | cut -d " " -f 2

Dishman
Tichner
Guerro
Cuniam
Dobrovolny
Veal
eJoysey
Liggons
Fray
Cork
Fray
```

---

**✏️ fmt:** A Simple optimal text formatter, it reformats paragraphs in specified file.

```shell
$ cat sample.txt | fmt

Adriaens Dishman Anna Tichner Bank 
Guerro Phil Cuniam Reagen 
Dobrovolny Cicily Veale Coop 
Joysey kendrick Liggons Micheal  
Fraybenn Cork Micheal Fray
```
Following option can be used with fmt command:

> **_-w_** → Reformat the text with a specific line width

```shell
$ cat sample.txt | fmt -w 1
AdriaensDishmanAnnaTichnerBankGuerroPhilCuniamReagenDobrovolnyCicilyVealeCoopJoyseykendrick  
```
...

* * *

**🤯 head:** Displays the first parts of a file, it outputs the first 10 lines by default.

$ cat sample.txt | headAdriaens DishmanAnna TichnerBank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn Cork

Following option can be used with head command:

> **_-n_** → Number of lines to be displayed

$ cat sample.txt | head -n 5Adriaens DishmanAnna TichnerBank GuerroPhil CuniamReagen Dobrovolny

* * *

**🌀 tail:** Displays the last parts of a file, it outputs the last 10 lines by default.

$ cat sample.txt | tailAnna TichnerBank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn CorkMicheal Fray

Following option can be used with tailcommand:

> **_-n_** → Number of lines to be displayed

$ cat sample.txt | tail -n 5Coop Joyseykendrick Liggonsmicheal Fraybenn CorkMicheal Fray

* * *

**📝 tr:** Translates or deletes characters from standard input.

> Lowercase to uppercase

$ cat sample.txt | tr \[:lower:\] \[:upper:\]ADRIAENS DISHMANANNA TICHNERBANK GUERROPHIL CUNIAMREAGEN DOBROVOLNYCICILY VEALECOOP JOYSEYKENDRICK LIGGONSMICHEAL FRAYBENN CORKMICHEAL FRAY

**Note**: We can also use regular expressions to translate the data.

> Apply ROT13 cipher to translate the data. To know more about ROT13 visit [_here_](https://medium.com/@piyush.kochhar1/rot13-a-missing-guide-c811427cfe6e)_._

$ cat sample.txt | tr a-zA-Z n-za-mN-ZA-MNqevnraf QvfuznaNaan GvpuareOnax ThreebCuvy PhavnzErntra QboebibyalPvpvyl IrnyrPbbc Wblfrlxraqevpx Yvttbafzvpurny Senloraa PbexZvpurny Senl

* * *

**⏳ sed:** A stream editor for filtering and transforming text.

We can use regular expressions to transform our text.

> To replace a substring: ‘s/text to replace/replacement text

$ cat sample.txt | sed 's/micheal/Michelle/'Adriaens DishmanAnna TichnerBank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick LiggonsMichelle Fraybenn CorkMicheal Fray

> To replace the nth occurrence: ‘s/text to replace/replacement text/occurence_no

$ cat sample.txt | sed 's/Micheal/Michelle/1'Adriaens DishmanAnna TichnerBank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn CorkMichelle Fray

> To replace all occurrences: ‘s/text to replace/replacement text/g

$ cat sample.txt |tr \[:upper:\] \[:lower:\] |sed 's/micheal/michelle/g'adriaens dishmananna tichnerbank guerrophil cuniamreagen dobrovolnycicily vealecoop joyseykendrick liggonsmichelle fraybenn corkmichelle fray

> To delete a line: ‘(line num)d’

_For nth line replace ‘2’ with the number of your line_

$ cat sample.txt | sed '2d'Adriaens DishmanBank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn CorkMicheal Fray

> To delete lines from range x to y: ‘(first line), (last line)d’

$ cat sample.txt | sed '1,5d'Cicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn CorkMicheal Fray

> To delete last line: ‘$d’

$ cat sample.txt | sed '$d'Adriaens DishmanAnna TichnerBank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn Cork

> To delete a line that matches a pattern: ‘pattern’

$ cat sample.txt | sed '/A/d'Bank GuerroPhil CuniamReagen DobrovolnyCicily VealeCoop Joyseykendrick Liggonsmicheal Fraybenn CorkMicheal Fray

**✍️ od**: Returns contents of a file in specified number system. It returns hexadecimal by default.

$ cat sample.txt | od0000000 062101 064562 062541  071556  042040  071551  066550  0671410000020 005015 067101 060556  052040  061551  067150  071145  0050150000040 060502 065556 043440  062565  071162  005157  064120  0661510000060 041440 067165 060551  006555  051012  060545  062547  0201560000100 067504 071142 073157  066157  074556  005015  064503  0645430000120 074554 053040 060545  062554  005015  067503  070157  0450400000140 074557 062563 006571  065412  067145  071144  061551  0201530000160 064514 063547 067157  006563  066412  061551  062550  0661410000200 043040 060562 006571  061012  067145  020156  067503  0655620000220 005015 064515 064143  060545  020154  071106  074541  0050150000240

> Get output in octal using **_-b_**

$ cat sample.txt | od -b0000000 101 144 162 151 141 145 156 163 040 104 151 163 150 155 ... 0000020 015 012 101 156 156 141 040 124 151 143 150 156 145 162 ...0000040 102 141 156 153 040 107 165 145 162 162 157 012 120 150 ...0000060 040 103 165 156 151 141 155 015 012 122 145 141 147 145 ...0000100 104 157 142 162 157 166 157 154 156 171 015 012 103 151 ...0000120 154 171 040 126 145 141 154 145 015 012 103 157 157 160 ...0000140 157 171 163 145 171 015 012 153 145 156 144 162 151 143 ...0000160 114 151 147 147 157 156 163 015 012 155 151 143 150 145 ...0000200 040 106 162 141 171 015 012 142 145 156 156 040 103 157 ...0000220 015 012 115 151 143 150 145 141 154 040 106 162 141 171 ...

> Get output in character format using **_-c_**

$ cat sample.txt | od -c0000000  A   d   r  i  a   e   n   s       D   i   s   h   m   a   n0000020 \\r  \\n   A  n  n   a       T   i   c   h   n   e   r  \\r  \\n0000040  B   a   n  k      G   u   e   r   r   o  \\n   P   h   i   l0000060      C   u  n  i   a   m  \\r  \\n   R   e   a   g   e   n0000100  D   o   b  r  o   v   o   l   n   y  \\r  \\n   C   i   c   i0000120  l   y      V  e   a   l   e  \\r  \\n   C   o   o   p       J0000140  o   y   s  e  y  \\r  \\n   k   e   n   d   r   i   c   k0000160  L   i   g  g  o   n   s  \\r  \\n   m   i   c   h   e   a   l0000200      F   r  a  y  \\r  \\n   b   e   n   n       C   o   r   k0000220 \\r  \\n   M  i  c   h   e   a   l       F   r   a   y  \\r  \\n0000240

**✣ wc**: Returns line, word and character count.

$ cat sample.txt | wc11      22     160

**_Hope you are now better at understanding pipes and filters!_**
