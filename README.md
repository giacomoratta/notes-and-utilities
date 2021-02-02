# Notes and Utilities

## Git

#### Merge commits
- avoid multiple commits about the same changes (e.g. many attempts to do something)
- after all of those commits, we want to merge them in one clean commit only
- `git rebase -i HEAD~3` (change the number until you see the first commit)
- in the editor, change to `s` all the commits behind the first one (which has to be `pick`), and save
- in the next editor, remove the multiple commit messages, set one message, and save
- `git push -f` (with force option) to change the commit list
- only the first commit will remain

#### Change commit name
- `git commit --amend`

#### Remove added files (with `git add`)
- `git restore --staged <filepath>`

#### Deleting multiple local branches
- `git branch | grep "<pattern>"`
- `git branch | grep "<pattern>" | xargs git branch -D`


## Network

#### Free ports
- `netstat -anp | grep "8080"`: check which processes are using port 8080 
- ord `sudo netstat -tulpn | grep :80`: processes using port 80
- or `sudo ss -lp "sport = 8080"`: check pid=...
- `kill -9 <PID>`: last column of previous output has the `PID`

## Developing
- `alias java-set8="sudo update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java"`: set java 8 as alternative


## Files

#### Search for text
- `grep -ri listen /etc/apache2`: check the word "listen" in each file of the absolute path



## Services

#### Basics
- `/etc/init.d/apache2 start` (stop, restart, status, etc.)
- `sudo service nginx start` (stop, restart, status, etc.)



## Apache2 (Ubuntu 20.04)
- `sudo apt install apache2`
- `sudo nano /etc/apache2/apache2.conf`: change configuration
- `sudo apachectl configtest`: check syntax of configuration file
- `sudo systemctl reload apache2`: reload apache2

#### Domains
- `cd /etc/apache2/sites-available/`: go to available websites .conf files
- `sudo a2ensite 000-default`: enable the default website
- `sudo a2dissite 000-default`: disable the default website

## File System
- `lsblk -f`: list block devices and more informations
- `blkid`: locate/print block device attributes
- `sudo file -s /dev/nvme0n1`: information about a specific device, such as its file system type



