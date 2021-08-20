# Markdown: how to make a link/jump in md files 
## 1. jump in one page <a name="h1"></a>

``` jump code

# definition of custom ID
### My Great Heading {#custom-id}

# in HTML syntax
<h3 id="custom-id">My Great Heading</h3>

# the syntax with custom heading IDs
[to be displayed](#title number-title text)

# in the HTML syntax
<a href="#heading-ids">Heading IDs</a>

# set a hook and jump
<span id="jump">idortext</span>
[taptojump](#jump)
```

## 2. jump to another page 

``` another one

[to be displayed](URLs)

# or you can also add a title to the URLs
(URLs) --- (URLs"title")
```

## 3. try for a while

[the first](#h2)
