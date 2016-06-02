Apache Storm Word Count
================

Apache Storm is a distributed stream processing engine.

These are the things we will look at in this Tutorial.

* Download Apache Storm
* Set it up on your machine

Download storm
--------------

wget http://mirrors.ibiblio.org/apache/storm/apache-storm-0.10.1/apache-storm-0.10.1.tar.gz

tar -xvf apache-storm-0.10.1.tar.gz

Download and start ZooKeeper
------------------

wget http://apache.mirrors.pair.com/zookeeper/zookeeper-3.4.8/zookeeper-3.4.8.tar.gz

tar -xvf zookeeper-3.4.8.tar.gz

cd zookeeper-3.4.8

cp conf/zoo_sample.cfg conf/zoo.cfg

./bin/zkServer.sh start


Start Storm Cluster on Local machine
------------------------------------

cd ../apache-storm-0.10.1

In one terminal start the nimbus server

./bin/storm nimbus

In another terminal start the supervisor

./bin/storm supervisor

In the 3rd terminal start the Storm Web UI

./bin/storm ui

Above command will start the Storm UI. You can visit

http://localhost:8080/index.html

to view the storm cluster.

Word Count example
------------------

Word count is a simple streaming example where storm keeps track of the words and their counts streaming in. This example
is included in the Storm distribution. The source code of the example can be found in

examples/storm-starter/src/jvm/storm/starter/WordCountTopology.java

In this example there are three processing units arranged in the graph.

RandomSentenceSpout (spout) --> SplitSentence (bolt) --> WordCount (bolt)

RandomSentenceSpout generates random sentnces. SplitSentence splits these sentences into words. These words are sent to
WordCount bolt where the count is kept.

Run the example word count
--------------------------

Now open another termial to run a Storm example word count

./bin/storm jar examples/storm-starter/storm-starter-topologies-0.10.1.jar storm.starter.WordCountTopology WordCount

You can view the topology by going to the web browser.

http://localhost:8080/index.html

To kill the topology use the command

./bin/storm kill WordCount


