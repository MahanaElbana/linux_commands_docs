
<h1 align="center"> GitHub Commands && How tos && Problems </h1>


<p align="center">
<code><img height="200" src="../pictures/github.png" /></code>
</p>

## What is Git and Github 🧐 ?

 - 💙 GIT is Distributed Version Control System
 - 💙 Git is Free and open source

# All git commands of github ordered 🔥 

## 👍 conclusion for git commands 👍

* ### For downloading project from github 🔦

``` Shell
git clone "url to github project" 
```

* ### To see your state after editing on files 🔦

``` Shell
git status 
```

***

* ### Stages of moving files from your device to remote repo 🔦

``` shell
working directory
   git add *  or git add .
     git add 'name of file' 'name of another file '
        staging area
            git commit -am "description"
                local repo
                   git push
                        remote repo 
```

***

* ### For removing files from staging area 🔦

```shell
git reset -- 'name of file' ,'name of another file '
```

***

* ### For loading files to local repo 🔦

``` shell
git commit -am "description"
          or 
git commit -m "description"
```

***

* ### To know any branch 🔦

```sheel
git branch
```

***

* ### To know any remoteRepo 🔦

```sheel
git remote -v
```

***

* # how to move your files from  *staging area* (git add) to working directory 🔦

```
git restore --staged *
```

* ### To load files to remote Repo 🔦

```sheel
git push 'remote name' 'branch name' 
git push origin main
```  

* ### how To add Contributors from github  🔦

```sheel
     from settings
         options 
             Manage access
                invite a collaborator
```  

***

* ### how To pull updating files from Remote Repo 🔦

 ```shell

 1] git fetch origin main
 2] git merge

 ```

***

* ### how To pull updating files from Remote Repo in one line command 🔦

``` shell
git pull origin main
````

***

* ### Stages of moving files from remote Repo to your device 🔦

``` shell
remote repo 
     git fetch
        local repo
            git stash save "description"
                staging area
                     git merge
                        working directory
```

***

* ### If you want to erase a file from working directory  ⬇️

```shell
 git  rm  file_name.extention
```

***

* ### To erase a file from both the working directory remote Repo ⬇️

```shell
 1] git rm "file name"
 2] git commit "description"
 3] git push "remote repo name" "branch name"
```

***

* ### If you erased a file from working directory and you want erase it from remote Repo ⬇️

```shell
 1] git add/rm "file name"
 2] git commit "description"
 3] git push "remote repo name" "branch name"
```

***

* ### If you erased a file from working directory by mistake and want to retrieve it ⬇️

```shell
 git restore file_name.extention
```

***

* ### To go back from stage area to working directory ⬇️

```shell
git restore --staged file_name.extension
```

***

* ### To show configuration list ⬇️

```shell
 git config -l
```

***

* ### To show your username and email respectively ⬇️

```shell
git config --global user.email 
git config --global user.name
```

***

* ### To edit your username and email respectively ⬇️

```shell
git config --global user.email "email"
git config --global user.name   "name"
```

***

* ### To edit your username and email respectively another method ⬇️

```shell
git config --global --edit
```

#### example on this method :- updating by using file (.gitconfig) 👍

```txt
[user]
        email = person@example.com
        name = person_name
[color "status"]
        added =blue
        changed = red bold
        untracked = green
[color "branch"]
        remote = magenta
```

***

* ### To show configration list which related to orgin ⬇️

```shell
git config -l --show origin
```

***

* ### To generate ssh key ⬇️

```shell
To generate key :-
   1] ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   2] add password 
To get key :-  
   1] cat /home/name_your_device/.ssh/id_rsa
To add key in github :- 
    from settings 
        SSH and GPG keys
           and the add SSH keys
To test your key :- 
    1] using command :-
         ssh -T git@github.com
         and then add password               
```

***

* ### To load exist project to github ⬇️

```shell
    1] from folder of your project :- 
       git init 
    2] go to github and create repo .
    3] choose ssh from page which appears after creating Repo 
    and then :- write the following commands :- 
      1] git branch -M main
      2] git remote add origin git@github.com:cbmbbmj/nene.git
      3] git add *
      4] git commit -m "description"
      5] git push -u origin main
``` 

***

* ### To add nickname for certain command ⬇️

```shell
    git config --global alias.nickname  command 

    EX:- 
      git config --global alias.br branch
        so we can get the branch by the following two commands :- 
          git br 
          git branch
    Another EX:- 
      git config --global alias.cm "commit -m"
        so we can get the branch by the following two commands :- 
          git cm "descrition"
          git commit -m "description" 

   if open .gitconfig :- from the command ==>  git config --global --edit :- 
    .gitconfig
      [user]
        email = email@gmail.com
        name = your name 
      [color "status"]
        added =blue
        changed = red bold
        untracked = green
      [color "branch"]
        remote = magenta
      [alias]
        br = branch
        cm = commit  -m
        st = status

``` 

* ### How to define and use aliases ⬇️

```urls
1] https://opensource.com/article/20/11/git-aliases
2] https://snyk.io/blog/10-git-aliases-for-faster-and-productive-git-workflow/
```

***

* ### To create a new branch ⬇️

```shell
  git branch branch_name
```

* ###  To switch to branch (move to another branch) ⬇️ 

```shell
   git checkout branch_name
```   

* ### To Delete the specified branch. ⬇️

```shell
  git branch -d branch_name
```

* ### To force delete the specified branch ⬇️ 

```shell
  git branch -D branch_name 
```

* ### to create branch and switch ⬇️ 

```shell
  git checkout -b branch_name
```  

* ### To rename the current branch ⬇️ 

```shell
  git branch -m branch_name 
```  

* ### To merge the current branch  to main branch ⬇️  

```shell
    go to main ==>           git checkout main 
    merge branch to main =>  git merge branch_name
```  

* ### To load  the current branch  to main branch ⬇️

```shell
git push origin name_branch   
   ==> make a pull request
``` 
   
***

# How to push on specific branch :
```
git push RemoteName RemoteBranch
git push origin main 
```

# How to make a clone to private repo 
```bash
git clone https://cbmbbmj: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@github.com/MahanaElbana/plt_2.git

https://userName:Your_classic_Token@github.com/UserName/RepoName 
```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