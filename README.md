# Code Reference for Ubuntu
## Directory Structure on File System
The typical directory structure on a Ubuntu Linux file system looks as follows
```Shell
/ (Root)        # Root of file system
/bin            # Binaries, symbolic link to /usr/bin/
/boot           # ...
/dev            # ...
/etc            # ...
/home           # Home directory, separate directory for each user
/lib            # Libraries, symbolic link to /usr/lib/
/lost+found     # ...
/media          # ...
/mnt            # ...
/opt            # ...
/proc           # ...
/root           # ...
/run            # ...
/sbin           # ...
/snap           # ...
/srv            # ...
/sys            # ...
/tmp            # ...
/usr            # ...
/var            # ...
```
## Directory Management
### Basics
```Shell
ls [OPTION] [VERZEICHNIS]         # list content of current directory
cd [OPTION] VERZEICHNIS           # change directory
mkdir [OPTION] Verzeichnisname    # create new directory
pwd [OPTIONEN]                    # print working directory

# Examples
ls $HOME              # Documents Pictures Downloads ...
cd /usr/local         # Change to /usr/local directory
cd                    # Change to home directory
mkdir bin             # creates new directory with name bin
pwd $HOME/Documents   # /home/USERNAME/Documents
```
### Copy
### Move
## User Management
### Basics
```Shell
id                # Shows information about current user
whoami            # Shows username of current user
users             # Shows list of users which are logged in
groups USERNAME   # Shows groups of user with given username
```
### Add User
```Shell
sudo adduser BENUTZER [OPTIONEN]
sudo addgroup [OPTIONEN] GRUPPE
# Examples
sudo adduser john             # create new user john
sudo adduser xyz www-data     # add user xyz to group
```
Add given user to sudo group
```Shell
sudo usermod -aG sudo BENUTZERNAME
```
Change password of given user 
```Shell
passwd [OPTIONEN] [BENUTZERNAME]
passwd           # Change own password
sudo passwd user # change users password
```
## Updates
For updates and upgrades, the following commands for the package manager can be used
```Shell
sudo apt update
sudo apt upgrade
```
## cat
Originally cat was used to concatenate files
```Shell
cat OPTIONEN DATEI(EN)
```
Merge files with cat
```Shell
cat Seite_1.txt Seite_2.txt > text_komplett.txt
```
Use cat to show content of text filed
```Shell
cat textfile.txt
```
## cd
Changing directory within the Linix shell is done via
```Shell
cd [OPTION] VERZEICHNIS
```
Merge files with cat
```Shell
cd /usr/local             # Wechsel nach /usr/local
cd bin                    # Wechsel von /usr/local nach /usr/local/bin
cd                        # Wechselt nach $HOME
cd ..                     # Wechselt ins übergeordnete Verzeichnis also z.B. von /home/user nach /home
cd ../user2               # Wechselt ins übergeordnete Verzeichnis und von dort nach user2, also z.B. von /home/user nach /home/user2 
```
Use cat to show content of text filed
```Shell
cat textfile.txt
```
## SSH
The secure shell (SSH) protocol is most widely used to safely log in to a remote machine (e.g. remote server or server cluster). The basic command is given by
```Shell
ssh username@remote
# Example
ssh john@myserver.mydomain.de
```
### Key Authentication
The public key authentication is the recommended way for log in purposes instead of using a username and password. The basic idea of SSH key authentication is as follows. Each user creates an SSH key pair consisting of a private and a public SSH key. The private key is kept private in every case on a local machine whereas the public SSH key is copied to each instance the user wants to log in to. 
Typically, the public key has the file ending ".pub"

The public key of a registered user is typically located at the remote client directory "~/.ssh/authorized_keys".

