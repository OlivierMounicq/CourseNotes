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

```console
C:\> mkdir GIT-1st-example 
C:\> cd  GIT-1st-example
C:\GIT-1st-example> git init
C:\> cd .git
C:\> tree /f 
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
