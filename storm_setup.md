Storm:

For setting up storm, we need the following:
    1. Zookeeper
    2. ZeroMQ
    3. jzmq

Installing ZeroMQ:

# Download zeromq
# Ref http://zeromq.org/intro:get-the-software 
shubhamrohilla@StormNimbusServer:/$ sudo wget https://github.com/zeromq/libzmq/releases/download/v4.2.2/zeromq-4.2.2.tar.gz

# Unpack tarball package
shubhamrohilla@StormNimbusServer:/$ sudo tar xvzf zeromq-4.2.2.tar.gz

# Install dependency
shubhamrohilla@StormNimbusServer:/$ sudo apt-get update && \
> sudo apt-get install -y libtool pkg-config build-essential autoconf automake uuid-dev

# Create make file
cd zeromq-4.2.2
./configure

# Build and install(root permission only)
sudo make install

# Install zeromq driver on linux
sudo ldconfig

# Check installed
ldconfig -p | grep zmq

# Expected
############################################################
# libzmq.so.5 (libc6,x86-64) => /usr/local/lib/libzmq.so.5
# libzmq.so (libc6,x86-64) => /usr/local/lib/libzmq.so
############################################################

Actual:
shubhamrohilla@StormNimbusServer:/zeromq-4.2.2$ ldconfig -p | grep zmq
	libzmq.so.5 (libc6,x86-64) => /usr/local/lib/libzmq.so.5
	libzmq.so (libc6,x86-64) => /usr/local/lib/libzmq.so

Installing libsodium:

# run in sudo
# Before installing, make sure you have installed all the needed packages
sudo apt-get install libtool pkg-config build-essential autoconf automake

shubhamrohilla@StormNimbusServer:/$ sudo apt-get install libtool pkg-config build-essential autoconf automake
Reading package lists... Done
Building dependency tree       
Reading state information... Done
autoconf is already the newest version (2.69-11).
automake is already the newest version (1:1.15.1-3ubuntu2).
build-essential is already the newest version (12.4ubuntu1).
libtool is already the newest version (2.4.6-2).
pkg-config is already the newest version (0.29.1-0ubuntu2).
0 upgraded, 0 newly installed, 0 to remove and 9 not upgraded.

sudo apt-get install libzmq-dev

shubhamrohilla@StormNimbusServer:/$ sudo apt-get install libzmq-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package libzmq-dev is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'libzmq-dev' has no installation candidate

# Install libsodium
git clone git://github.com/jedisct1/libsodium.git

shubhamrohilla@StormNimbusServer:/zeromq-4.2.2$ sudo git clone git://github.com/jedisct1/libsodium.git
Cloning into 'libsodium'...
remote: Enumerating objects: 175, done.
remote: Counting objects: 100% (175/175), done.
remote: Compressing objects: 100% (124/124), done.
remote: Total 32568 (delta 87), reused 104 (delta 49), pack-reused 32393
Receiving objects: 100% (32568/32568), 8.57 MiB | 26.26 MiB/s, done.
Resolving deltas: 100% (19344/19344), done.

shubhamrohilla@StormNimbusServer:/zeromq-4.2.2$ cd libsodium/

------ Will do libsodium later.
--------------------------------------------------------------------------------------------------------------------------------------

Moving on with Storm installation:

--------------------------------------------------------------------------------------------------------------------------------------

How to connect to the linux VM on Cloud using terminal:

ssh -i <location of ssh key full path> username@<full server name / public IP Address>
e.g. ssh -i StormNimbusServer_key.pem shubhamrohilla@13.82.135.53
or ssh -i StormNimbusServer_key.pem shubhamrohilla@srnimbus.eastus.cloudapp.azure.com

--------------------------------------------------------------------------------------------------------------------------------------

Meaning of ps -ef|grep processname ::

-e and -f are options to the ps command, and pipes take the output of one command and pass it as the input to another. 

Here is a full breakdown of this command:

ps - list processes
-e - show all processes, not just those belonging to the user
-f - show processes in full format (more detailed than default)
command 1 | command 2 - pass output of command 1 as input to command 2
grep find lines containing a pattern
processname - the pattern for grep to search for in the output of ps -ef
So altogether

ps -ef | grep processname
means: look for lines containing processname in a detailed overview/snapshot of all current processes, and display those lines.

--------------------------------------------------------------------------------------------------------------------------------------

Copying a file from local workstation to linux vm using scp:

scp -i <location of ssh key full path> <full path : file to move> username@<full server name / public IP Address>:~
e.g. shubhamrohilla@shubhamrohilla-mac azure % scp -i StormNimbusServer_key.pem /Users/shubhamrohilla/IdeaProjects/Storm_Testing_v1/target/Storm_Testing_v1-1.0-SNAPSHOT-jar-with-dependencies.jar shubhamrohilla@srnimbus.eastus.cloudapp.azure.com:~

Storm_Testing_v1-1.0-SNAPSHOT-jar-with-dependencies.jar                                                                     100%   53MB   1.8MB/s   00:29

--------------------------------------------------------------------------------------------------------------------------------------

Steps to setup and start Storm in linux VM:
---------------------------------------------------------------------------------------------------

1. Login to linux VM:
$ ssh -i StormNimbusServer_key.pem shubhamrohilla@srnimbus.eastus.cloudapp.azure.com

---------------------------------------------------------------------------------------------------

2. Install Apache Storm from the link : https://downloads.apache.org/storm/apache-storm-2.2.0/apache-storm-2.2.0.tar.gz
$ sudo wget https://downloads.apache.org/storm/apache-storm-2.2.0/apache-storm-2.2.0.tar.gz

