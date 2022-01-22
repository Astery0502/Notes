# The internal of Git #

## Plumbing and Porcelain ##
With *git init* command, Git creates the *.git* directory which contains almost everything that Git stores and manipulates is located.

```
$ ls -F1
config 
description
HEAD
hooks/
info/
objects/
refs/
```

Among the directories and files:  
- The *config* file contains your project-specific configuration options.
- *HEAD* and *index* and *objects* and *refs* are core parts of Git:
    - object directory stores all the content for your database.
    - refs directory stores pointers into commit objects in that data (branches, tags, remotes and more).
    - HEAD file points to the branch you currently have checked out.
    - the index file is where Git stores your staging area information.

## Git Objects ##

After initialize a new Git repository.
```
$ git init repo
$ cd repo
$ find .git/objects
.git/objects
.git/objects/info
.git/objects/pack

$ find .git/objects -type f # find the objects created under .git
```

- git cat-file
```
git cat-file -p -t SHA-1_KEY
# -t only returns the type (blob, tree)
# -p instructs the command to figure out the type and return the content but the filename.

git cat-file -p master^{tree}
# returns the tree object that is pointed to by the last commit on your master branch
```

- git hash-object 

```
echo "expressions" > | git hash-object -w --stdin
# pipe the expression into a hash-object 
# --stdin tells the git get content to be processed from stdin
# -w option tells Git not simply return the key but write that object tothe database

git hash-object filename
```

- git update-index -- with the command above --git add  
the staging area wouldn't be cleared until the write-tree command is sent to Git. the same file path written in the staging area would be overwritten.
```
git update-index --add --cacheinfo 100644 \
SHA-1_KEY filename
# --add option means the file doesn't yet exist in the staging area
# --cacheinfo means the file you're adding isn't in your directory but it is in your database
# 100644 means a normal file; 100755 means an executed file; 12000 specifies a symbolic link
# SHA-1 with the mode are required for the --cacheinfo
```

- git write-tree -- to write the staging area out to a tree object
```
git write tree
git cat-file -p SHA-1_from_tree
```

- git commit-tree -- create a commit object from a tree with the message, author and date.
```
echo "First commit" | git commit-tree SHA-1_tree
# returns the SHA-1 key of the commit object
echo "Second commit" | git commit-tree SHA-1_tree -p last_commit
```

- *git add* and *git commit*: It stores blobs for the files that have changed, updates the index, write out trees, and writes commit objects that reference the top-level trees and the commits that came immediately before them.

- git log -stat SHA-1_commit -- only see the commits before referred to git commit-tree * commit_last

## Git References ##

In the .git/refs directory:
```
$ find .git/refs
.git/refs
.git/refs/heads
.git/refs/tags
```

- create a new reference to your commit:
```
echo SHA-1_commit > .git/refs/heads/branch_name(master)
git log --pretty=online master
# --pretty means the style of git log to display
```

- git update-ref -- basically how a branch is set
```
git update-ref refs/heads/master SHA-1_commit
git update-ref refs/heads/test SHA-1_commit2
```

When you run git branch, Git automatically runs that update-ref command to add SHA-1 of the last commit of the branch into whatever new reference you want to create.

### The HEAD ###

- git checkout branchname; cat .git/HEAD # look up the current HEAD

- git symboloc-ref HEAD
```
$ git symbolic-ref HEAD refs/heads/branchname
# set the value of HEAD using the same command
$ cat .git/HEAD
# can't point HEAD outof refs/
```

### Tags ###

The *tag* object is much like a commit object, but it points to a commit rather than a tree. It is like a branch reference, but it never moves.

- git update-ref -- make a lightweighted tag
```
git update-ref refs/tags/tagname SHA-1_commit
```

- git tag -a -- create an annotated tag: Git creates a tag object and then writes a reference to it rather than to the commit.
```
git tag -a tagname SHA-1_commit -m 'tag message'
cat .git/refs/tags/tagname
git cat-file -p SHA-1_tag
# the object points to the commit SHA-1 value that you tagged, and any other type of objects can also be tagged
```

### Remotes ###

Git stores the value you last pushed to that remote for each branch in the refs/remotes directory. 

```
$ git remote add orgin git@github.com:schacon/simplegit-progit.git
$ git push origin master
```

check the refs/remtoes/origin/master
```
$ cat .git/refs/remotes/origin/master
# returns the hash SHA-1 pointed to branches
```

remote references differ from branches mainly in they're considered read-only. You can switch to one, but Git won't symbolically reference HEAD to one, so you'll never update it with a commit command. Git manages them as bookmarks to the last known state of where those branches were on those servers.