In order to create a key pair we can use the following command
```Shell
ssh-keygen -t rsa -b 4096 -C "user@server Server 1"
```
The public key can be placed on the remote system via the use of the "ssh-copy" command
```Shell
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```
In case "ssh-copy" cannot be used or does not work as expected we may copy the public key content manually to the remote system via
```Shell
cat id_rsa.pub | ssh user@server 'cat>> ~/.ssh/authorized_keys'
```
### Security settings
If SSH is used on a server, the following settings for the global SSH configuration file "/etc/ssh/sshd_config" should be set for security reasons
```Shell
PasswordAuthentication no
ChallengeResponseAuthentication no
PermitRootLogin no
```
This enforces the log in via key authentication. The SSH server can be restarted via
```Shell
sudo systemctl reload ssh
```
## Firewall
We can use the ufw (uncomplicated firewall) package which can be installed as follows
### Installation
```Shell
sudo apt-get install ufw
```
### Status
Check for the firewall status
```Shell
sudo ufw status
```
### Different Commands and Settings
Reload the firewall after adjusting rules
```Shell
sudo ufw reload
```
At this point, the firewall is no active. We can define rules for allowing outgoing and blocking incoming traffic
```Shell
sudo ufw default deny incoming  
sudo ufw default allow outgoing
```
Show apps and rules
```Shell
sudo ufw app list
```
In any case, it is necessary to allow the standard SSH protocol in order to access the remote machine
```Shell
sudo ufw allow ssh
```
### Enabling
We can enable the firewall (after allowing ssh) by
```Shell
sudo ufw enable
```


## Basic Terminal Navigation

| Command | Description | Examples |
|---------|-------------|----------|
| `pwd` | Print working directory | `pwd` → `/home/user` |
| `ls` | List directory contents | `ls -la` (shows all files with details) |
| `cd` | Change directory | `cd Documents`, `cd ..` (parent directory), `cd ~` (home) |
| `mkdir` | Create directory | `mkdir new_folder` |
| `rm` | Remove files/directories | `rm file.txt`, `rm -r folder/` (recursive), `rm -rf folder/` (force) |
| `cp` | Copy files/directories | `cp file.txt backup.txt`, `cp -r dir1/ dir2/` |
| `mv` | Move/rename files | `mv file.txt newname.txt`, `mv file.txt ~/Documents/` |
| `touch` | Create empty file | `touch newfile.txt` |
| `cat` | Display file contents | `cat file.txt` |
| `less` | View file with pagination | `less large_file.txt` (use q to exit) |
| `head`/`tail` | Show beginning/end of file | `head -n 10 file.txt`, `tail -f log.txt` (follow) |
| `find` | Search for files | `find /home -name "*.txt"` |
| `grep` | Search text patterns | `grep "pattern" file.txt`, `grep -r "text" /dir/` (recursive) |

## File Permissions

| Command | Description | Examples |
|---------|-------------|----------|
| `chmod` | Change file permissions | `chmod 755 script.sh`, `chmod +x script.sh` (make executable) |
| `chown` | Change file owner | `chown user:group file.txt` |
| `umask` | Set default permissions | `umask 022` (default is usually 022) |

Permission Numeric Values:
- 4: Read (r)
- 2: Write (w)
- 1: Execute (x)

Common Permission Combinations:
- 755 (rwxr-xr-x): Owner can read/write/execute, others can read/execute
- 644 (rw-r--r--): Owner can read/write, others can read
- 700 (rwx------): Owner can read/write/execute, others have no access

## Process Management

| Command | Description | Examples |
|---------|-------------|----------|
| `ps` | Show process status | `ps aux` (all processes), `ps -ef` (full format) |
| `top`/`htop` | Process monitoring | `top`, `htop` (more interactive) |
| `kill` | Terminate process | `kill PID`, `kill -9 PID` (force kill) |
| `pkill` | Kill process by name | `pkill firefox` |
| `bg` | Send process to background | `bg` |
| `fg` | Bring process to foreground | `fg` |
| `jobs` | List background jobs | `jobs` |
| `nohup` | Run command immune to hangups | `nohup command &` |
| `&` | Run process in background | `command &` |
| `pgrep` | Find process ID by name | `pgrep firefox` |

## System Information

