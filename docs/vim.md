# VIM
- `vi file_name` or `vim file_name` to open the file

## Command Mode
- `:set number` to set number labelling for each line
- `:syntax on` to color-lightning the syntax

### Navigating around
- Move Forward/Backward
  - `w`: move forward word by word
  - `b`: move backward word by word
- Move Up/Down/Left/Right
  - `j`: move down
  - `k`: move up
  - `h`: move left
  - `l`: move right
- Move begining/end of the line
  - `0`: beginning of the line
  - `$`: end of the line
- Begininng of the file: `gg`
- `SHIFT + ]` to move line by line in VIM editor

## Insert Mode
- press `i` to enter insert mode, or `a` means append

### Undo & Redo
- Exit the **Insert Mode** by pressing `ESC` 
- Undo: `u`
- Redo: `CTRL + r`

### Delete
- Exit the **Insert Mode** by pressing `ESC` 
- `d` delete
  - `dw` delete a word
  - `db` delete a beginning of the word
  - `dd` delete a line

### Cut, Copy and Patse

## How to quit VIM editor
- `ESC` (to back Command mode) &#8594; `:q!`
