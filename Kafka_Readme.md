# Create a VM in Azure #
1. Create a Resource - VM
2. Download the .pem private key.

<hr>

How to Connect with VM: ssh -i KafkaTesting_key.pem azureuser@20.106.150.2

Ensure you have given read-only access to the private key : chmod 400 KafkaTesting_key.pem

Generic Command to generate a public key corresponding to your private key:
ssh-keygen \
    -m PEM \
    -t rsa \
    -b 4096 \
    -C "azureuser@myserver" \
    -f ~/.ssh/mykeys/myprivatekey \
    -N mypassphrase

Command used:

ssh-keygen -m PEM -t rsa -b 4096 -C "azureuser@168.61.49.221" -f /Users/shubhamrohilla/Documents/Shubham/azure/myprivatekey -N kafkapass


# Installing Kafka # : 

Following: https://www.digitalocean.com/community/tutorials/how-to-install-apache-kafka-on-ubuntu-20-04


To follow along, you will need:

1. One Ubuntu 20.04 server and a non-root user with sudo privileges. Follow the steps specified in this guide if you do not have a non-root user set up.
2. At least 4GB of RAM on your server. Installations without this amount of RAM may cause the Kafka service to fail.
3. OpenJDK 11 installed on your server. To install this version, follow our tutorial How To Install Java with APT on Ubuntu 20.04. Kafka is written in Java, so it requires a JVM.

# Download openJDK11 to your new VM #

1. Connect to the VM : ssh -i KafkaTesting_key.pem azureuser@168.61.49.221
2. To install this version, first update the package index: sudo apt update
3. Next, check if Java is already installed: java -version
4. If not found : sudo apt install default-jre - this will install openJDK11
5. check for java -version:
    azureuser@KafkaTesting:~$ java -version
    openjdk version "11.0.11" 2021-04-20
    OpenJDK Runtime Environment (build 11.0.11+9-Ubuntu-0ubuntu2.18.04)
    OpenJDK 64-Bit Server VM (build 11.0.11+9-Ubuntu-0ubuntu2.18.04, mixed mode, sharing)
6.You may need the Java Development Kit (JDK) in addition to the JRE in order to compile and run some specific Java-based software. To install the JDK, execute the following command, which will also install the JRE: sudo apt install default-jdk
7. Verify install JDK: javac -version
    azureuser@KafkaTesting:~$ javac -version
    javac 11.0.11


# Installing Apache Kafka in your Linux Machine #
1. **Creating a User for Kafka** : Because Kafka can handle requests over a network, your first step is to create a dedicated user for the service. This minimizes damage to your Ubuntu machine in the event that someone compromises the Kafka server. We will create a dedicated kafka user in this step.

    a. Logged in as your non-root sudo user, create a user called kafka: sudo adduser kafka
    Console:
        azureuser@KafkaTesting:~$ sudo adduser kafka
    Adding user `kafka' ...
    Adding new group `kafka' (1001) ...
    Adding new user `kafka' (1001) with group `kafka' ...
    Creating home directory `/home/kafka' ...
    Copying files from `/etc/skel' ...
    Enter new UNIX password: 
    Retype new UNIX password: 
    passwd: password updated successfully
    Changing the user information for kafka
    Enter the new value, or press ENTER for the default
            Full Name []: 
            Room Number []: 
            Work Phone []: 
            Home Phone []: 
            Other []: 
    Is the information correct? [Y/n] Y
    Password: kafka123

    b. Add the kafka user to the sudo group with the adduser command. You need these privileges to install Kafka’s dependencies: sudo adduser kafka sudo
    azureuser@KafkaTesting:~$ sudo adduser kafka sudo
    Adding user `kafka' to group `sudo' ...
    Adding user kafka to group sudo
    Done.

    c. Your kafka user is now ready. Log into the account using su: su -l kafka
    azureuser@KafkaTesting:~$ su -l kafka
    Password: 
    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

2. **Downloading and Extracting the Kafka Binaries** : 
    a. Let’s download and extract the Kafka binaries into dedicated folders in our kafka user’s home directory. To start, create a directory in /home/kafka called Downloads to store your downloads: mkdir ~/Downloads
    b. Use curl to download the Kafka binaries: curl "https://downloads.apache.org/kafka/2.8.0/kafka_2.12-2.8.0.tgz" -o ~/Downloads/kafka.tgz
    c. Create a new Directory for Kafka: mkdir ~/kafka and move to this directory : cd kafka
    d. Extract the archive you downloaded using the tar command: tar -xvzf ~/Downloads/kafka.tgz --strip 1 
        We specify the --strip 1 flag to ensure that the archive’s contents are extracted in ~/kafka/ itself and not in another directory (such as ~/kafka/kafka_2.13-2.6.0/) inside of it.

3. **Configuring Kafka Servers** :
    a. Kafka’s default behavior will not allow you to delete a topic. A Kafka topic is the category, group, or feed name to which messages can be published. To modify this, you must edit the configuration file. Kafka’s configuration options are specified in server.properties. Open this file with nano or your favorite editor: nano ~/kafka/config/server.properties
    b. First, add a setting that will allow us to delete Kafka topics. Add the following to the bottom of the file: delete.topic.enable = true
    c. Second, change the directory where the Kafka logs are stored by modifying the logs.dir property: log.dirs=/home/kafka/logs

