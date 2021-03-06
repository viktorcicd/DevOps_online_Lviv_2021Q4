## Module 1 DevOps Introduction

### TASK 1.1


Create and configure a local git repository

![conf](./images/conf.png "config")

Create and configured a Github repository

![github](./images/github.png "github")


Create branches and provide manipulations according to the task

```
git clone git@github.com:viktorcicd/DevOps_online_Lviv_2021Q4.git

```
Following commands were used during the process
```
git add .
git commit -m "init commit"
git checkout -b develop
git checkout -b images
git checkout -b styles
```
 ![branch](./images/branch.png "branch")
 
 ![folders](./images/folders.png "folders")
 
```
 git add .
 git status
 git commit -m "add styles"
 git checkout develop
 git branch
 git merge images
 git merge styles
 nano index.html
 git add index.html
 git status
 git commit -m "merge manually fixed"
 git checkout master
 git merge develop
 git log
 git log -p
 git log -p --all
 
 ```
![merge](./images/merge.png "merge")

![reflog](./images/reflog.png "reflog")

![reflog](./images/branches.png "reflog")
 
 DevOps is a metodology that solves the issues in cooperation between development and operation/production teams. In other words Devops specialists have to understand, implement  processes of the development and operation cycle.
 