| Command | Description | Examples |
|---------|-------------|----------|
| `uname` | System information | `uname -a` (all info) |
| `lsb_release` | Ubuntu version | `lsb_release -a` |
| `df` | Disk space usage | `df -h` (human-readable) |
| `du` | Directory space usage | `du -sh directory/` (summary, human-readable) |
| `free` | Memory usage | `free -h` (human-readable) |
| `lsblk` | List block devices | `lsblk` |
| `lshw` | Hardware information | `sudo lshw` |
| `lscpu` | CPU information | `lscpu` |
| `ifconfig`/`ip` | Network interfaces | `ifconfig`, `ip addr` |
| `lsof` | List open files | `lsof -i :80` (check port 80) |
| `dmesg` | Kernel messages | `dmesg` |

## Package Management (APT)

| Command | Description | Examples |
|---------|-------------|----------|
| `apt update` | Update package lists | `sudo apt update` |
| `apt upgrade` | Upgrade packages | `sudo apt upgrade` |
| `apt install` | Install package | `sudo apt install package_name` |
| `apt remove` | Remove package | `sudo apt remove package_name` |
| `apt purge` | Remove package and configs | `sudo apt purge package_name` |
| `apt search` | Search packages | `apt search keyword` |
| `apt show` | Show package details | `apt show package_name` |
| `apt list` | List packages | `apt list --installed` |
| `apt autoremove` | Remove unused dependencies | `sudo apt autoremove` |
| `dpkg -i` | Install .deb file | `sudo dpkg -i package.deb` |
| `add-apt-repository` | Add PPA | `sudo add-apt-repository ppa:name/ppa` |

## Text Processing

| Command | Description | Examples |
|---------|-------------|----------|
| `grep` | Search for pattern | `grep "pattern" file.txt`, `grep -i` (case insensitive) |
| `sed` | Stream editor | `sed 's/old/new/g' file.txt` (substitute) |
| `awk` | Text processing | `awk '{print $1}' file.txt` (print first column) |
| `cut` | Extract sections | `cut -d ',' -f 1 file.csv` (1st field, comma delimiter) |
| `sort` | Sort lines | `sort file.txt`, `sort -n` (numeric), `sort -r` (reverse) |
| `uniq` | Remove duplicates | `sort file.txt \| uniq` |
| `wc` | Count lines/words/chars | `wc -l file.txt` (line count) |
| `tr` | Translate characters | `cat file.txt \| tr '[a-z]' '[A-Z]'` (uppercase) |
| `diff` | Compare files | `diff file1.txt file2.txt` |
| `tee` | Read from stdin, write to stdout/files | `command \| tee file.txt` |

## Redirection & Pipes

| Symbol | Description | Examples |
|--------|-------------|----------|
| `>` | Redirect stdout (overwrite) | `ls > files.txt` |
| `>>` | Redirect stdout (append) | `echo "text" >> file.txt` |
| `<` | Redirect stdin | `sort < unsorted.txt` |
| `2>` | Redirect stderr | `command 2> errors.log` |
| `2>&1` | Redirect stderr to stdout | `command > output.txt 2>&1` |
| `\|` | Pipe output to next command | `ls \| grep ".txt"` |
| `/dev/null` | Discard output | `command > /dev/null 2>&1` |

## Shell Scripting Basics

### Script Header
```bash
#!/bin/bash
# Description: My script
```

### Variables
```bash
NAME="Ubuntu"         # Define variable (no spaces around =)
echo $NAME            # Use variable
echo "${NAME}_user"   # Use variable in string
readonly CONST="value" # Constant variable
```

### Command Substitution
```bash
current_dir=$(pwd)    # New style
date_old=`date`       # Old style
```

### Math Operations
```bash
result=$((5 + 3))     # Arithmetic expansion
let sum=10+20         # Using let
expr 5 + 3            # Using expr (spaces required)
```

### Conditional Statements
```bash
if [ "$a" -eq "$b" ]; then
    echo "a equals b"
elif [ "$a" -gt "$b" ]; then
    echo "a is greater than b"
else
    echo "a is less than b"
fi

# Modern test syntax
if [[ "$string" == *wild* ]]; then
    echo "Pattern matched"
fi
```

