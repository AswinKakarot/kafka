Prerequisites
1. VirtualBox

2. Vagrant
Website: https://www.vagrantup.com/
Docs: https://www.vagrantup.com/docs/index.html
Download: https://releases.hashicorp.com/vagrant/2.0.1/vagrant_2.0.1_x86_64.deb?_ga=2.195067498.797000418.1515422389-1127522286.1512833876

	Steps for Installation
	1. wget https://releases.hashicorp.com/vagrant/2.0.1/vagrant_2.0.1_x86_64.deb?_ga=2.195067498.797000418.1515422389-1127522286.1512833876
	2. sudo dpkg -i vagrant_2.0.1_x86_64.deb

3. Kafka Vagrant Repository
https://github.com/eucuepo/vagrant-kafka

	Step for Installation
	1. Clone the Repository
	2. vagrant up
	3. vagrant status

	VM IP Mappings
	Name 	Address
	zookeeper1 	10.30.3.2
	zookeeper2 	10.30.3.3
	zookeeper3 	10.30.3.4
	broker1 	10.30.3.30
	broker2 	10.30.3.20
	broker3 	10.30.3.10

	Ports	
	Zookeeper servers bind to port 2181. Kafka brokers bind to port 9092.
	
	Cleanup
	vagrant destroy -f

Insights
Zookeeper
Shell
	$KAFKA_HOME/bin/zookeeper-shell.sh 10.30.3.2:2181

	ls /
[cluster, controller, controller_epoch, brokers, zookeeper, admin, isr_change_notification, consumers, log_dir_event_notification, latest_producer_id_block, config]

	ls /brokers/topics
[t1, t2, __consumer_offsets]

	ls /brokers/ids
[1, 2, 3]

Kafka
Create a topic
	 /vagrant/scripts/create-topic.sh test-one
Send data to the topic
	echo "Yet another line from stdin" | $KAFKA_HOME/bin/kafka-console-producer.sh \
	--topic test-one --broker-list 10.30.3.10:9092,10.30.3.20:9092,10.30.3.30:9092
Consume the data
	/vagrant/scripts/consumer.sh test-one