4. **Creating Systemd Unit Files and Starting the Kafka Server** :
    a. In this section, you will create systemd unit files for the Kafka service. This will help you perform common service actions such as starting, stopping, and restarting Kafka in a manner consistent with other Linux services.
    b. Create the unit file for zookeeper: sudo nano /etc/systemd/system/zookeeper.service
    c. create the systemd service file for kafka: sudo nano /etc/systemd/system/kafka.service
        i) The [Unit] section specifies that this unit file depends on zookeeper.service. This will ensure that zookeeper gets started automatically when the kafka service starts.
        ii) The [Service] section specifies that systemd should use the kafka-server-start.sh and kafka-server-stop.sh shell files for starting and stopping the service. It also specifies that Kafka should be restarted if it exits abnormally.
        iii) Start Kafka : sudo systemctl start kafka
        iv) To ensure that the server has started successfully, check the journal logs for the kafka unit: sudo systemctl status kafka
            azureuser@KafkaTesting:~$ sudo systemctl status kafka
            ● kafka.service
            Loaded: loaded (/etc/systemd/system/kafka.service; disabled; vendor preset: enabled)
            Active: active (running) since Sat 2021-07-24 09:52:00 UTC; 34s ago
            Main PID: 1731 (sh)
                Tasks: 72 (limit: 4915)
            CGroup: /system.slice/kafka.service
                    ├─1731 /bin/sh -c /home/kafka/kafka/bin/kafka-server-start.sh /home/kafka/kafka/config/server.properties > /home/kafka/kafka/kafka.log 2>&1
                    └─1742 java -Xmx1G -Xms1G -server -XX:+UseG1GC -XX:MaxGCPauseMillis=20 -XX:InitiatingHeapOccupancyPercent=35 -XX:+ExplicitGCInvokesConcurrent -XX:MaxInlineLevel=15 -Djava.awt.headles

            Jul 24 09:52:00 KafkaTesting systemd[1]: Started kafka.service. :: You now have a Kafka server listening on port 9092.
        v) You have started the kafka service. But if you rebooted your server, Kafka would not restart automatically. To enable the kafka service on server boot, run the following commands: 
            i) sudo systemctl enable zookeeper
                azureuser@KafkaTesting:~$ sudo systemctl enable zookeeper
                Created symlink /etc/systemd/system/multi-user.target.wants/zookeeper.service → /etc/systemd/system/zookeeper.service.
            ii) sudo systemctl enable kafka
                azureuser@KafkaTesting:~$ sudo systemctl enable kafka
                Created symlink /etc/systemd/system/multi-user.target.wants/kafka.service → /etc/systemd/system/kafka.service.
            

5. **Testing the Kafka Installation** :
    a) In this step, you will test your Kafka installation. Specifically, you will publish and consume a “Hello World” message to make sure the Kafka server is behaving correctly. Publishing messages in Kafka requires:
        i) A producer, who enables the publication of records and data to topics.
        ii) A consumer, who reads messages and data from topics.
        iii) To begin, create a topic named TutorialTopic:
            kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic TutorialTopic
            bin/kafka-topics.sh --create --topic TutorialTopic --bootstrap-server localhost:9092 -- worked
            Describe Topic: bin/kafka-topics.sh --describe --topic TutorialTopic --bootstrap-server localhost:9092
        iv) You can create a producer from the command line using the kafka-console-producer.sh script. It expects the Kafka server’s hostname, a port, and a topic as arguments. Now publish the string "Hello, World" to the TutorialTopic topic:
            echo "Hello, World" | bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TutorialTopic > /dev/null
        v) Next, create a Kafka consumer using the kafka-console-consumer.sh script. It expects the ZooKeeper server’s hostname and port, along with a topic name as arguments. The following command consumes messages from TutorialTopic. Note the use of the --from-beginning flag, which allows the consumption of messages that were published before the consumer was started:
            bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TutorialTopic --from-beginning
            azureuser@KafkaTesting:/home/kafka/kafka$ bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TutorialTopic --from-beginning
            Hello, World
        vi) Open new Terminal: echo "Hello World from Shubham Rohilla!!" | bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TutorialTopic > /dev/null

6. **Installing KafkaT (Optional)** : 
    KafkaT is a tool that Airbnb developed. It makes it easier to view details about your Kafka cluster and perform certain administrative tasks from the command line. But because it is a Ruby gem, you will need Ruby to use it. You will also need the build-essential package to build the other gems that KafkaT depends on. Install them using apt:
    sudo apt install ruby ruby-dev build-essential
    You can now install KafkaT using the gem command: sudo CFLAGS=-Wno-error=format-overflow gem install kafkat
        The “Wno-error=format-overflow” compilation flag is required to suppress Zookeeper’s warnings and errors during kafkat’s installation process.
        KafkaT uses .kafkatcfg as the configuration file to determine the installation and log directories of your Kafka server. It should also have an entry pointing KafkaT to your ZooKeeper instance.
    Create a new file called .kafkatcfg: nano ~/.kafkatcfg
    nano ~/.kafkatcfg
    You are now ready to use KafkaT. For a start, here’s how you would use it to view details about all Kafka partitions:

    kafkat partitions

