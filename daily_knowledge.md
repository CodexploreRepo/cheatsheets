# Daily Knowledge

## Day 4

### Linux (Shell)

- Persist the environment variables in the terminal
  - If we set `export KUBECONFIG=~/.kube/config-prod` in the terminal, if we close it, the variable `KUBECONFIG` will be removed.
  - So in order to persist the environment variables, you can set inside the `.zshrc` if using zsh shell or `.bashrc` if using Bash shell.

```Shell
alias k=kubectl # you can set the alias
export KUBECONFIG=~/.kube/config-prod
```

## Day 3

### Git

- How to stop tracking a file but still keep in the local repo: `git rm *.csv --cached`

  - `cached` option removes the file from the index but keeps it in the working directory
  - From the above example, this is to remove all `.csv` file from being tracked by Git
  - `git rm *.csv` without `cached` option: will remove the file permanently
  - Once done, need to commit & push the changes to the remote repo

- Check the remote origin:

```shell
git remote -v
# origin  https://github.com/CodexploreRepo/jenkins.git (fetch)
# origin  https://github.com/CodexploreRepo/jenkins.git (push)
```

- Delete Branch
  - Need to switch to another branch before deleting current branch

```git
git checkout <AnotherBrandName>
git branch -d <Branch-Name> // delete branch locally
git branch -D <Branch-Name> // brute-force delete the branch

// delete branch remotely
git push origin --delete BranchName
```

- Merge multiple commits to a single one

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
  git push -f origin branch_name
  ```

- Modify commit message: `git commid --amend` and then update the commit message
  - Once done, you need to force `-f` push `git push -f origin branch_name`

## Day 2

### Linux (Shell)

- `echo $SHELL` to know which shell is using
  - `/bin/zsh` bash shell
  - `/bin/bash` zsh shell
- `source ~/.zshrc` reload changes of the file ` ~/.zshrc` in your current shell environment.

- **Login shell** is the first process that executes under your user ID when you log in for an interactive session.
  - Login shells typically read a file that does things like setting environment variables:
    - `/etc/profile` and `~/.profile` for the traditional Bourne shell
    - `~/.bash_profile` additionally for **Bash**
    - `/etc/zprofile` and `~/.zprofile` for **zsh**
- `$PATH` normally contains something when `~/.profile` is sourced (by default it contains `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games`)
  - Latest Mac OS versions the default shell is **zsh**, simply added new entries to the $PATH by editing ~/.zshrc the following way
    - `:$PATH` is put at the end of the value to be added to PATH, so that PATH ends up containing both the newly assigned path & existing paths where the newly assigned path will be put at first

```Shell
export PATH=/path/available/only/for/zsh/shells:$PATH

# /path/available/only/for/zsh/shells:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games`
```

#### Difference between `bashrc` and `bash_profile`

- This is also applicable for `zshrc` and `zprofile`

  | `bash_profile` (`zprofile`)                                                                                                             | `bashrc` (`zshrc`)                                                                                                                                            |
  | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | executed only once when you **log in to your account**                                                                                  | executed each time you open a new terminal window                                                                                                             |
  | changes will take effect only when you log out and log back in again.                                                                   | changes will take effect **immediately**                                                                                                                      |
  | set environment variables that are needed for entire session. This means that changes to bash_profile will affect all terminal windows. | customize your shell environment for each individual terminal window. This means that any changes you make to bashrc will affect only current terminal window |

## Day 1

### `scp` file transfer from one machine to another

- For example (transfer file from machine A to machine B):
  - Generate public & private key pairs, share the public key to Machine B, and Machine A will keep the private key
- `scp -i /location_in_machine_A/to/private/key -v -P 64022 file_path machineB@ip_address:/path/to/store/inB/`
  - `-i` Identity
  - `-v` verbose to debug
  - `-P` port (note P should be in captital letter)

### Curl

- `curl` is a command-line tool and library for transferring data with URLs.
- `curl -vvv telnet://hostname:port`
  - `-vvv`: This option increases the verbosity of curl output.
  - `telnet://hostname:port`: This part of the command specifies the URL to connect to. It tells `curl` to use the `Telnet` protocol to connect to the specified hostname and port.

### Telnet

Telnet is a network protocol and a command-line tool that allows you to remotely access and manage devices or systems over a network.

### Shell

- `ls -ltr`: This will display a detailed list of files and directories in the current directory, sorted by modification time, with the oldest entries listed first.
- `printenv` to print all the environment variables
- `echo $PATH` to print all the paths
- `unzip file.zip -d directory_path` to unzip a file
