# Daily Knowledge

## Day 3

### Git

- Check the remote origin:

```shell
git remote -v
# origin  https://github.com/CodexploreRepo/jenkins.git (fetch)
# origin  https://github.com/CodexploreRepo/jenkins.git (push)
```

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
