# ICCS474
## Internet Programming

## BASH

### What is Bash?
- It is a unix shell.
- It typically runs in a text window, where the user types commands that cause actions.
- Bash can also read commands from a file, called a script
- For example,
- To create a folder, we usually use File Manager provided by the OS.

Using terminal, we can type in bash command to create a folder in the current working directory.

```bash
mkdir <FOLDERNAME>
```

### Bash commands

Code reference from Live example

```bash
pwd               # present working directory
touch <FILENAME>  # create an empty file
ls                # List files and folders
ls -a             # list all files and folders including hidden files
ls -la            # list all files and folders including hidden files in detail
cd <FOLDERNAME>   # change directory to specific folder
cd /              # change directory to root
cd ~              # change directory to home folder
cd ..             # change directory up one level
cat <FILENAME>    # see file detail
tail <FILENAME>    # see file content from the last line of the file.
cp <SOURCE FILE NAME> <DESTINATION FILE NAME>   #copy file
mv <SOURCE FILE NAME> <DESTINATION FILE NAME>   #move file
rm <FILENAME>       # delete (remove) file
rm -r <FOLDERNAME>  # delete (remove) file or folder
rm -f <FILENAME>    # force delete (remove) file
rm -rf <FOLDERNAME> # force delete (remove) file or folder
ln -s <FILENAME1> <FILENAME2>  # symbolic link file (like shortcut)
```

`.` is typically current folder. You can do many things with it. eg. you can simply type

```bash
subl .            # if you have sublime symlinked
atom .            # if you have atom
subl ~/Desktop    # if you want to open Desktop folder in sublime
open .            # only for MAC open pwd in finder app
```

### Terminal Text Editor

It doesn't matter how many text editor you have on your computer. Because when you are working on server, you will end up with just command lines.

It is very very important that you know these 2 text editor in terminal.

#### nano

Try it by typing `nano ~/Desktop/hello.md`
If you choose to save the file, it should create a file on Desktop.

#### vim

VIM is a very advance tool. Some programmer are still using it in a daily basis. They are not even bothered to use Sublime or Atom.

In most Ubuntu build, `vim` is preinstalled but you might want to keep it up to date by running `sudo apt-get install vim`.

Using it is more difficult, here are the list of commands you must remember.

```bash
# press `i` to start editing (esc to exit edit mode)
# type `:q` to quit
# type `:q!` to force exit without saving
# type `:w` to save
# type `:wq` to save and quit
# type `/<something>` to find something in text. (type `/` to go to the next result)
```

Of course there are a lot more shortcuts. You can even create your own vim profile and store it in your own git.

For example, check my vimrc. https://github.com/SaKKo/vimrc/blob/master/.vimrc

I rarely use it so don't expect me to be expert in vim.