### Comparison Operators
Numeric:
- `-eq` (equal)
- `-ne` (not equal)
- `-gt` (greater than)
- `-lt` (less than)
- `-ge` (greater than or equal)
- `-le` (less than or equal)

String:
- `==` (equal)
- `!=` (not equal)
- `-z` (empty string)
- `-n` (not empty string)

File tests:
- `-e` (exists)
- `-f` (regular file)
- `-d` (directory)
- `-r` (readable)
- `-w` (writable)
- `-x` (executable)

### Loops

For loop:
```bash
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# Range
for i in {1..5}; do
    echo "Number: $i"
done

# C-style
for ((i=0; i<5; i++)); do
    echo "Number: $i"
done
```

While loop:
```bash
count=0
while [ $count -lt 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

Until loop:
```bash
count=0
until [ $count -ge 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

### Case Statement
```bash
case "$option" in
    start)
        echo "Starting service"
        ;;
    stop)
        echo "Stopping service"
        ;;
    restart|reload)
        echo "Restarting service"
        ;;
    *)
        echo "Usage: $0 {start|stop|restart}"
        ;;
esac
```

### Functions
```bash
# Define function
my_function() {
    echo "Parameter 1: $1"
    local local_var="I'm local"  # Local variable
    return 0  # Return status
}

# Call function
my_function "parameter"
```

### Input & Output
```bash
# Read user input
echo "Enter name:"
read name
echo "Hello, $name"

# Read with prompt
read -p "Enter age: " age

# Read secret
read -sp "Password: " password
echo

# Read into array
read -a arr -p "Enter items: "
echo "First item: ${arr[0]}"
```

### Arrays
```bash
# Define array
fruits=("apple" "banana" "cherry")

# Access element
echo ${fruits[1]}  # banana

# All elements
echo ${fruits[@]}

# Array length
echo ${#fruits[@]}

# Add element
fruits+=("orange")

# Iterate
for fruit in "${fruits[@]}"; do
    echo "$fruit"
done
```

### String Operations
```bash
str="Ubuntu Linux"

# Length
echo ${#str}

# Substring (position, length)
echo ${str:0:6}  # Ubuntu

# Replace
echo ${str/Ubuntu/Debian}  # Debian Linux

# Replace all occurrences
echo ${str//u/U}

# Check if starts with
if [[ "$str" == Ubuntu* ]]; then
    echo "Starts with Ubuntu"
fi
```

## Advanced Shell Features

### Error Handling
```bash
# Exit on error
set -e

# Exit on unbound variable
set -u

# Trap errors
trap 'echo "Error on line $LINENO"; exit 1' ERR

# Custom error function
error() {
    echo "ERROR: $1" >&2
    exit 1
}
```

### Process Substitution
```bash
diff <(ls dir1) <(ls dir2)
```

### Here Documents
```bash
cat << EOF > file.txt
This is line 1
This is line 2
EOF
```

### Brace Expansion
```bash
echo {1..5}         # 1 2 3 4 5
echo {a..e}         # a b c d e
echo file{1,2,3}.txt # file1.txt file2.txt file3.txt
mkdir -p project/{src,docs,tests}
```

### Parameter Substitution
```bash
# Default value if unset
echo ${var:-default}

# Assign default if unset
echo ${var:=default}

# Error if unset
echo ${var:?error}

# Use alternate if set
echo ${var:+alternate}
```

### Command Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Ctrl+C` | Interrupt (kill) current process |
| `Ctrl+Z` | Suspend current process |
| `Ctrl+D` | End of file/input |
| `Ctrl+L` | Clear screen |
| `Ctrl+A` | Move cursor to beginning of line |
| `Ctrl+E` | Move cursor to end of line |
| `Ctrl+U` | Cut from cursor to beginning of line |
| `Ctrl+K` | Cut from cursor to end of line |
| `Ctrl+W` | Cut word before cursor |
| `Ctrl+Y` | Paste previously cut text |
| `Ctrl+R` | Search command history |
| `!!` | Repeat last command |
| `!$` | Last argument of previous command |
| `!*` | All arguments of previous command |
| `!string` | Most recent command starting with "string" |
| `Alt+.` | Insert last argument of previous command |


