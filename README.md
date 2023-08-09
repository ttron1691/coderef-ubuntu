# Code Reference for Ubuntu
## Directory Management
### Copy Files and Directories
### Move Files and Directories
## User Management
### Add User
```Shell
sudo adduser BENUTZER [OPTIONEN]
sudo addgroup [OPTIONEN] GRUPPE
```
Examples
```Shell
sudo adduser newuser      # create new user
sudo adduser xyz www-data # add user to group
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
