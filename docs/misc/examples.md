# Examples of how to use mkdocs

## Code Annotation Examples

### Codeblocks

Some `code` goes here.

### Plain codeblock

A plain codeblock:

```
Some code here
def myfunction()
// some comment
```

#### Code for a specific language

Some more code with the `py` at the start:

``` py
import tensorflow as tf
def whatever()
```

#### With a title

``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

#### With line numbers

``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

#### Highlighting lines

``` py hl_lines="2 3"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

## Icons and Emojs

##### Emojs: <small><a href="https://gist.github.com/rxaviers/7360908" target="_blank">list</a></small>  
:smile: :purple_heart:  


##### FontAwesome Icons <small><a href="https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons/fontawesome" target="_blank">list</a></small>  
:fontawesome-regular-face-laugh-wink:
:fontawesome-brands-twitter:{ .twitter }  


##### Octicons <small><a href="https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons/octicons" target="_blank">list</a></small>  
:octicons-heart-fill-24:{ .heart }
:octicons-alert-24:  
>

##### Simple Icons <small><a href="https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons/simple" target="_blank">list</a></small>  
:simple-adidas:
:simple-digitalocean:  


##### Material Icons <small><a href="https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons/material" target="_blank">list</a></small>     
:material-account-cog:
:material-account-credit-card-outline:


:logo-monochrome:
:logo:



 