
Setting Up Apache Storm in ubuntu:

1. To setup Apache Storm - you need Java first.
cmd: java -version
if not installed then install java first.
cmd: sudo apt install default-jre

Snippet:
shubhamrohilla@StormNimbusServer:~$ java -version
openjdk version "11.0.10" 2021-01-19
OpenJDK Runtime Environment (build 11.0.10+9-Ubuntu-0ubuntu1.18.04)
OpenJDK 64-Bit Server VM (build 11.0.10+9-Ubuntu-0ubuntu1.18.04, mixed mode, sharing)

2. Now you have java, Storm requires Apache Zookeeper for coordination and storing the states of the worker nodes.
    a. Creating a user for Zookeeper:
        shubhamrohilla@StormNimbusServer:~$ sudo useradd zookeeper -m
        The -m flag creates a home directory for the user. In this case, it will be /home/zookeeper. To name the user differently, replace zookeeper with the name of your choice.
    b. Next, set bash as the default shell for the new user with the command:
        shubhamrohilla@StormNimbusServer:~$ sudo usermod --shell /bin/bash zookeeper
        usermod: no changes
    c. Set a password for the user:
        shubhamrohilla@StormNimbusServer:~$ sudo passwd zookeeper
        Enter new UNIX password: <zookepeer@123>
        Retype new UNIX password: <zookepeer@123>
        passwd: password updated successfully
    d. Then, add the user to the sudoers group for it to have sudo privileges:
        shubhamrohilla@StormNimbusServer:~$ sudo usermod -aG sudo zookeeper
    e. Check to verify that the user is now a superuser by listing the accounts in the sudoers group:
        shubhamrohilla@StormNimbusServer:~$ sudo getent group sudo
        sudo:x:27:shubhamrohilla,zookeeper
3. Creating a Zookeeper Data Directory: 
    Before installing ZooKeeper, create a directory structure where it can store configuration and state data (on a local disk or remote storage).
   a. To store the data on the local machine, first create a new ZooKeeper directory by running:
        shubhamrohilla@StormNimbusServer:~$ sudo mkdir -p /data/zookeeper
   b. Then, give the ZooKeeper user ownership to that directory:
        shubhamrohilla@StormNimbusServer:~$ sudo chown -R zookeeper:zookeeper /data/zookeeper
4. Downloading and Installing Zookeeper:
    Go to: https://zookeeper.apache.org/releases.html get the latest stable version http address.
    a. shubhamrohilla@StormNimbusServer:~$ cd /opt
    b.  Use the wget command to download the .tar file. Paste the link copied from the official Apache web page:
        shubhamrohilla@StormNimbusServer:/opt$ sudo wget https://apache.mirror.digitalpacific.com.au/zookeeper/zookeeper-3.7.0/apache-zookeeper-3.7.0-bin.tar.gz
    c. Extract the file by running:
        shubhamrohilla@StormNimbusServer:/opt$ sudo tar -xvf apache-zookeeper-3.7.0-bin.tar.gz
        Note: When extracting the file, the name of the ZooKeeper binary package will vary. Make sure it matches the file you downloaded.
    d. Rename the extracted file to zookeeper with the command:
        shubhamrohilla@StormNimbusServer:/opt$ sudo mv apache-zookeeper-3.7.0-bin zookeeper
    e. Give the zookeeper user ownership of that file by running:
        shubhamrohilla@StormNimbusServer:/opt$ sudo chown -R zookeeper:zookeeper /opt/zookeeper
