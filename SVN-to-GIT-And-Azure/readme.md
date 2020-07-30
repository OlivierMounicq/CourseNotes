## From SVN to GIT and Azure

The purpose is to switch from SVN to GIT as SCM and we use TFS as remote origin.  

Initially, the remote repo has been created.  

Here, the workflow to pass from SVN to GIT and push the code to Azure DevOps.   

1/ Open a PowerShell window

2/ create two directories  
```bat
PS E:\> mkdir E:\Retro-OUT-For-Git
PS E:\> mkdir E:\Retro-OUT-For-Git-WorkingDir
```

3/ Checkout the SVN trunk    
```bat
PS E:\> svn checkout https://srv-www-04.finaveo.local:8443/svn/upsideo/retro/trunk E:\Retro-OUT-For-Git
```

4/ Go to the directory Retro-OUT-For-Git  
```bat
PS E:\> cd Retro-OUT-For-Git
```

5/ Get the ID and name of the developers from the SVN log  (powershell command)
```powershell
PS E:\Retro-OUT-For-Git> svn.exe log --quiet | ? { $_ -notlike '-*' } | % { "{0} = {0} <{0}>" -f ($_ -split ' \| ')[1] } | Select-Object -Unique | Out-File -Encoding ASCII 'dev-list.txt'  
```

_Remark #1_: an alternative way to get the list is to use a command in the GIT bash console (with awk command):  
```bat
$ svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > dev-list.txt  
```

_#Remark #2_: beware about the output file encoding. We have to force the encoding to ASCII mode otherwise the powershell default encoding mode is not recognize by the git command.  

6/ Clone the svn repo by using the GIT command git svn clone :  
```bat
PS E:\Retro-OUT-For-Git> git svn clone https://srv-www-04.finaveo.local:8443/svn/upsideo/retro --prefix=svn/ --no-metadata --authors-file "dev-list.txt" --stdlayout E:\Retro-OUT-For-Git-WorkingDir  
```

7/ Go to the working directory (here E:\Retro-OUT-For-Git-WorkingDir)
```bat
PS E:\Retro-OUT-For-Git> cd E:\Retro-OUT-For-Git-WorkingDir
```

8/ Add the remote branch  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git remote add origin https://tfs.upsideo.net/tfs/lmep/lmep/_git/lmep  
```

9/Get the remote branches  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git fetch  
```

10/ Pull the origin UPSIDEV branch
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git pull origin UPSIDEV --allow-unrelated-histories  
```

11/ Load the code source from the branch origin UPSIDEV  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git checkout UPSIDEV  
```

12/ Merge the branch Master (this branch contains the SVN code) onto the origin UPSIDEV branch  
```bat
PS E:\Retro-OUT-For-Git-WorkingDir> git merge master  
```

13/ Push the code to  
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
