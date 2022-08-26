# Shell 
## What is the shell?
- Computers these days have a variety of interfaces for giving them commands; fanciful graphical user interfaces, voice interfaces, and even AR/VR are everywhere. These are great for 80% of use-cases, but they are often fundamentally restricted in what they allow you to do — you cannot press a button that isn’t there or give a voice command that hasn’t been programmed. To take full advantage of the tools your computer provides, we have to go old-school and drop down to a textual interface: The Shell.
- In this lecture, we will focus on the Bourne Again SHell, or “bash” for short. This is one of the most widely used shells, and its syntax is similar to what you will see in many other shells. To open a shell prompt (where you can type commands), you first need a terminal. Your device probably shipped with one installed, or you can install one fairly easily.

## Shell Command
- **Environment Variable** called `$PATH` that lists which directories the shell should search for programs when it is given a command
  - When we run the echo command, the shell sees that it should execute the program echo, and then searches through the :-separated list of directories in $PATH for a file by that name. When it finds it, it runs it (assuming the file is executable; more on that later).
  ```shell
  home:~$ echo $PATH
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  
  home:~$ which echo
  /bin/echo
  
  home:~$ /bin/echo $PATH
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  ```
### Using the shell
| Command  | Description | 
|----------|-------------|
|`echo`|A program simply prints out its arguments. <br>- If you want to provide an argument that contains spaces or other special characters (e.g., a directory named "My Photos"), you can either quote the argument with `'` or `"` , or escape just the relevant characters with `\` (`My\ Photos`).|
|`which`|To find out which file is executed for a given program name |

### Navigating in the shell
| Command  | Description | 
|----------|-------------|
|`.`| refers to your current directory|
|`..`| refers to the parent of your current directory|
|`~`| `~`: the tilda slash refers to your home directory <br> so for example `~/.bashrc` refer to `.bashrc` is a file in home directory|
|`-`| previous path <br>`cd -` to change directory to previous path|
|`pwd`| get the path of current working directory|
|`ls`|print the contents of the current directory|

- `ls -l`: This gives us a bunch more information about each file or directory present.
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
| Command  | Description | 
|----------|-------------|
|`mv <src_path> <dst_path>`| Move/rename the file<br>`mv foo.md dotfiles.md` to rename the "foo" to "dotfiles" file|
|`cp <src_path> <dst_path>`|Copy the file|
|||
|`tar zxvf sentences.tgz -C sentences` | unzip file  **sentences.tgz** into **sentences** folder | 
|||
|`cat file.txt`| **cat** a program that is use to display the content of a file|
|`touch new_file.txt`|**touch** command is for creating a file |
|`nano file.txt` |**nano** is a text editor|


## Nano Editor
There is a basic menu at the bottom of the screen. The commands are:
- `^G` Get help
- `^O` Write out the file (save)
- `^W` Where is (find)
- `^K` Cut Text (remove line)
- `^J` Justify
- `^X` Exit
- `^R` Read (insert another file)
- `^\` Replace (find and replace)
- `^U` Uncut Text (paste line)
- `^T` To Spell (spell check)
