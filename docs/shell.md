# Shell

## What is the shell?

- Computers these days have a variety of interfaces for giving them commands; fanciful graphical user interfaces, voice interfaces, and even AR/VR are everywhere. These are great for 80% of use-cases, but they are often fundamentally restricted in what they allow you to do — you cannot press a button that isn’t there or give a voice command that hasn’t been programmed. To take full advantage of the tools your computer provides, we have to go old-school and drop down to a textual interface: The Shell.
- In this lecture, we will focus on the **Bourne Again SHell**, or “**bash**” for short. This is one of the most widely used shells, and its syntax is similar to what you will see in many other shells. To open a shell prompt (where you can type commands), you first need a terminal. Your device probably shipped with one installed, or you can install one fairly easily.

## Terminal vs Shell

- **Terminal**: Text Input Environment (“Hardware Terminal”) or a program wraps around the Shell
- **Shell** (Bash or zSH): Text Input Interface (”Software”)
  - `BASH`: default MacOS/Linux terminal uses
  - `zSH`: good to use for local development with taking from (BASH + Improvemnts).
  <p align="center">
  <img width="550" alt="image" src="https://user-images.githubusercontent.com/64508435/188552799-5e37a32d-5a35-44e7-93a4-7a25a667c88f.png">
  </p>

```shell
# Open the terminal of Mac, by default,
echo $SHELL
>> /bin/bash
>> /bin/zsh
```

### Install zSH for Mac

