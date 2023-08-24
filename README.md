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



