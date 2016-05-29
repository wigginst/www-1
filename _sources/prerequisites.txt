Prerequisites
=============
In order to setup Hadoop properly in your local machine you need to first satisfy the following prerequisites in your environment.

1. Java

   Download Oracle JDK 8 from http://www.oracle.com/technetwork/java/javase/downloads/index.html
   Extract the archive to a folder named jdk1.8.0
   Set the following environment variables. (You can set the variables in the .bashrc file)

.. code-block:: bash

    JAVA_HOME=<path-to-jdk1.8.0-directory>
    PATH=$JAVA_HOME/bin:$PATH
    export JAVA_HOME PATH


2.  SSH and Rsync

    Install SSH and Rsync is not already installed in the environment.

.. code-block:: bash

    sudo apt-get install ssh
    sudo apt-get install rsync


3. Download and extract latest Hadoop binary into your machine. The latest hadoop binary files are available at http://hadoop.apache.org/releases.html. The following commands will download and extract Hadoop version 2.7.2.

.. code-block:: bash

    wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz
    tar -xzvf hadoop-2.7.2.tar.gz


4. Make sure everything was done properly. Execute the following command from the hadoop folder that we just extracted

.. code-block:: bash

    ./bin/hadoop