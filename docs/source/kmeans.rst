K-Means
=======

This section describes how to implement K-means algorithm using Hadoop.

.. image:: images/figures/hadoopkmeans.png
   :height: 300px
   :width: 520px
   :alt: hadoop kmeans
   :align: center

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

    generate N data points (D dimensions), write to HDFS
    generate M centroids, write to HDFS
    for iterations{
        configure a job
        launch the job
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

    output newCentroid to HDFS



Compile the Code
------------------
The code is available at https://github.com/ADMIcloud/examples. Download the code by using git clone command or by clicking the Download Zip button. The go to the HadoopKmeans directory and compile the code.
In the build.xml, change "PATH-TO-YOUR-HADOOP-HOME" to your Hadoop Home directory.

.. code-block:: xml

    <project name="hadoopCompile" default="jar" basedir=".">
        <target name="init">
	        <property name="sourceDir" value="."/>
	        <property name="outputDir" value="classes"/>
	        <property name="buildDir" value="jar"/>
	        <property name="lib.dir" value="PATH-TO-YOUR-HADOOP-HOME"/>
	        <path id="classpath">
		        <fileset dir="${lib.dir}" includes="**/*.jar"/>
	        </path>
        </target>
        <target name="clean" depends="init">
	        <delete dir="${outputDir}"/>
	        <delete dir="${buildDir}"/>
        </target>
        <target name="prepare" depends="clean">
	        <mkdir dir="${outputDir}"/>
	        <mkdir dir="${buildDir}"/>
        </target>
        <target name="compile" depends="prepare">
	        <javac srcdir="${sourceDir}" destdir="${outputDir}" classpathref="classpath"/>
        </target>
        <target name="jar" depends="compile">
	        <jar destfile="${buildDir}/hadoopkmeans.jar" basedir="${outputDir}">
		        <manifest>
			        <attribute name="Main-Class" value="admicloud.kmeans.mapreduce.KmeansMain"/>
		        </manifest>
	        </jar>
        </target>
    </project>


.. code-block:: bash

    $ cd HadoopKmeans
    $ ant



Run the Code
------------------
The usage is

.. code-block:: bash

    $ hadoop jar jar/hadoopkmeans.jar <num Of Data Points> <size of a vector> <num of Centroids> <number of map tasks> <number of iteration>

For example

.. code-block:: bash

    $ hadoop jar jar/hadoopkmeans.jar 100 3 10 2 3

It wil firstly generate 100 data points, each one is a 3-D vector. The data will be saved to HDFS. It then generate 10 initial centroids and write them to HDFS. For every iteration, it loads centroids and reads key-value pairs to do computation. And then write new centroids back to HDFS.


View the Results
------------------

.. code-block:: bash

    $ hdfs dfs -ls -R kmeans

