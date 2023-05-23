# Table of Contents

# the unix system
- unix: the operating system
- kernel: core of the os which allocates time and memory to processes
- shell: outer layer of the os that interacts with the user and sends requests to the kernel (ex: zsh, bash available in terminal)
- see location of shell currently using: `echo $SHELL`
- see default shell `echo $0`
- set current shell to csh (or zsh, bash,...) which is a shell in a shell `csh` 
- exit current shell (which returns to shell running current shell) `exit`

# command structure
- commands are located as executable code, usually in /bin or /usr/bin
- shell looks for command's code at directories listed in path variable, in order, seperated by ":". see the path variable `echo $PATH`
- command to see where command executable code is located `which java`
- command take the form: command options arguments
- options are (dash and letter, `-v`) or (two dashes and keyword, `--version`)
- multiple options `-nvl` or `-n -v -l`
- options can take arguments (`-n50` or `-n 50`)
- output text `echo "hello world"`
- reads and executes file in shell `source file`

# text editors
- text editors in unix include emacs, nano, vim...: `nano` or `nano file.txt`

# navigating directory
- working directory: the current directory you are at
- see the present working directory `pwd`
- see the files/folders in the working directory `ls`. options: 
  - `-a` show all
  - `-l` list with information
  - `-h` make information human readable sizes
- change directory into hi relative to current `cd hi`. change relative to the root of the hard drive `cd /hi`. goto root directory `cd ~`
- unix file systems often have in the root directory:
  - `/bin` commands/programs
  - `/etc` configurations
  - `/home` users home directory
  - `/lib` system libraries
  - `/tmp` temporary files
  - `/usr` unix system resources
  - `/var` variable system data files

# creating directory
- create in working director `mkdir newfolder`
- create multiple folders within each other `mkdir -p newfolder/inner/finalfold`

# moving file
- move directory `mv original/location.txt /final`
- move directory and rename file `mv original/location.txt /final/newname.txt`
- options are: 
  - `-f` the default which forces renaming/overwriting
  - `-n` no overwriting
  - `-i` interactive, making it ask you

# read text files
- concatenate and output text `cat hello.txt` or `cat h1.txt h2.txt`
- output all at once `more h1.txt`
- output with scrolling and better viewing `less h1.txt`

# copying
- copy file from.txt into new.txt `cp from.txt new.txt`
- copy entire directory and all children `cp -R original orig_backup`
- options:
  - `-f` force overwriting
  - `-n` no overwriting
  - `-i` interacting, making it ask you

# deleting
- delete file permanently `rm file.txt`
- delete directory `rm -R foldername`

# symbolic link
- an alias for a path
- breaks if folder/file in path is removed
- `ln -s original/file path/symlink_name`

# searching
- search by file name: `find /location_to_search -name "file.jpg"`
- use `*` as a wildcard 

# users
- use `sudo` keyword before command to have root permission
- see username of current login `whoami`
- see all current logins `who`
- see path to current users home `echo $HOME`
- see groups that current user is in `groups`
- change ownership of file to user1 in group group1 `chown user1:group1 file.txt`
  - `-R` to set directory and all subfiles to new owner and group

# file permissions
- using `ls -l` to see first column displaying permission
- 9 letters represent user, group, other permission. 3 letters in each show read (r) write (w) and execute (x) permissions. This is represented in octal as 7 for wrx, 6 for wr-,...
- set permissions `chmod 777 filename`

# system information
`date` current system date
`uptime` how long system has been on
`users` all users who are on system
`who` all current logins; console is background computer itself
`uname` name of flavor of unix using
  - `-a` more information
  - `-p` processor name
`df` amount of disk free space avaiable
  - `-h` human readable
`du path/to_dir` disk usage in blocks of space
  - `-h` human readable
  - `-a` all files and directories
  - `-d 1` depth of 1 showing info one level deep into director

# processes
- `ps` list of processes belonging to current user running
  - `-a` list of processes running by all users
  - `-x` list of all processes
- `ps aux` old style to list more information about processes including user
- `top` running dashboard of all processes
- pid is process id for a process
- `kill -9 2650` kill a process with pid 2650
- `history` list of previous commands, with reference numbers
- `!458` runs command with reference number 458
- `sudo !!` runs previous command with sudo

# input and output
- `command > file` direct stdout to file
- `command >> file` appends stdout to end of file
- `command < file` direct stdin from file
- `command1 | command2` pipping takes output of command1 as input
- /dev/null is a black hold where any data sent there is deleted
- `main -s “subject” hi@gmail.com < msg_file` unix builtin mail program
- `mysql -u user -p database < db_backup.sql` run backup database scripts

# bash configuration
- upon login by user, shell configures at ~/.bash_profile and ~/.bash_login
- upon starting a new shell, shell configures at ~/.bashrc
- upon logout, shell looks at ~/.bash_logout
- ~/.bash_profile configurations will load for one shell, but to make them load for new shells too you need to duplicate confiurations in ~/.bashrc or add this code to .bash_profile:
```
if [ -f ~/.bashrc ]; then
	source ~/.bashrc
fi
```

# zshell configuration
- upon login by user, shell configures in order at ~/.zshenv, ~/.zprofile, ~/.zshrc, ~/.zlogin
- upon starting a new shell, configures in order at ~/.zshenv, ~/.zshrc
- upon logging out ~/.zlogout
- notice ~/.zshenv and ~/.zshrc appear for both new shells and first shell
- set info displayed at new shell login in ~/.zshrc:
```
echo “”
echo -n “Welcome, “; whoami
echo “”
```

# alias
- `alias` lists all current aliases
- `alias ll=ls -lah` create a new alias named ll which runs ls -lah, which only exists for current shell
- aliases should be added to configuration file (.zshrc) so they can be used anytime you start a shell

# environment variables
- environemnt variables are used by commands and applications. they are settings for the unix environment
- environment variables must be set in configuration file to be run at every new shell
- `export MY_NAME=‘xander’` create environment variable MY_NAME with value xander
- `echo $MY_NAME` see environment variable 
- $HOME
  - the home path for the current user logged in
- $PATH
  - the path variable is described in [command structure](#command-structure)
  - `export PATH=“$PATH:/usr/local/newdir”`add a path to the end of the current path variable
- $PS1
  - `export PS1=“%n > “`
  - command prompt is set in environment variable PS1, which appears at the beginning of each new line in the terminal
  - zsh format codes for setting PS1:
    - %n username
    - %N current shell
    - %d current working directory
    - %1d basename of current working
    - %M hostname
    - %m hostname up to first period
    - %! history number of this command
    - %w date in weekday-date format
    - %T time in 24-hr HH:MM format
    - %* time in 24-hr HH:MM:SS format
    - %t time in 12-hr HH:MM am/pm format
    - %D{format} use strftime format (%Y-%m-%d)

