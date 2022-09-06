# Git Command Cheat Sheet

# SSH
- Generate the SSH Key pairs (private key `id_rsa` and public key `id_rsa.pub`)
  - Note: remember to key in something, say 123, in **Enter passphrase** 

```shell
ssh-keygen

>>Generating public/private rsa key pair.
>>Enter file in which to save the key (/Users/quannguyen/.ssh/id_rsa): /Users/quannguyen/.ssh/id_rsa_github
```
- Modify the `config` file in the `.ssh` folder in the home directory & add the id_rsa_github into 

```Shell
vi ~/.ssh/config

Host *
  UseKeychain yes
  AddKeysToAgent yes

#Github (default)
  IdentityFile ~/.ssh/id_rsa_github
```
- Run `ssh-agent` in the background: everytime push and pull, it will remember the password and there is no need to type again and again.
```Shell
eval $(ssh-agent -s)
>> Agent pid 12988

# add github ssh private key to ssh agent
ssh-add --apple-use-keychain ~/.ssh/id_rsa_github

# [OPTIONAL] to view ids added into the SSH agent
ssh-add -l
3072 SHA256:xzLDvVc/glS1fRjST0SvLLzi41F9TtzyR9bl6QGSP5c quannguyen@Quans-MacBook-Pro.local (RSA)
3072 SHA256:SgQx28pEKNWmnTQ0UiGTkvNq0nJL2W5/j9ahYX4Q2b0 quannguyen@Quans-MacBook-Pro.local (RSA)
```
- Copy the public key and paste into Github account using `pbcopy < ~/.ssh/id_rsa_github.pub` command


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
# Pull
- `pull` is to get the update from remote repo
  - `git pull origin branch_name` to get the latest update from that branch 
  - `git checkout origin/branch_name path_to_file` to get the pull version a certain file only 


# Fetch 
- How to fetch a remote branch to local repos
```git
git fetch origin <branch-name>
git checkout <branch-name>

# also can combine the 2 commands
git fetch && git checkout <branch-name>
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
