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

And to get the content saved into the blob, we will use another plumbiong command : _git cat-file_ : 

```console
C:\GIT-1st-example> git cat-file -p f719
GIT : How it works ?
```
_Remark:_ you does not need to type all the hash code after _cat-file -p_, but only 4 characters (minimal quantity, but if several blob share the same 4 first characters, you have to type more character in order to identify the blob) 

Now, we will create a new directory named _src_ and we will add a new file named _helloworld.py_ :

```console
C:\GIT-1st-example> mkdir src 
C:\GIT-1st-example> cd src
C:\GIT-1st-example\src> notepad helloworld.py
```

And the file content is :

```py
#!/usr/bin/env python3

print("Hello World!")
```

Let check the update in the GIT object model : 

```console
C:\GIT-1st-example\src> cd ..
C:\GIT-1st-example> git add .
C:\GIT-1st-example\> git commit -m "2nd commit : add the python file"
C:\GIT-1st-example> cd .git
C:\GIT-1st-example\.git> tree /f 
```

And we can see that some objects have been added in the _objects_ subdirectory:

```console
Folder PATH listing for volume Windows
Volume serial number is 7E3E-9A68
C:.
│   COMMIT_EDITMSG
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
├───logs
│   │   HEAD
│   │
│   └───refs
│       └───heads
│               master
│
├───objects
│   ├───42
│   │       55c42db81d12a8824cd3c64862bdb1404faa04
│   │
│   ├───9f
│   │       0c98d2a3e28f6e982067535699136a573385a9
│   │
│   ├───bc
│   │       a043fe83ede3a8d5385e723dccec4b74dd15c6
│   │
│   ├───df
│   │       311d344734adc6e7cbea60c3e31987f855a9fe
│   │
│   ├───f7
│   │       19f6ba8069fff67026125d461f28f9424caed7
│   │
│   ├───info
│   └───pack
└───refs
    ├───heads
    │       master
    │
    └───tags
```

Let start by the root object. For do that, we will use the second commit : 

```command
C:\GIT-1st-example> git log
```

```command
commit 4255c42db81d12a8824cd3c64862bdb1404faa04 (HEAD -> master)
Author: Olivier Mounicq <mounicq@gmail.com>
Date:   Thu Jul 30 23:56:44 2020 +0200

    2nd commit : add the python file
```

The commit had a related hash code : _4255c42db81d12a8824cd3c64862bdb1404faa04_ . Let discover what this blob contains :

```command
C:\GIT-1st-example> git cat-file -p 4255
```
So this blob is a _commit_ and it contains a tree _bca043fe83ede3a8d5385e723dccec4b74dd15c6_

```command
tree bca043fe83ede3a8d5385e723dccec4b74dd15c6
author Olivier Mounicq <mounicq@gmail.com> 1596146204 +0200
committer Olivier Mounicq <mounicq@gmail.com> 1596146204 +0200

2nd commit : add the python file
```

Let's check what contains this tree ! 

```command
C:\GIT-1st-example> git cat-file -p bca0
```

Well , there are our first file _readme.md_ and also the _src_ directory.

```command
100644 blob f719f6ba8069fff67026125d461f28f9424caed7    readme.md
040000 tree df311d344734adc6e7cbea60c3e31987f855a9fe    src
```

Let's verify the content of the blob:

```command
C:\GIT-1st-example> git cat-file -p f719
```

And it's our first file without doubt:

```command
GIT : How it works ?
```

Ok. Let's dig the branch of the tree! 

```command
C:\GIT-1st-example> git cat-file -p df31
```

And we get that:

```command
100644 blob 9f0c98d2a3e28f6e982067535699136a573385a9    helloworld.py
```


And finally, we have the python file:

```command
C:\GIT-1st-example> git cat-file -p 9f0c
```

```command
#!/usr/bin/env python3

print("Hello World!")
```

### 5/ File updating and GIT object model

Add update the first line in the _readme.md_ file : ```# GIT : How it works ?```

