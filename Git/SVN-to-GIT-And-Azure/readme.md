## From SVN to GIT and Azure

The purpose is to switch from SVN to GIT as SCM and we use TFS as remote origin.  

Initially, the remote repo has been created.  

Here, the workflow to pass from SVN to GIT and push the code to Azure DevOps.   

__1/__ Open a PowerShell window

__2/__ create two directories  
```bat
PS E:\> mkdir E:\Retro-OUT-For-Git
PS E:\> mkdir E:\Retro-OUT-For-Git-WorkingDir
```

__3/__ Checkout the SVN trunk    
```bat
PS E:\> svn checkout https://srv-www-04.finaveo.local:8443/svn/upsideo/retro/trunk E:\Retro-OUT-For-Git
```

__4/__ Go to the directory Retro-OUT-For-Git  
```bat
PS E:\> cd Retro-OUT-For-Git
```

__5/__ Get the ID and name of the developers from the SVN log  (powershell command)
```powershell
PS E:\Retro-OUT-For-Git> svn.exe log --quiet | ? { $_ -notlike '-*' } | % { "{0} = {0} <{0}>" -f ($_ -split ' \| ')[1] } | Select-Object -Unique | Out-File -Encoding ASCII 'dev-list.txt'  
```

_Remark #1_: an alternative way to get the list is to use a command in the GIT bash console (with awk command):  
```bat
$ svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > dev-list.txt  
```

_Remark #2_: beware about the output file encoding. We have to force the encoding to ASCII mode otherwise the powershell default encoding mode is not recognize by the git command.  

__6/__ Clone the svn repo by using the GIT command git svn clone :  
```bat
PS E:\Retro-OUT-For-Git> git svn clone https://srv-www-04.finaveo.local:8443/svn/upsideo/retro --prefix=svn/ --no-metadata --authors-file "dev-list.txt" --stdlayout E:\Retro-OUT-For-Git-WorkingDir  
```

_Remark:_ : maybe you want to export to GIT a specific branch, so in this case, you must add the option -T branches/_<myBranch>_
```bat
PS E:\Retro-OUT-For-Git>  git svn clone -T branches/UpsideoRetro  https://srv-www-04.finaveo.local:8443/svn/upsideo/retro --prefix=svn/ --no-metadata --authors-file "dev-list.txt" --stdlayout E:\Retro-IN-For-Git-WorkingDir
```


__7/__ Go to the working directory (here E:\Retro-OUT-For-Git-WorkingDir)
```bat
PS E:\Retro-OUT-For-Git> cd E:\Retro-OUT-For-Git-WorkingDir
```

__8/__ Add the remote branch  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git remote add origin https://tfs.upsideo.net/tfs/lmep/lmep/_git/lmep  
```

__9/__ Get the remote branches  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git fetch  
```

__10/__ Pull the origin UPSIDEV branch
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git pull origin UPSIDEV --allow-unrelated-histories  
```

__11/__ Load the code source from the branch origin UPSIDEV  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git checkout UPSIDEV  
```

__12/__ Merge the branch Master (this branch contains the SVN code) onto the origin UPSIDEV branch  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git merge master  
```

__13/__ Push the code to  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git push origin UPSIDEV 
```

All the steps of the workflow

```bat
PS E:\> mkdir E:\Retro-OUT-For-Git
PS E:\> mkdir E:\Retro-OUT-For-Git-WorkingDir
PS E:\> svn checkout https://srv-www-04.finaveo.local:8443/svn/upsideo/retro/trunk E:\Retro-OUT-For-Git
PS E:\> cd E:\Retro-OUT-For-Git
PS E:\Retro-OUT-For-Git> git svn clone https://srv-www-04.finaveo.local:8443/svn/upsideo/retro --prefix=svn/ --no-metadata --authors-file "dev-list.txt" --stdlayout E:\Retro-OUT-For-Git-WorkingDir  
PS E:\Retro-OUT-For-Git> cd E:\Retro-OUT-For-Git-WorkingDir
PS E:\Retro-OUT-For-Git-WorkingDir> git remote add origin https://tfs.upsideo.net/tfs/lmep/lmep/_git/lmep
PS E:\Retro-OUT-For-Git-WorkingDir> git fetch
PS E:\Retro-OUT-For-Git-WorkingDir> git pull origin UPSIDEV --allow-unrelated-histories
PS E:\Retro-OUT-For-Git-WorkingDir> git checkout UPSIDEV
PS E:\Retro-OUT-For-Git-WorkingDir> git merge master
PS E:\Retro-OUT-For-Git-WorkingDir> git push origin UPSIDEV
```



### Links

[Learn how to migrate from Subversion (SVN) to Git, including history](https://docs.microsoft.com/en-us/azure/devops/repos/git/perform-migration-from-svn-to-git?view=azure-devops)  
[HOW EASY IT’S TO MIGRATE SVN TO TFS 2013 ](https://blogs.incyclesoftware.com/2013/08/how-easy-its-to-migrate-svn-to-tfs-2013-git-repo/)  
