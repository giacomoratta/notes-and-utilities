# Notes and Utilities

## Files, directories, search
- `find . -type f -exec grep -H 'my text' {} \;`: search "my text" in all files in the current directory


## Git

#### Restore files
- `git restore <filepath>`: restore the previous version (from previous commit)
- `git restore --staged <filepath>` (remove file from commit, added with `git add`)

#### Merge commits
- avoid multiple commits about the same changes (e.g. many attempts to do something)
- after all of those commits, we want to merge them in one clean commit only
- `git rebase -i HEAD~3` (change the number until you see the first commit)
- in the editor, change to `s` all the commits behind the first one (which has to be `pick`), and save
- in the next editor, remove the multiple commit messages, set one message, and save
- `git push origin +branch-name-123` to force push to this branch only
- only the first commit will remain

#### Change current commit (name, add new changes, etc.)
- `git commit --amend`
- `git push origin +branch-name-123`

#### Deleting multiple local branches
- `git branch | grep "<pattern>"`
- `git branch | grep "<pattern>" | xargs git branch -D`

#### Stash
- `git stash clear` - deletes all stashed changes
- `git stash -m "possible changes 1"` - pushes a stash with a label
- `git stash push src/f1.js src/f2.js` - pushes a stash by listing files


## Networking

#### Free ports
- `netstat -anp | grep "8080"`: check which processes are using port 8080 
- ord `sudo netstat -tulpn | grep :80`: processes using port 80
- or `sudo ss -lp "sport = 8080"`: check pid=...
- `kill -9 <PID>`: last column of previous output has the `PID`

#### Troubleshooting
- `traceroute 127.0.0.1`: trace the route to a host
- `nslookup localhost`: interactive queries to DNS
- `dig localhost`: DNS lookup utility (more verbose than `nslookup`)


## Developing
- `alias java-set8="sudo update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java"`: set java 8 as alternative


## Files

#### Search for text
- `grep -ri listen /etc/apache2`: check the word "listen" in each file of the absolute path

#### Edit files
- `sed -i'' 1d large-data-file.csv`: remove the first line 



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


## Docker

#### Basics
- `docker image ls -a`: list all images (hidden/intermediate included)
- `docker ps -a`: list all containers

#### Images
- `docker build -t abc123 .`: build the image

#### Containers: execution
- `docker run -d -t abc123`: run container based on image "abc123", detached (-d) and with terminal (-t)
- `docker run -d -t -p 3020:3000 abc123`
- `docker run -d -t -P abc123`: expose ports with automatically assigned one (-P)
- `docker exec -ti e390ceb99781 sh`: access the container with a terminal

#### Images: cleaning
- `docker rmi 9329ff23f2`: remove 1 image
- `docker rmi $(docker images -q)`: remove all images
- print all image IDs of intermediates <none>; the size is cumulative, so nothing to care about... just look at the list sometimes
  `docker images -a | awk '/none/ {print $3}'`
  `docker rmi $(docker images -a | awk '/none/ {print $3}')`

#### Containers: stop and cleaning
- `docker stop 84a4114a37d9`: stop 1 container
- `docker stop $(docker ps -a -q)`: stop all running containers
- `docker container rm 84a4114a37d9`: remove 1 container
- `docker rm $(docker ps -a -q)`: remove all containers

## MySQL

#### The basics
- `mysql --port=3306 -h localhost -u myname -p`: connect with password
- `mysql> select * from mysql.user;`: show users
- `mysql> DESC mysql.user;`: show users with less info
- `mysql> USE database_name;`: select the database to work with
- `mysql> SHOW FULL TABLES;` or `mysql> SHOW TABLES;`: show tables of a database

#### Users and privileges
- `mysql> SHOW GRANTS FOR username;`: check the privileges given to an user
- `mysql> CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';`: create a new user with a password
- `mysql> GRANT ALL PRIVILEGES ON *.* TO 'user_name'@'localhost' WITH GRANT OPTION;';`: make a super-user
- `mysql> CREATE USER 'username'@'%' IDENTIFIED BY 'password';`: create a new user with a password for any host
- `mysql> GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;`: create a new user with a password for any host
- `mysql> FLUSH PRIVILEGES;`: reload all the privileges


## AWS

#### Connect via CLI
- `cat ~/.aws/credentials` - check if credentials are present
- `cat ~/.aws/config` - check config details
- `aws configure --profile abc123` - add credentials for profile "abc123"
- `export AWS_DEFAULT_PROFILE=abc123` - set default profile, to avoid `--profile` parameter
- `aws s3api list-buckets` - simple command for a quick check

#### SSM Parameter Store
- `aws ssm get-parameters --names /my-app/dev/db-url /my-app/dev/db-password`
- `aws ssm get-parameters --names /my-app/dev/db-url /my-app/dev/db-password --with-decryption`: automatically encoded secrets with KMS key
- `aws ssm get-parameters-by-path --path /my-app/ --recursive`: lists all parameters under the path


## JEST

#### Investigations
- `jest --runInBand --detectOpenHandles --config jest.config.json --runTestsByPath src/server/**/*.test.js`
- `--runInBand`: run tests sequentially
- `--detectOpenHandles`: wait for open handles
