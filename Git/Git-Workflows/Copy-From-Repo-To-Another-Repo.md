## From A repo to another one 

We want to copy source code from a GIT repo to another GIT repo  

```ps1
PS C:\> mkdir Temp  
PS C:\> cd Temp  
PS C:\Temp> git clone https://github.com/OlivierMounicq/GitRepo1.git
PS C:\Temp> cd GitRepo1
PS C:\Temp\GitRepo1> git remote add origin2 https://github.com/OlivierMounicq/GitRepo2.git
PS C:\Temp\GitRepo1> git pull origin2 master --allow-unrelated-histories
PS C:\Temp\GitRepo1> git push origin2 master
```




