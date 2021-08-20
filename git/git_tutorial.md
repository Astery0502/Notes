# Make your own git #

[TOC]

## importing a new project ##

### 1. Start a git repository ###

Assume a new folder with files, place it under Git revision control as follows.

```bash
$ cd project 
$ git init
```

Git will reply

```
Initialized empty Git repository in .git/
```

> a new directory created named '.git'.

### 2. Store all as snapshot ###

Next, tell Git to take a snapshot of the contents of all files under the current directory (nore the .), with **git add**:

```
$ git add .
```

This snapshot is now stored in a temporary staging area which git calls the "index". You can permanently store the contents of the index inthe repository with **git commit**:

```
$ git commit
```

This will prompt you for a commit message. You've now stored the first version of your project in Git.

## Making changes ##

### 1. Add the modified ###

Modify some files, then add their updated contents to the index:

```
$git add file1 file2 file3
```

You are now ready to commit. You can see what is about to be committed using **git diff** with the --cached option:

### 2. read the diff and status ###
```
$ git diff --cached
 
```

( Without --cached, **git diff** will show you any changes that you've made but not yet added to the index.) You can also get a breif summary of the situation with **git status-s**:

``` " with command git status -s show the brief status
M file1
M file2
M file3
```

### 3. commit your change and messages ###

Make any further adjustments and **git add** add any newly modified content to index. Finally, commit your changes with:

```
$ git commit
```

This will again prompt you for a amessage describing the change, and then record a new version of the project.

Alternatively, instead of running **git add** beforehand, you can use

```
$ git commit -a
```

which will add any modified files to index and commit with one step.  

A note on commit messages: begin the commit message with a single short ( less than 50 character) line summarizing the change, fokkowed by a blank line and then a more thotough description. The text up to the first blank line in a commit message is treated as the commit title, and that title is used throughout Git.

### 4. viewing project history ###

You can view the history of your changes using

```
$ git log
```

Or you want a complete diffs at each step, use
```
$ git log -p
```

Often the overview of the change is uselful to get a feel of each step

```
git log -- stat --summury
```

### 5. Managing braches ###
 
A single Git repository can maintain multiple branches of development. To create a new branch named "experimental", use

```
$ git branch experimental
```
Now running
```
git branch
```

you will get a list of all existing branches:

```
  experimental
* master
```

The "master" branch is a default branch that was created for you automatically. The asterisk marks the branch you are currently one

* type

```
$ git switch experimental
```
to switch experimetntal branch. Now edit a file, commit the change, and switch back to the master branch:
```
(edit file)
$ git commit -a
$ git switch master
```

