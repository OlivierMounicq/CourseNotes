## GIT : How it works

### 1/ Porcelain commands & plumbing commands

The porcelain commands:  
- git add  
- git pull  
- git commit  
- ..  

The plumbing command:  
- git cat-file  
- git hash-object  
- git count-objects  

### 2/ GIT definition  

GIT = Distributed Revision Control System  

GIT =  Persistent Map + Content Tracker + Revision Control System + Distributed Revision Control System  

### 3/ Git objects

The GIT object types:  
- Blob    
- Tree  
- Commit  
- Annoted Tag  

### 4/ First example

We will create a new directory to manipulate the GIT object model. We have to initialize this local repository.

```console
C:\> mkdir GIT-1st-example 
C:\> cd  GIT-1st-example
C:\GIT-1st-example> git init
C:\GIT-1st-example\.git> cd .git
C:\GIT-1st-example\.git> tree /f 
```

We can see the GIT object model:

```console
C:.
│   config
│   description
│   HEAD
│
├───hooks
│       applypatch-msg.sample
│       commit-msg.sample
│       fsmonitor-watchman.sample
│       post-update.sample
│       pre-applypatch.sample
│       pre-commit.sample
│       pre-merge-commit.sample
│       pre-push.sample
│       pre-rebase.sample
│       pre-receive.sample
│       prepare-commit-msg.sample
│       update.sample
│
├───info
│       exclude
│
├───objects
│   ├───info
│   └───pack
└───refs
    ├───heads
    └───tags
```

Now we add a new text file in the directory  

```console
C:\GIT-1st-example\.git> cd..
C:\GIT-1st-example> notepad readme.md
```

And we add this content into the file : "GIT : How it works ?" (save and close notepad)  
And we can notify that GIT has detected a new file :

```console
C:\GIT-1st-example>git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        readme.md

nothing added to commit but untracked files present (use "git add" to track)
```

But nothing has been adding in the object model :

```console 
C:\GIT-1st-example\> cd .git
C:\GIT-1st-example\.git> tree /f
```

```console
Folder PATH listing for volume Windows
Volume serial number is 7E3E-9A68
C:.
│   config
│   description
│   HEAD
│
├───hooks
│       applypatch-msg.sample
│       commit-msg.sample
│       fsmonitor-watchman.sample
│       post-update.sample
│       pre-applypatch.sample
│       pre-commit.sample
│       pre-merge-commit.sample
│       pre-push.sample
│       pre-rebase.sample
│       pre-receive.sample
│       prepare-commit-msg.sample
│       update.sample
│
├───info
│       exclude
│
├───objects
│   ├───info
│   └───pack
└───refs
    ├───heads
    └───tags
```

And we will add this file. There are different ways : either by naming the file _git add readme.md_ or by doing a adding group _git add ._ (git add _dot_)

```console
C:\GIT-1st-example\.git> cd..
C:\GIT-1st-example> git add .
```

And the status has changed:

```console 
C:\GIT-1st-example> git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   readme.md
```

And the object model has been updated too. New objects have been added in _objects_ directory: 

```console
C:\GIT-1st-example> cd .git
C:\GIT-1st-example\.git> tree /f
```
   
```console
Folder PATH listing for volume Windows
Volume serial number is 7E3E-9A68
C:.
│   config
│   description
│   HEAD
│   index
│
├───hooks
│       applypatch-msg.sample
│       commit-msg.sample
│       fsmonitor-watchman.sample
│       post-update.sample
│       pre-applypatch.sample
│       pre-commit.sample
│       pre-merge-commit.sample
│       pre-push.sample
│       pre-rebase.sample
│       pre-receive.sample
│       prepare-commit-msg.sample
│       update.sample
│
├───info
│       exclude
│
├───objects
│   ├───f7
│   │       19f6ba8069fff67026125d461f28f9424caed7
│   │
│   ├───info
│   └───pack
└───refs
    ├───heads
    └───tags
```
       
An object is pair of key-value and the key is the hash of the file. The nade of the node (it's a blob) _f7/19f6ba8069fff67026125d461f28f9424caed7_ is the hash of the file _readme.md_  

Let get the hash code of the _readme.txt_ file. And we use a plumbing command:

```console 
C:\GIT-1st-example\.git> cd..
C:\GIT-1st-example> git hash-oject readme.txt
f719f6ba8069fff67026125d461f28f9424caed7
```


