## From SVN to GIT and Azure

The purpose is to switch from SVN to GIT as SCM and we use TFS as remote origin.  

Initially, the remote repo has been created.  

Here, the workflow to pass from SVN to GIT and push the code to Azure DevOps.   


1/ create a directory and checkout the solution (the trunk) from SVN into this directory.    

2/ Open a powershell command window and go to the directory with the code source

3/ Get the ID and name of the developers from the SVN log  (powershell command)
```powershell
svn.exe log --quiet | ? { $_ -notlike '-*' } | % { "{0} = {0} <{0}>" -f ($_ -split ' \| ')[1] } | Select-Object -Unique | Out-File -Encoding ASCII 'dev-list.txt'  
```

_Remark #1_: an alternative way to get the list is to use a command in the GIT bash console (with awk command):  
```bat
svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > dev-list.txt  
```

_#Remark #2_: beware about the output file encoding. We have to force the encoding to ASCII mode otherwise the powershell default encoding mode is not recognize by the git command.  

4/ Clone the svn repo by using the GIT command git svn clone :  
```bat
git svn clone https://srv-www-04.finaveo.local:8443/svn/upsideo/retro --prefix=svn/ --no-metadata --authors-file "dev-list.txt" --stdlayout E:\Retro-OUT-For-Git-WorkingDir  
```

5/ Go to the working directory (here E:\Retro-OUT-For-Git-WorkingDir)

6/ Add the remote branch  
```bat
git remote add origin https://tfs.upsideo.net/tfs/lmep/lmep/_git/lmep  
```

7/Get the remote branches  
```bat
git fetch  
```

8/ 
```bat
git pull origin UPSIDEV --allow-unrelated-histories  
```

9/ Load the code source from the branch origin UPSIDEV  
```bat
git checkout UPSIDEV  
```

10/ Merge the branch Master (this branch contains the SVN code) onto the origin UPSIDEV branch  
```bat
git merge master  
```

11/ Push the code to  
```bat
git push origin UPSIDEV 
```





```bat

mkdir E:\Retro-OUT-For-Git
mkdir E:\Retro-OUT-For-Git-WorkingDir
cd E:\Retro-OUT-For-Git


git svn clone https://srv-www-04.finaveo.local:8443/svn/upsideo/retro --prefix=svn/ --no-metadata --authors-file "dev-list.txt" --stdlayout E:\Retro-OUT-For-Git-WorkingDir  
cd E:\Retro-OUT-For-Git-WorkingDir
git remote add origin https://tfs.upsideo.net/tfs/lmep/lmep/_git/lmep
git fetch
git pull origin UPSIDEV --allow-unrelated-histories
git checkout UPSIDEV
git merge master
git push origin UPSIDEV
```