- **Step 1**: Install [iTerm](https://iterm2.com/)
- **Step 2**: Install zSH via homebrew command `brew install zsh`
- **Step 3**: Open iTerm terminal and change it to zSH instead of BASH via command `chsh -s /bin/zsh`
- **Step 4**: Install [Oh My ZSH](https://github.com/ohmyzsh/ohmyzsh/), a framework to manage zSH configuration, via curl command

```Shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

- **Step 4.1**: add `code` for VS Code by running below command. [Reference Link](https://code.visualstudio.com/docs/setup/mac)
  ```Shell
  cat << EOF >> ~/.zshrc
  # Add Visual Studio Code (code)
  export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
  EOF
  ```
- **Step 4.2**: Set zSH as default terminal of VSCode
  - Go to Preference &#8594; Settings &#8594; search for Terminal &#8594; and select zSH as default interated Terminal for OSX as shown in below picture
  <p align="center">
  <img width="800" alt="Screenshot 2022-09-06 at 14 17 38" src="https://user-images.githubusercontent.com/64508435/188560568-1d37b5ae-e322-4248-8fce-6c986401e8c9.png"></p>

## Shell Command

### Environment Variable `$PATH`

- **Environment Variable** `$PATH`: lists which directories the shell should search for programs when it is given a command

  - When we run the echo command, the shell sees that it should execute the program `echo`, and then searches through the **:**-separated list of directories in $PATH for a file by that name. When it finds it, it runs it (assuming the file is executable; more on that later).
    - For example, when type `echo`, the shell will search and find the `echo` executable in the directory `/bin`

  ```shell
  home:~$ echo $PATH
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

  home:~$ which echo
  /bin/echo

  home:~$ /bin/echo $PATH
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  ```

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

### Using the shell

| Command           | Description                                                                                                                                                                                                                                                                                     |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `echo`            | A program simply prints out its arguments. <br>- If you want to provide an argument that contains spaces or other special characters (e.g., a directory named "My Photos"), you can either quote the argument with `'` or `"` , or escape just the relevant characters with `\` (`My\ Photos`). |
| `man <some_cmd>`  | To check the document of the shell command, say `man rm` to read the doc of remove command                                                                                                                                                                                                      |
| `source ~/.zshrc` | reload changes in your current shell environment.                                                                                                                                                                                                                                               |
| `which`           | To find out which file is executed for a given program name                                                                                                                                                                                                                                     |
| `whoami`          | To check which user is logged in                                                                                                                                                                                                                                                                |
| `$()`             | The `$()` syntax sends the output from one command into another command <br> For example: `docker container rm --force $(docker container ls --all --quiet)` is to send the output from the command `docker container ls --all --quiet` to the next command `docker container rm --force`       |

### Navigating in the shell

| Command | Description                                                                                                                       |
| ------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `.`     | refers to your current directory                                                                                                  |
| `..`    | refers to the parent of your current directory                                                                                    |
| `~`     | `~`: the tilda slash refers to your home directory <br> so for example `~/.bashrc` refer to `.bashrc` is a file in home directory |
| `-`     | previous path <br>`cd -` to change directory to previous path                                                                     |
| `pwd`   | get the path of current working directory                                                                                         |
| `ls`    | print the contents of the current directory                                                                                       |

- `ls -l`: This gives us a bunch more information about each file or directory present.
- `ls -ltr`: This will display a detailed list of files and directories in the current directory, sorted by modification time, with the oldest entries listed first.
- On Linux servers, the server needs to know two things about files:
  - What can be done to a file: read (r), write (w), execute (x).
  - Who can do it

```Shell
home:~$ ls -l /home
drwxr-xr-x 1 ubuntu  users  4096 Jun 15  2019 missing
```

- First, the d at the beginning of the line tells us that missing is a directory.
- Then follow three groups of three characters (rwx). These indicate what permissions the owner of the file (ubuntu)
- (xr) the owning group (users)
- (x) public (“everyone else”)

### Frequent Commands

| Command                               | Description                                                                                                                                                   |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `mv <src_path> <dst_path>`            | Move/rename the file<br>`mv foo.md dotfiles.md` to rename the "foo" to "dotfiles" file <br> -f Attempt to remove the files without prompting for confirmation |
| `cp <src_path> <dst_path>`            | Copy the file                                                                                                                                                 |
| `rm [flags] [file/folder name]`       | -r: recursively delete a non-empty directory and all of its contents                                                                                          |
|                                       |                                                                                                                                                               |
| `tar zxvf sentences.tgz -C sentences` | unzip file **sentences.tgz** into **sentences** folder                                                                                                        |
| `> /dev/null`                         | `/dev/null` is the null file, a special file that’s present in every single Linux system. <br>`> /dev/null` anything written to it is discarded.              |

#### Read/Write a File

| Command              | Description                                                                                                                                                                       |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cat file.txt`       | **cat** a program that is use to display the content of a file                                                                                                                    |
| `head file.txt`      | to view the first few lines of a file                                                                                                                                             |
| `tail file.txt`      | to view the last few lines of a file                                                                                                                                              |
| `touch new_file.txt` | **touch** command is for creating a file                                                                                                                                          |
| `nano file.txt`      | **nano** is a text editor                                                                                                                                                         |
| `vi file.txt`        | Open the file using VIM editor                                                                                                                                                    |
|                      |                                                                                                                                                                                   |
| `tee`                | Copy the standard input to standard output/ to a file <br>Flag `-a` append the output to the files rather than overwriting them. <br> See `tee` example in the below code snippet |

- `tee` example
  - `echo $'\n127.0.0.1 registry.local'` is to print the string `'\n127.0.0.1 registry.local'` to the standard input
  - `tee` to append that string into the `hosts` file at `/etc` location

```Shell
echo $'\n127.0.0.1 registry.local' | sudo tee -a /etc/hosts`
```

#### `mkdir`

- `-p` to ensure that if the parent folder is not made yet, the command will also create the parent folder
  - `mkdir -p /repos/new_folder` make the repos folder as well if it is not created yet

#### `cat`

- Create a File with `cat` command

```bash
cat > example.txt
# a file `example.txt` is created and awaiting input from the user, type desired text, and press CTRL+D to exit

ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
deepak clerk sales 23000
sunil peon sales 13000
```

#### `grep`

- search the string inside your file via `grep "regex"`
- `cat query.sql | grep "order"`
- `-e` grep with a pattern
  - For example: `grep -e 'inet\s'` to grep with pattern **inet** follow by a space

#### `awk`

- `awk`: format output lines
- By default, `awk` prints every line of data from the specified file

```bash
$ awk '{print}' employee.txt

# Output
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
```

- Print the lines which match the given pattern.

```bash
$ awk '/manager/ {print}' employee.txt

# Output: awk command prints all the line which matches with the ‘manager’
ajay manager account 45000
varun manager sales 50000
```

- Splitting a Line Into Fields:
  - For each record i.e line, the awk command splits the record delimited by whitespace character by default and stores it in the `$n` variables. If the line has 4 words, it will be stored in `$1`, `$2`, `$3` and `$4` respectively.
  - Also, `$0` represents the whole line.

```bash
$ awk '{print $1,$4}' employee.txt

# Output: $1 and $4 represents Name and Salary fields respectively.
ajay 45000
sunil 25000
varun 50000
```

#### Find a file or directory

- `find . -type f -name query.sql`
  - to find at the current directory
  - `-type f` either f means file, or d means directory
  - `-name` the name of the file that need to be searched
    - can use `iname` for not case-sensitive
- `find . -type f -empty` to find the empty files

#### Find a IP address

- Find your machine's IP address: `ifconfig en0 | grep -e 'inet\s' | awk '{print $2}'`
- `ifconfig en0` will return the ip config corresponding to en0
- `grep -e 'inet\s'` will only select the row containing the inet which is `inet 192.168.0.191 netmask 0xffffff00 broadcast 192.168.0.255`
- `awk '{print $2}' will only print the second word from the row above which is `192.168.0.191`

## Terminal Shortcut

- In `.zshrc` or `.bashrc` file, we can add **alias**

```Shell
# Inside .bashrc or .zshrc file
# DEVELOPMENT
alias gs='git status'
alias activate='./venv/bin/activate'

## Kubernetes
```

## Variables

- Set a variable via `export` command
- Access the variable's value with `$`

```Shell
 # using Bash on Linux or Mac
 export dockerId="quanngha"
 echo $dockerId

 # or you can simply use = sign to set a variable
 hostIP=$(ifconfig en0 | grep -e 'inet\s' | awk '{print $2}')
```

## For Loop

```bash
for <variable name> in <a list of items>;do <some command> $<variable name>;done;

# Example
for i in {1..5}; do curl http://localhost:8010 > /dev/null; done;
```

## `Base64` Encoding

- Encoding Username & Password

```bash
# encode the word 'usename' as base64-format
➜  echo -n 'username' | base64
dXNlcm5hbWU=
# encode the word 'password' as base64-format
➜  echo -n 'password' | base64
cGFzc3dvcmQ=
```

- Encoding & Decoding the secrect binary file (e.g. private key)
  - Encoding: The output of below command can be stored in the secrect manager, so later we can load into the docker file as the environmental variable

```bash
# encode
# -w 0 option specifies that the output lines should not be wrapped. It means that the base64-encoded output will be in a `single line`, without line breaks.
cat id_rsa | base64 -w 0
```

- Decoding:
  - This is to decode the encoded base64 string into the binary output

```bash
# Decoding
echo $ENCODED_BASE64_STRING | base64 -d > id_rsa.pem
chmod 600 id_rsa.pem # give READ WRITE access to the owner
```

## `scp` file transfer from one machine to another

- For example (transfer file from machine A to machine B):
  - Generate public & private key pairs, share the public key to Machine B, and Machine A will keep the private key
- `scp -i /location_in_machine_A/to/private/key -v -P 64022 file_path machineB@ip_address:/path/to/store/inB/`
  - `-i` Identity
  - `-v` verbose to debug
  - `-P` port (note P should be in captital letter)