# Configuring DNS in Azure #

DNS Name:  kafkatesting
VM Server address : kafkatesting.eastus.cloudapp.azure.com

Kafka server: http://kafkatesting.eastus.cloudapp.azure.com:9092
Zookeeper Server: http://kafkatesting.eastus.cloudapp.azure.com:2181

----------------------------------------------------------------

1. start vm: ssh -i KafkaTesting_key.pem azureuser@kafkatesting.eastus.cloudapp.azure.com
2. create kafka topic: kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic SampleTopic
3. rm /path/to/dir/*
4. Create a Consumer: bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic SampleTopic_2 --from-beginning

To be added in server.properties:
listeners=PLAINTEXT://:9092
advertised.listeners=PLAINTEXT://localhost:9092

cluster id: JkmvCUxpSuuFvHB-N0gWkA
/home/kafka/kafka/zk_logs/


--------------------------------------------------------------------------------------------------------------------------

# Installing Confluent Platform on the VM #

*https://www.tutorialkart.com/apache-kafka/kafka-confluent/*

1. Install Confluent public key : wget -qO – http://packages.confluent.io/deb/3.3/archive.key | sudo apt-key add –

1. Download Confluent Platform on your local system : confluent.io/installation

Copy the file to VM : scp -i KafkaTesting_key.pem /Users/shubhamrohilla/Downloads/confluent-6.2.0.zip azureuser@20.106.150.2:~

Move the file to the specific location : sudo mv confluent-6.2.0.zip /home/confluentPlatform

unzip the zip file : sudo unzip confluent-6.2.0.zip

--- updated control-center.properties
bootstrap.servers=20.106.150.2:9093
zookeeper.connect=20.106.150.2:2186
confluent.controlcenter.schema.registry.url=http://localhost:447
# KSQL cluster URL
#confluent.controlcenter.ksql.<ksql-cluster-name>.url=http://localhost:8088

-- server.properties
listeners=PLAINTEXT://:9093
advertised.listeners=PLAINTEXT://20.106.150.2:9093
zookeeper.connect=localhost:2186

-- zookeeper.properties
clientPort=2186
admin.serverPort=8082

--schema-registry.properties
listeners=http://0.0.0.0:447
kafkastore.bootstrap.servers=PLAINTEXT://localhost:9093


check for the available ports if not occupied: netstat -ltnp
azureuser@KafkaTesting:~$ netstat -ltnp
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
tcp6       0      0 :::35875                :::*                    LISTEN      -                   
tcp6       0      0 :::9092                 :::*                    LISTEN      -                   
tcp6       0      0 :::2181                 :::*                    LISTEN      -                   
tcp6       0      0 :::33869                :::*                    LISTEN      -         

Run Zookeeper:
azureuser@KafkaTesting:/home/confluentPlatform/confluent-6.2.0$ sudo bin/zookeeper-server-start etc/kafka/zookeeper.properties

Run Kafka:
azureuser@KafkaTesting:/home/confluentPlatform/confluent-6.2.0$ sudo bin/kafka-server-start etc/kafka/server.properties

[2021-08-08 09:40:09,382] WARN [Producer clientId=ConfluentBalancerSampleStoreProducer] Bootstrap broker 20.106.150.2:9093 (id: -1 rack: null) disconnected (org.apache.kafka.clients.NetworkClient)
[2021-08-08 09:40:11,161] INFO [AdminClient clientId=kafka-cruise-control] Metadata update failed (org.apache.kafka.clients.admin.internals.AdminMetadataManager)


Run Schema Registry : 
azureuser@KafkaTesting:/home/confluentPlatform/confluent-6.2.0$ sudo bin/schema-registry-start etc/schema-registry/schema-registry.properties

[2021-08-08 09:46:06,818] INFO Adding listener: http://0.0.0.0:447 (io.confluent.rest.ApplicationServer:384)

azureuser@KafkaTesting:~$ netstat -ltnp
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::42931                :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
tcp6       0      0 :::32889                :::*                    LISTEN      -                   
tcp6       0      0 :::8090                 :::*                    LISTEN      -                   
tcp6       0      0 :::35875                :::*                    LISTEN      -                   
tcp6       0      0 :::9092                 :::*                    LISTEN      -                    :: Normal Kafka Broker
tcp6       0      0 :::9093                 :::*                    LISTEN      -                    :: Confluent Platform Kafka Broker
tcp6       0      0 :::2181                 :::*                    LISTEN      -                    :: Normal Zookeeper
tcp6       0      0 :::2186                 :::*                    LISTEN      -                    :: Confluent Platform Zookeeper
tcp6       0      0 :::33869                :::*                    LISTEN      -                   
tcp6       0      0 :::39471                :::*                    LISTEN      -      