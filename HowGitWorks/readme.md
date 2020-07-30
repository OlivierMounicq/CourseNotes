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





















```cmd
>mkdir GitExmple
>cd GitExample
>git init
>cd .git
```

```console
>tree /f
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