---------------------------------------------------------------------------------------------------

3. Extract the tar file:
$ sudo tar -zxf apache-storm-2.2.0.tar.gz

---------------------------------------------------------------------------------------------------

4. Create directory for logs:
$ cd apache-storm-2.2.0
~/apache-storm-2.2.0$ mkdir data

---------------------------------------------------------------------------------------------------

5. Modify the Configuration file for Storm i.e. storm.yaml
~/apache-storm-2.2.0$ sudo vim conf/storm.yaml

Things to update : (Update it with my current storm.yaml file)

storm.zookeeper.servers:
 - "localhost"
storm.local.dir: “/path/to/storm/data(any path)”
nimbus.host: "localhost"
supervisor.slots.ports:
 - 6700
 - 6701
 - 6702
 - 6703

---------------------------------------------------------------------------------------------------

6. Start Zookeeper on 2181: (It'll occupy 3 ports - Client Server - 2181 (must set in zoo.cfg) Admin Server - 9876 (must set in zoo.cfg), ?? - 37069(randomly assigned))
/$ sudo /opt/zookeeper/bin/zkServer.sh start
~STARTED~

---------------------------------------------------------------------------------------------------

7. Start Nimbus Server: (It'll occupy port : 6627)
/$ sudo home/apache-storm-2.2.0/bin/storm nimbus
Running: java -server -Ddaemon.name=nimbus -Dstorm.options= -Dstorm.home=/home/apache-storm-2.2.0 -Dstorm.log.dir=/home/apache-storm-2.2.0/logs -Djava.library.path=/usr/local/lib:/opt/local/lib:/usr/lib:/usr/lib64 -Dstorm.conf.file= -cp /home/apache-storm-2.2.0/*:/home/apache-storm-2.2.0/lib/*:/home/apache-storm-2.2.0/extlib/*:/home/apache-storm-2.2.0/extlib-daemon/*:/home/apache-storm-2.2.0/conf -Xmx1024m -Djava.deserialization.disabled=true -Dlogfile.name=nimbus.log -Dlog4j.configurationFile=/home/apache-storm-2.2.0/log4j2/cluster.xml org.apache.storm.daemon.nimbus.Nimbus

---------------------------------------------------------------------------------------------------

8. Start Supervisor Server: (It'll occupy port : 6628)
/$ sudo home/apache-storm-2.2.0/bin/storm supervisor
Running: java -server -Ddaemon.name=supervisor -Dstorm.options= -Dstorm.home=/home/apache-storm-2.2.0 -Dstorm.log.dir=/home/apache-storm-2.2.0/logs -Djava.library.path=/usr/local/lib:/opt/local/lib:/usr/lib:/usr/lib64 -Dstorm.conf.file= -cp /home/apache-storm-2.2.0/*:/home/apache-storm-2.2.0/lib/*:/home/apache-storm-2.2.0/extlib/*:/home/apache-storm-2.2.0/extlib-daemon/*:/home/apache-storm-2.2.0/conf -Xmx256m -Djava.deserialization.disabled=true -Dlogfile.name=supervisor.log -Dlog4j.configurationFile=/home/apache-storm-2.2.0/log4j2/cluster.xml org.apache.storm.daemon.supervisor.Supervisor

---------------------------------------------------------------------------------------------------

9. Start Storm UI: (It'll occupy port : 6627)
/$ sudo home/apache-storm-2.2.0/bin/storm ui
Running: java -server -Ddaemon.name=ui -Dstorm.options= -Dstorm.home=/home/apache-storm-2.2.0 -Dstorm.log.dir=/home/apache-storm-2.2.0/logs -Djava.library.path=/usr/local/lib:/opt/local/lib:/usr/lib:/usr/lib64 -Dstorm.conf.file= -cp /home/apache-storm-2.2.0/*:/home/apache-storm-2.2.0/lib/*:/home/apache-storm-2.2.0/extlib/*:/home/apache-storm-2.2.0/extlib-daemon/*:/home/apache-storm-2.2.0/lib-webapp/*:/home/apache-storm-2.2.0/conf -Xmx768m -Djava.deserialization.disabled=true -Dlogfile.name=ui.log -Dlog4j.configurationFile=/home/apache-storm-2.2.0/log4j2/cluster.xml org.apache.storm.daemon.ui.UIServer

---------------------------------------------------------------------------------------------------

10. Check all the servers started:

shubhamrohilla@StormNimbusServer:/$ netstat -ltnp
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::37069                :::*                    LISTEN      -                   
tcp6       0      0 :::8080                 :::*                    LISTEN      -                   
tcp6       0      0 :::9876                 :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
tcp6       0      0 :::6627                 :::*                    LISTEN      -                   
tcp6       0      0 :::6628                 :::*                    LISTEN      -                   
tcp6       0      0 :::2181                 :::*                    LISTEN      -  

---------------------------------------------------------------------------------------------------

11. Copy the Jar file from local workstation to Linux VM:

shubhamrohilla@shubhamrohilla-mac azure % scp -i StormNimbusServer_key.pem /Users/shubhamrohilla/IdeaProjects/Storm_Testing_v1/target/Storm_Testing_v1-1.0-SNAPSHOT-jar-with-dependencies.jar shubhamrohilla@srnimbus.eastus.cloudapp.azure.com:~

Storm_Testing_v1-1.0-SNAPSHOT-jar-with-dependencies.jar                                                                     100%   53MB   1.8MB/s   00:29

---------------------------------------------------------------------------------------------------

