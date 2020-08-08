# Jupyter Notebooks

## Adding kernel for Hydrogen in Atom

1. Install the ipykernel in your virtual environment:
`pipenv install ipykernel`

2. Start shell with:
`pipenv shell`

3. Set name so Atom Hydrogen can recognize:
`pipenv run python -m ipykernel install --user --name=name-of-kernel`

4. Start Atom (from within pipenv shell) and when you run code (control-enter), Atom should list python kernels to use (including `name-of-kernel`)

## Installing Modules

```python
# Install a pip package in the current Jupyter kernel
import sys
!{sys.executable} -m pip install scipy
```

the last word is the name of the module to install

## Capturing Output to File

You can use `%%capture` Jupyter notebook's magic command to catch output of cell and then paste it to your text file with

```python
with open('output.txt', 'w') as out:
   out.write(cap.stdout)
```

if you want to cell code to specific file for example.txt you can use magic function `%%writefile`

```python
%%writefile example.txt
ab = 'This is code'
a = 5
print(a+ 2)
```

Also if you want to append to file you must use `-a` parameter

---

-   [How\_to\_get\_started\_coding\_in\_Python?](https://nbviewer.jupyter.org/github/Tanu-N-Prabhu/Python/blob/master/How_to_get_started_coding_in_Python%3F.ipynb),
    this notebook explains how to become a good python programmer, by
    [Tanu Nanda Prabhu](https://github.com/Tanu-N-Prabhu/Python), author
    and editor at [Towards data
    science](https://medium.com/@tanunprabhu95)

-   [Python Strings from Scratch
    !!!](https://nbviewer.jupyter.org/github/Tanu-N-Prabhu/Python/blob/master/Strings/Strings.ipynb),
    this notebook explains Python Strings from basic to advance level,
    by [Tanu Nanda Prabhu](https://github.com/Tanu-N-Prabhu/Python)

-   [Python Tuples from Scratch
    !!!](https://nbviewer.jupyter.org/github/Tanu-N-Prabhu/Python/blob/master/Tuples/%20Tuples.ipynb),
    this notebook explains Python Tuples from basic to advance level, by
    [Tanu Nanda Prabhu](https://github.com/Tanu-N-Prabhu/Python)

-   [Python Dictionary from Scratch
    !!!](https://nbviewer.jupyter.org/github/Tanu-N-Prabhu/Python/blob/master/Dictionary%20/%20Python_Dictionary.ipynb),
    this notebook explains Python Dictionary from basic to advance
    level, by [Tanu Nanda
    Prabhu](https://github.com/Tanu-N-Prabhu/Python)

-   [Python Lists from Scratch
    !!!](https://nbviewer.jupyter.org/github/Tanu-N-Prabhu/Python/blob/master/Lists.ipynb),
    this notebook explains Python Lists from basic to advance level with
    the help of an example, by [Tanu Nanda
    Prabhu](https://github.com/Tanu-N-Prabhu/Python).

-   [Learning to code with
    Python](http://nbviewer.ipython.org/urls/bitbucket.org/amjoconn/watpy-learning-to-code-with-python/raw/3441274a54c7ff6ff3e37285aafcbbd8cb4774f0/notebook/Learn%20to%20Code%20with%20Python.ipynb),
    part of an [introduction to
    Python](https://bitbucket.org/amjoconn/watpy-learning-to-code-with-python/src)
    from the [Waterloo Python users
    group](http://watpy.ca/blog/post/learn-code-python-review-feb-2013).

-   [Introduction to Python for Data
    Scientists](http://nbviewer.jupyter.org/github/phelps-sg/python-bigdata/blob/master/src/main/ipynb/intro-python.ipynb)
    by [Steve Phelps](http://sphelps.net) (part of a larger collection
    on [Data Science and Big
    Data](https://github.com/phelps-sg/python-bigdata)).

-   [Python Descriptors
    Demystified](http://nbviewer.ipython.org/gist/ChrisBeaumont/5758381/descriptor_writeup.ipynb),
    an in-depth discussion of the descriptor protocol in Python, by
    [Chris Beaumont](http://chrisbeaumont.org).

-   [A collection of not so obvious Python stuff you should
    know!](http://nbviewer.ipython.org/github/rasbt/python_reference/blob/master/tutorials/not_so_obvious_python_stuff.ipynb?create=1),
    by [Sebastian Raschka](https://github.com/rasbt).

-   [Key differences between Python 2.7.x and Python
    3.x](http://nbviewer.ipython.org/github/rasbt/python_reference/blob/master/tutorials/key_differences_between_python_2_and_3.ipynb),
    by [Sebastian Raschka](https://github.com/rasbt).

-   [A beginner's guide to Python's namespaces, scope resolution, and
    the LEGB
    rule](http://nbviewer.ipython.org/github/rasbt/python_reference/blob/master/tutorials/scope_resolution_legb_rule.ipynb?create=1),
    by [Sebastian Raschka](https://github.com/rasbt).

-   [Sorting CSV files using the Python csv
    module](http://nbviewer.ipython.org/github/rasbt/python_reference/blob/master/tutorials/sorting_csvs.ipynb),
    by [Sebastian Raschka](https://github.com/rasbt).

-   Python 3 OOP series by [Leonardo
    Giordani](https://github.com/lgiordani): [Part 1: Objects and
    types](http://nbviewer.ipython.org/github/lgiordani/blog_source/blob/master/pelican/content/notebooks/Python_3_OOP_Part_1__Objects_and_types.ipynb),
    [Part 2: Classes and
    members](http://nbviewer.ipython.org/github/lgiordani/blog_source/blob/master/pelican/content/notebooks/Python_3_OOP_Part_2__Classes_and_members.ipynb),
    [Part 3: Delegation - composition and
    inheritance](http://nbviewer.ipython.org/github/lgiordani/blog_source/blob/master/pelican/content/notebooks/Python_3_OOP_Part_3__Delegation__composition_and_inheritance.ipynb),
    [Part 4:
    Polymorphism](http://nbviewer.ipython.org/github/lgiordani/blog_source/blob/master/pelican/content/notebooks/Python_3_OOP_Part_4__Polymorphism.ipynb),
    [Part 5:
    Metaclasses](http://nbviewer.ipython.org/github/lgiordani/blog_source/blob/master/pelican/content/notebooks/Python_3_OOP_Part_5__Metaclasses.ipynb),
    [Part 6: Abstract Base
    Classes](http://nbviewer.ipython.org/github/lgiordani/blog_source/blob/master/pelican/content/notebooks/Python_3_OOP_Part_6__Abstract_Base_Classes.ipynb)

-   [How to Aggregate Subscriber's Interest using the 3
    methods:](https://nbviewer.jupyter.org/github/abbas-taher/Montreal-Python-69/blob/master/Montreal%20Python%2069.ipynb) (1)
    Python Dictionary, (2) Apache PySpark - GroupBy Transformation,
    and (3) Apache PySpark - ReduceBy Transformation by [Abbas
    Taher](https://github.com/abbas-taher).
