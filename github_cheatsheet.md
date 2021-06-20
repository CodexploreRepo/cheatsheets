## Branch
### Create a new branch

```git
//To list all existing branches in a repository
git branch

//<--Create a new branch-->
git branch new-branch

//<--Switch to new-branch-->
git checkout new-branch

//Working on the new branch: add > commit > push origin new-branch
//<--Merge to Master Branch-->
git checkout master

git merge new-branch

//<--Merge Pull Request in Github-->
```
### Delete Branch
```Git
// [Optional] Need to switch to another branch before deleting current branch
git checkout AnotherBrandName
// delete branch locally
git branch -d BranchName

// delete branch remotely
git push origin --delete BranchName
```
