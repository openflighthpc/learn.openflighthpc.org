.. _hadoop:

Hadoop
======

About
-----

Hadoop is a scalable, distributed computing solution provided by Apache. Similar to queuing systems, Hadoop allows for distributed processing of large data sets.

Workflow
--------

Installing Hadoop Manually to Shared Filesystem
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Install dependencies for Hadoop (press 'y' to confirm the installation when prompted)::

    [flight@gateway1 (scooby) ~]$ sudo yum install java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64

- Download Hadoop v3.2.1::

    [flight@gateway1 (scooby) ~]$ wget -O /tmp/hadoop.tgz http://tiny.cc/hadoop321

- Decompress the Hadoop installation to shared storage::

    [flight@gateway1 (scooby) ~]$ cd /opt/apps
    [flight@gateway1 (scooby) ~]$ tar xzf /tmp/hadoop.tgz

- Edit line 54 in ``/opt/apps/hadoop-3.2.1/etc/hadoop/hadoop-env.sh`` to point to the Java installation as follows::

    export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64/jre

Downloading the Hadoop Job
^^^^^^^^^^^^^^^^^^^^^^^^^^

These steps help setup the Hadoop environment and download a spreadsheet of data which will Hadoop will sort into sales units per region.

- Download and source Hadoop environment variables::

    [flight@gateway1 (scooby) ~]$ wget https://tinyurl.com/hadoopenv
    [flight@gateway1 (scooby) ~]$ source hadoopenv

- Create job directory::

    [flight@gateway1 (scooby) ~]$ mkdir MapReduceTutorial
    [flight@gateway1 (scooby) ~]$ chmod 777 MapReduceTutorial

- Download job data::

    [flight@gateway1 (scooby) ~]$ cd MapReduceTutorial
    [flight@gateway1 (scooby) MapReduceTutorial]$ wget -O hdfiles.zip https://tinyurl.com/hdinput1
    [flight@gateway1 (scooby) MapReduceTutorial]$ unzip -j hdfiles.zip

- Check that job data files are present::

    [flight@gateway1 (scooby) MapReduceTutorial]$ ls
    desktop.ini  hdfiles.zip  SalesCountryDriver.java  SalesCountryReducer.java  SalesJan2009.csv  SalesMapper.java

Preparing the Hadoop Job
^^^^^^^^^^^^^^^^^^^^^^^^

- Compile java for job::

    [flight@gateway1 (scooby) MapReduceTutorial]$ javac -d . SalesMapper.java SalesCountryReducer.java SalesCountryDriver.java

- Create a manifest file::

    [flight@gateway1 (scooby) MapReduceTutorial]$ echo "Main-Class: SalesCountry.SalesCountryDriver" >> Manifest.txt

- Compile the final java file for job::

    [flight@gateway1 (scooby) MapReduceTutorial]$ jar cfm ProductSalePerCountry.jar Manifest.txt SalesCountry/*.class

Starting the Hadoop Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Start the Hadoop distributed file system service::

    [flight@gateway1 (scooby) MapReduceTutorial]$ $HADOOP_HOME/sbin/start-dfs.sh

- Start the resource manager, node manager and app manager service::

    [flight@gateway1 (scooby) MapReduceTutorial]$ $HADOOP_HOME/sbin/start-yarn.sh

- Create directory for processing data and copy sales results in::

    [flight@gateway1 (scooby) MapReduceTutorial]$ mkdir ~/inputMapReduce
    [flight@gateway1 (scooby) MapReduceTutorial]$ cp SalesJan2009.csv ~/inputMapReduce/

- Load the data into the distributed file system::

    [flight@gateway1 (scooby) MapReduceTutorial]$ $HADOOP_HOME/bin/hdfs dfs -ls ~/inputMapReduce

Running the Hadoop Job
^^^^^^^^^^^^^^^^^^^^^^

- Execute the MapReduce job::

    [flight@gateway1 (scooby) MapReduceTutorial]$ $HADOOP_HOME/bin/hadoop jar ProductSalePerCountry.jar ~/inputMapReduce ~/mapreduce_output_sales


- View the job results::

    [flight@gateway1 (scooby) MapReduceTutorial]$ $HADOOP_HOME/bin/hdfs dfs -cat ~/mapreduce_output_sales/part-00000 | more

