# Vim useful tips

[Motions](#motions)

[Text Object Selection](#selection)

[Operation](#operation)

[Substitution Command](#substitution)

[Terminal in nvim](#terminal)

[regex](#regex)

## Motions <a name="motions"></a>

> Move the cursor position, can be used after an operator command  
> [count] {motion} repeats {motion} [count] times

- linewise / charactereise
1. linewise : moving between lines affect lines
2. characterwise : move within a line affect characters

- exclusive / inclusive
1. exclusive : the last character towards the end of the buffer is not included
2. inclusice : the start and end position of the motion are included in the operation


### __Chr motions__

| Motion      | Action                |
|-------------|-----------------------|
| h, j, k, l  | left, down, up, right |
| ctrl + j, k | quick down, up        |

### __Word motions__

| Motion | Action                      |
|--------|-----------------------------|
| w  | ords                        |
| W  | WORDS forward               |
| b  | words backward              |
| B  | WORDS backward              |
| e  | Forward to the end of word  |
| E  | Forward to the end of WORD  |
| ge | Backward to the end of word |
| gE | Backward to the end of WORD |

### __Sentence motions__

| Motion | Action                                           |
|--------|--------------------------------------------------|
| 0      | To the first character of the line               |
| ^      | To the first non-blank character of the line     |
| \$     | To the end of the line                           |
| g_     | To the last non-blank character of the line      |
| -      | lines upward, on the first non-blank character   |
| enter  | lines downward, on the first non-blank character |


### __Text target motions__

| Motion | Action                                   |
|--------|------------------------------------------|
| %      | Find the next item and jump to its match |
| (      | sentences backward                       |
| )      | sentences forward                        |
| {      | paragraphs backward                      |
| }      | paragraphs forward                       |
| \]\]   | sections forward or to the next '{'      |
| \[\[   | sections backward or to the previous '{' |
| \]\[   | sections forward or to the next '}'      |
| \[\]   | sections backward or to the previous '}' |


### __Window motions__

| Motion | Action                                                        |
|--------|---------------------------------------------------------------|
| ctrl-d | Scroll half window Downwards in the buffer                    |
| ctrl-u | Scroll half window Upwards in the buffer                      |
| ctrl-f | Scroll window pages Forwards (downwards) in the buffer        |
| ctrl-b | Scroll window [count] pages Backwards (upwards) in the buffer |
| zz     | line at the center of the window                              |
| H      | To the first line of window                                   |
| M      | To the middle line of window                                  |
| L      | To the bottom line of window                                  |


### __Search motions__ 

| Motion                | Action                                                                         |
|-----------------------|--------------------------------------------------------------------------------|
| ###                   | Search forward for the [count]'th occurrence of the word nearest to the cursor |
| #                     | Same as aabove but search backward                                             |
| {count} f {char}      | To [count]'th occurrence of {char} to the right                                |
| F                     | Opposite direction of f                                                        |
| {count} t {char}      | Till before [count]'th occurrence of {char} to the right                       |
| T                     | Opposite direction of t                                                        |
| / {pattern} [/] enter | Search forward for the [count]'th occurrence of {pattern}                      |
| ? {pattern} [?] enter | Search backward for the [count]'th previous occurrence of {pattern}            |
| n                     | Repeat the latest "/" or "?" [count] times                                     |
| N                     | Repeat the latest "/" or "?" [count] times in opposite direction               |



## Text object selection <a name='selection'></a>

> Only be used while in Visual mode or after an operator  
> modifiers 'a' and 'i'  differs from mode key


1. Modifier 


2. Text object
	6. block symbol

* Usage after an operator
	1. For non-block objects:
		- "a" commands applies to the object and the white space after the object
		- "i" commands applies to the object but the space except for the cursor is on white space
	2. For a block object 
		- applies to the block where the cursor is in, or on brace. "i" excludes the braces but "a" includes 

* Example 
	- aw: "a word" 
	- ip: "inner paragraph"
 
## Operation <a name='operation'></a> 

- Grammer rules
	1. [count]opt means repeats count times 
	2. doubling the operator on a line
	3. executed in ex mode with specific grammer 

* not individually used
* for some opts, ["x] ~ {motion} means {motion} text and store/take in the register x

1. useful before text object selection

| Commands | Feature | Action                                |
| d        | reg     | Delete text that {motion} moves over  |
| c        | i mode  | Delete {motion} text and start insert |
| y        | reg     | Yank {motion} text                    |
| g~       | none    | Switch case of {motion} text          |
| gU       | none    | Make {motion} text uppercase          |
| gu       | none    | Make {motion} text lowercase          |

* these are operations allowed to be used before text object selection
* also have diifferent syntax as other opts eg. dd, yy~

2. only direct to a cursor motion

| Commands | Action |
|

## Substitute command in ex mode <a name='substitution'></a>

1. change the chr in lines
``` some examples of basic s command in ex mode
# change the current line achr to bchr 
:s/achr/bchr/g

# change n line to the last line (the very first) achr to bchr
:n,$/achr/bchr/g

# change every line
:%s/achr/bchr/

# use # seperation but / as a chr
:s#achr/#bchr/#

# or we can also use +, the / serves as chr to s
:s+/achr//////+//bchr///+
```

2. some extra use

``` delete the quote
# delete all // quote
:%s!/s*//.*!!
# delete all /* */ quote
:%s!/s*//*/_./{-}/*//s*!!
```

to be continued ...

## Terminal in the nvim <a name='terminal'></a>

1. open a terminal in a window

```
:te
#or
:terminal
```

2. open a terminal (shell) on a vim tab

```
:e term://$SHELL
```

- In above, we use a special file name, just similiar to a HTTP link, but with the protol term: and the path SHELL which results in a default command SHELL.

- Now we can split our window as below.

```
# vertically split 
:vs term://$SHELL

# horizontally split
:split  term://$SHELL

# a new tab
:tabe term://$SHELL

```

3. change the mode of the terminal tab

- the same 'a' and 'i' into the insert mode
- in " :h :tw " help info we find how to go back to the normal mode:

```
<C-\><C-n>
```

With above, we can map our keys and use the terminal in nvim.

## regex for reading pattern.txt in help <a name='regex'></a>
