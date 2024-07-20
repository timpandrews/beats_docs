# Examples of how to use mkdocs (Code, Icons/Emojs, Images)

## Code Annotation Examples

### Codeblocks
To create inline code, use single backticks (`) around the code

Some `code` goes here.

### Plain codeblock
To create a code block in Markdown, you can use three backticks (```) before and after the code. Optionally, you can specify the language for syntax highlighting.

```
Some code here
def myfunction()
// some comment
```

#### Code for a specific language
Optionally, you can specify the language for syntax highlighting.  You can user the three
backticks followed by the language ie (``` python)

<small>The following languages are supported (**python**, **py**, javascript, java, c, cpp, csharp, **html**, **css**, ruby, php, **bash**, **json**, **yaml**, markdown, sql, r, go, swift, kotlin, perl)</small>

*(``` py)*

``` py
import tensorflow as tf
def whatever()
```

#### With a title
*(``` py title="bubble_sort.py")*

``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

#### With line numbers
*(``` py linenums="1")*

``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

#### Highlighting lines
*(``` py hl_lines="2 3")*

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

## Images
![Beats Documentation](../assets/icons/beats_docs.jpg){: width="25%"}  
```
![Beats Documentation](../assets/icons/beats_docs.jpg){: width="25%"}  
```
![Jenzen JoyRider](../assets/JenZen.jpg){: width="25%"}

```
![Jenzen JoyRider](../assets/JenZen.jpg){: width="25%"}  
```

**When referencing images in your MkDocs project, be mindful of the directory level of your Markdown file relative to the image directory. In some cases, you may need to navigate up one level to access the image folder, for example, ```![Alt text](../assets/image.jpg)```. In other situations, if your Markdown file is at the same level as the assets folder, you can reference the image directly, like this: ```![Alt text](assets/image.jpg)```.*