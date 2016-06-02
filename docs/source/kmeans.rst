K-Means
=======

This section describes how to implement K-means algorithm using Hadoop.

Pseudo Code
------------------
Denote:
- N is the number of data points
- M is the number of centroids
- D is the dimension of centroids
- Vi refers to the ith data point(vector)
- Cj refers to the jth centroid

------------------
The Main Method
------------------

.. code-block:: java

    generate N data points (D dimensions)
    write to HDFS
    generate M centroids
    write to HDFS
    for iterations{
        configure job
        launch job
    }


------------------
The Mapper
------------------

.. code-block:: java

    load centroids

    #The value of the input key-value pair is a data point Vi
    find the nearest centroid Cj for the data point Vi
    Context.write(j, <Vi, 1>)


------------------
The Reducer
------------------

.. code-block:: java

    #The key is an ID of a centroid, the value list is a list of <Vi, 1>
    newCentroid = a new D dimensional vector
    count = 0
    for each pair <Vi, 1> in the value list{
        for k in 0 to (D-1) {
            newCentroid[k] += Vi[k]
        }
        count += 1
    }

    for k in 0 to (D-1) {
            newCentroid[k] /= count
    }

    Context.write(key, newCentroid)



Compile the Code
------------------
The code is available at https://github.com/ADMIcloud/examples. Download the code by using git clone command or by clicking the Download Zip button. The go to the HadoopKmeans directory and compile the code.

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

It wil firstly generate 100 data points, each one is a 20 dimensional vector. The data will be stored in <localInputDir> directory. Then the data will be copied to HDFS. It then generate 10 centroids and write them to HDFS. For every iteration, it loads centroids and reads key-value pairs to do computation. And then write new centroids back to HDFS.


View the Results
------------------

.. code-block:: bash

    $ hdfs dfs -ls test-my-k