5. Configuring Zookeeper in Standalone mode:
    The next step is creating a configuration file for ZooKeeper. The configuration below sets up ZooKeeper in standalone mode (used for developing and testing). For production environments, you need to run ZooKeeper in replication mode.
    To configure ZooKeeper in standalone mode, create a new zoo.cfg file in the zookeeper directory:
        shubhamrohilla@StormNimbusServer:/opt$ sudo nano /opt/zookeeper/conf/zoo.cfg
        Add the following lines:
        tickTime = 2000
        dataDir = /data/zookeeper
        clientPort = 2181
        initLimit = 5
        syncLimit = 2
        Bear in mind this is a basic configuration setting for a single node cluster. The file can differ according to your needs. The lines above consist of the following:
        tickTime: The number of milliseconds of each tick.
        dataDir: The directory where snapshots of the in-memory database and transaction log for updates are stored.
        clientPort: The port listening for client connections.
        initLimit: The number of ticks that the initial synchronization phase can take.
        syncLimit: The number of ticks that can pass between sending a request and getting an acknowledgement.
6. Starting the Zookeeper Service:
    Now, you can start the ZooKeeper service. Run the following command inside the /opt/zookeeper directory. If you exited out of the directory, navigate in it with cd /opt/zookeper.
    To start the ZooKeeper service use the command:
    shubhamrohilla@StormNimbusServer:/opt/zookeeper$ sudo bin/zkServer.sh start
    /usr/bin/java
    ZooKeeper JMX enabled by default
    Using config: /opt/zookeeper/bin/../conf/zoo.cfg
    Starting zookeeper ... STARTED
7. Connecting to Zookeeper server:
    Once you have started the service, you can connect to the ZooKeeper server.
    shubhamrohilla@StormNimbusServer:/opt/zookeeper$ sudo bin/zkCli.sh -server 127.0.0.1:2181
8. To close the session:
    [zk: 127.0.0.1:2181(CONNECTED) 1] quit
9. To stop the Zookeeper:
    shubhamrohilla@StormNimbusServer:/opt/zookeeper$ sudo bin/zkServer.sh stop
    /usr/bin/java
    ZooKeeper JMX enabled by default
    Using config: /opt/zookeeper/bin/../conf/zoo.cfg
    Stopping zookeeper ... STOPPED
10. Creting a System Service File:
    Finally, you need to create a service file to manage ZooKeeper.
    a. Create a new zookeeper.service file in a text editor of your choice:
     shubhamrohilla@StormNimbusServer:/$ sudo nano /etc/systemd/system/zookeeper.service
     File Content:
        [Unit]
        Description=Zookeeper Daemon
        Documentation=http://zookeeper.apache.org
        Requires=network.target
        After=network.target

        [Service]    
        Type=forking
        WorkingDirectory=/opt/zookeeper
        User=zookeeper
        Group=zookeeper
        ExecStart=/opt/zookeeper/bin/zkServer.sh start /opt/zookeeper/conf/zoo.cfg
        ExecStop=/opt/zookeeper/bin/zkServer.sh stop /opt/zookeeper/conf/zoo.cfg
        ExecReload=/opt/zookeeper/bin/zkServer.sh restart /opt/zookeeper/conf/zoo.cfg
        TimeoutSec=30
        Restart=on-failure

        [Install]
        WantedBy=default.target
    b. Reload the systemd service by running:
        shubhamrohilla@StormNimbusServer:/$ systemctl daemon-reload
        ==== AUTHENTICATING FOR org.freedesktop.systemd1.reload-daemon ===
        Authentication is required to reload the systemd state.
        Multiple identities can be used for authentication:
        1.  Ubuntu (shubhamrohilla)
        2.  zookeeper
        Choose identity to authenticate as (1-2): 2
        Password: 
        ==== AUTHENTICATION COMPLETE ===
    c. Then, start the ZooKeeper service and enable it to start on boot:
        Not working:
        shubhamrohilla@StormNimbusServer:/$ systemctl start zookeeper
        ==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
        Authentication is required to start 'zookeeper.service'.
        Multiple identities can be used for authentication:
        1.  Ubuntu (shubhamrohilla)
        2.  zookeeper
        Choose identity to authenticate as (1-2): 2
        Password: 
        ==== AUTHENTICATION COMPLETE ===
        Job for zookeeper.service failed because the control process exited with error code.
        See "systemctl status zookeeper.service" and "journalctl -xe" for details.

        

