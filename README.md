# Notes and Utilities

## Git

#### Clean commits
- avoid multiple commits about the same changes (e.g. many attempts to do something)
- after all of those commits, we want to merge them in one clean commit only
- `git rebase -i HEAD~3` (change the number until you see the first commit)
- in the editor, change to `s` all the commits behind the first one (which has to be `pick`), and save
- in the next editor, remove the multiple commit messages, set one message, and save
- `git push -f` (with force option) to change the commit list
- only the first commit will remain



## Network

#### Free ports
- `netstat -anp | grep "8080"`: check which processes are using port 8080 
- `kill -9 <PID>`: last column of previous output has the `PID`

## Developing
- `alias java-set8="sudo update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java"`: set java 8 as alternative
