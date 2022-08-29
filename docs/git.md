# Git Command Cheat Sheet

# Table of contents

- [Table of contents](#table-of-contents)
- [Remote Repo Management](#remote-repo-management)
- [Branch](#branch)
- [Pull](#pull)
- [Utils](#utils)
  - [Adding Access Token](#adding-access-token) 

# Remote Repo Management
<p align="center"><img  src="https://user-images.githubusercontent.com/64508435/175200336-a8520e15-3eb8-4d63-995f-c557cb319e7a.png" width="400"/></p>

## Adding a remote repository
- **origin**: the repo you clone to locally
- **upstream**: the repo you fork
```git
git remote add origin <link to remote cloned repo>
git remote add upstream <link to remote forked repo>
```
## Removing a remote repository
```git
git remote rm origin 
```

# Branch
## Create a new branch
- `git branch <new-branch>`: to create a new branch locally
- `git checkout -b <new-branch>`: to create and checkout to the new branch`

# Pull
- `pull` is to get the update from remote repo
  - `git pull origin branch_name` to get the latest update from that branch 
  - `git checkout origin/branch_name path_to_file` to get the pull version a certain file only 


# Fetch a remote branch locally
```git
git fetch origin <branch-name>
git checkout <branch-name>

# also can combine the 2 commands
git fetch && git checkout <branch-name>
```

## Merge a new branch
### Merge on Remote Repo
- Need to create the Pull Request to merge into `Dev/Main` branch
### Merge Locally
- In order to merge a branch to master/main
```git
//Working on the new branch: add > commit > push origin new-branch
git checkout master
git merge <new-branch>
```
## Delete Branch
- Need to switch to another branch before deleting current branch
```Git
git checkout <AnotherBrandName>
git branch -d <Branch-Name> // delete branch locally
git branch -D <Branch-Name> // brute-force delete the branch

// delete branch remotely
git push origin --delete BranchName
```
# Utils

## Adding Access Token
<img width="723" alt="Screenshot 2022-01-02 at 16 10 29" src="https://user-images.githubusercontent.com/64508435/147871336-273983a6-e74f-4acf-a227-40a0540bb280.png">
Link: https://github.com/settings/tokens 

If you're using MacOS, just simply follow these steps:

- Goto: this link (settings -> developers setting -> personal access tokens).
- Generate a new token (Need to select the permission) and copy-paste it somewhere safely.
- Now search for an App in your Mac, named Keychain Access.
- Search for github.com (if there are multiple github logins then choose Kind: Internet password), double-click it.
- Click on show password, then enter your mac's password and hit enter.
- Password should be visible by now. Now, just paste the token you generated in step 2 and click Save changes.

[(Back to top)](#table-of-contents)
