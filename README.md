# unix-utilities

## Network

#### Free ports
- `netstat -anp | grep "8080"`: check which processes are using port 8080 
- `kill -9 <PID>`: last column of previous output has the `PID`

## Developing
- `alias java-set8="sudo update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java"`: set java 8 as alternative
