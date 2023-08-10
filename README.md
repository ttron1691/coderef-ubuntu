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

