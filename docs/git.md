# Git CheatSheet

## SSH setup on Mac for Github / Bitbucket / Gitlab

- [Tutorial Video](https://www.youtube.com/watch?v=4nI0zHrOti4): Below instructions are for Github, but you can follow the same procedure for Bitbucket and Gitlab and multiple remote repos can be used within the same MacOS system.
- Generate the SSH Key pairs (private key `id_rsa` and public key `id_rsa.pub`)
  - [Optional]: remember to key in something, say 123, in **Enter passphrase** for the password

```shell
# option 1: using ed25519
ssh-keygen -t ed25519 -C "your_email@example.com"
# option 2: if you are using a legacy system that doesn't support the Ed25519 algorithm, use:
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- This creates a new SSH key, using the provided email as a label.

```shell
>>Generating public/private rsa key pair.
>>Enter file in which to save the key (/Users/quannguyen/.ssh/id_rsa): /Users/quannguyen/.ssh/id_rsa_github
```

- Modify the `config` file in the `.ssh` folder in the home directory & add the id_rsa_github into by using command:

```shell
vi ~/.ssh/config
# If the config does not exists, then using follow command to create: toch ~/.ssh/config
```

```Shell
# inside the ~/.ssh/config
Host *
  UseKeychain yes
  AddKeysToAgent yes

  # Github (default)
  IdentityFile ~/.ssh/id_rsa_github

  # Bitbucket (secondary)
  IdentityFile ~/.ssh/id_rsa_bitbucket
```

- Run `ssh-agent` in the background: everytime push and pull, it will remember the password and there is no need to type again and again.

```Shell
# run the ssh-agent in the background
eval $(ssh-agent -s)
# >> Agent pid 12988

# add github ssh private key to ssh agent &  store your passphrase in the keychain.
ssh-add --apple-use-keychain ~/.ssh/id_rsa_github

# [OPTIONAL] to view ids added into the SSH agent
ssh-add -l
3072 SHA256:xzLDvVc/glS1fRjST0SvLLzi41F9TtzyR9bl6QGSP5c quannguyen@Quans-MacBook-Pro.local (RSA)
3072 SHA256:SgQx28pEKNWmnTQ0UiGTkvNq0nJL2W5/j9ahYX4Q2b0 quannguyen@Quans-MacBook-Pro.local (RSA)
```

- Copy the public key and paste into Github account using `pbcopy < ~/.ssh/id_rsa_github.pub` command

## Remote Repo Management

<p align="center"><img  src="https://user-images.githubusercontent.com/64508435/175200336-a8520e15-3eb8-4d63-995f-c557cb319e7a.png" width="400"/></p>

### Adding a remote repository

- **origin**: the repo you clone to locally
- **upstream**: the repo you fork

```git
git remote add origin <link to remote cloned repo>
git remote add upstream <link to remote forked repo>
```

- Check the remote origin:

```shell
git remote -v
# origin  https://github.com/CodexploreRepo/jenkins.git (fetch)
# origin  https://github.com/CodexploreRepo/jenkins.git (push)
```

### Removing a remote repository

```git
git remote rm origin
```

## Branch

### Create a new branch

- `git branch <new-branch>`: to create a new branch locally
- `git checkout -b <new-branch>`: to create and checkout to the new branch`

### Merge a new branch

#### Merge on Remote Repo

- Need to create the Pull Request to merge into `Dev/Main` branch

#### Merge Locally

- In order to merge a branch to master/main

```git
//Working on the new branch: add > commit > push origin new-branch
git checkout master
git merge <new-branch>
```

### Delete Branch

- Need to switch to another branch before deleting current branch

```Git
git checkout <AnotherBrandName>
git branch -d <Branch-Name> // delete branch locally
git branch -D <Branch-Name> // brute-force delete the branch

// delete branch remotely
git push origin --delete BranchName
```

## Pull

- `pull` is to get the update from remote repo
  - `git pull origin branch_name` to get the latest update from that branch
  - `git checkout origin/branch_name path_to_file` to get the pull version a certain file only

## Fetch

- How to fetch a remote branch to local repos

```git
git fetch origin <branch-name>
git checkout <branch-name>

# also can combine the 2 commands
git fetch && git checkout <branch-name>
```

## Log

```git
git log
git log --oneline
git log --oneline --graph --decorate # display Git commit history

git diff <commitID1> <commitID2>     # show diff between two commits
```

## Rebase

### Merge multiple commits to a single one

- For example, merge commit from commit A to D, not include commit A

```git
git rebase -i A
# rebase commit A..D into E (3 commands)
# change from
pick B
pick C
pick D
# to
pick B
fixup C
fixup D
```

- Once rebased, you need to force `-f` push

```git
git push  -f origin branch_name
```

## Frequently Used Commands

- How to view the git log: `git log --oneline --graph --decorate`
- How to unstage files & removing the most recent `n` commit with `git reset`:
  - There are different modes of reset:
    - `--soft` **un-commit** changes, changes are left staged (index).
    - `--mixed` (default mode): **un-commit** + **un-stage** changes, changes are left in working tree.
    - `--hard` **un-commit** + **un-stage** + **delete** changes
  - Example 1 (default mode): `git reset HEAD~3`
    - This is `--mixed` mode meaning the current branch's HEAD pointer will be moved back `n=3` commits in history, un-doing the last 3 commits on the branch.
    - The changes from the un-done commits will be moved back to the staging area (**un-stage**), and the working directory will remain un-changed, allowing you to re-commit or modify them as needed.
- How to stop tracking a file in local repo:
  - `git rm *.csv --cached` stop tracking a file but still keep in the local repo
    - `cached` option removes the file from the index but keeps it in the working directory
    - From the above example, this is to remove all `.csv` file from being tracked by Git
  - `git rm *.csv` without `cached` option: will remove the file permanently
  - Once done, need to commit & push the changes to the remote repo
- How to compare file:
  - `git diff <commitID1> <commitID2>` show diff between two commits
  - `git diff file_name` view the change in the file
    [(Back to top)](#table-of-contents)
