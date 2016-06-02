K-Means
=======

This section describes how to implement K-means algorithm using Hadoop.

The Main Method
------------------


The Mapper
------------------


The Reducer
------------------


Compile the Code
------------------
The code is available at https://github.com/ADMIcloud/examples. Download the code by using git clone command or by clicking the Download Zip buttion. The go to the HadoopKmeans directory and compile the code.

.. code-block:: bash

    $ cd HadoopKmeans
    $ ant



Run the Code
------------------
The usage is

.. code-block:: bash

    $ hadoop jar jar/hadoopkmeans.jar  <numOfDataPoints> <num of Centroids> <number of map tasks> <number of iteration> <localInputDir>

Here <localInputDir> is a directory where you want to store the data point files generated at the beginning of the code.

For example

.. code-block:: bash

    $ hadoop jar jar/hadoopkmeans.jar  100 10 2 5 input

It wil firstly generate 100 data points, each one is a 20 dimension vector. The data will be stored in <localInputDir> directory. Then generate 10 centroids and write them to HDFS. For every iteration, it loads centroids and reads key-value pairs to do computation. And then write new centroids back to HDFS.


View the Results
------------------

.. code-block:: bash

    $ hdfs dfs -ls test-my-k

