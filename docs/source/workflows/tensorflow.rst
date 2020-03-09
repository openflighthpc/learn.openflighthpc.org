.. _tensorflow:

Tensorflow
==========

About
-----

Tensorflow is an open-source machine learning platform. It provides an ecosystem of tools and libraries that allow researchers to build and deploy machine learning applications.

Workflow 1: Singularity
-----------------------

Installing Tensorflow with Singularity
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: The flight environment will need to be activated before the environments can be created so be sure to run ``flight start`` or `setup your environment to automatically activate the flight environment <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment>`_.

- Create a singularity software environment::

    [flight@gateway1 (scooby) ~]$ flight env create singularity

- Activate the environment::

    [flight@gateway1 (scooby) ~]$ flight env activate singularity

Running the Job
^^^^^^^^^^^^^^^

- Download the example job models::

    <singularity> [flight@gateway1 (scooby) ~]$ git clone https://github.com/tensorflow/models.git

- Launch the tensorflow docker container with singularity to run the job::

    <singularity> [flight@gateway1 (scooby) ~]$ singularity exec docker://tensorflow/tensorflow:1.15.0 python ./models/tutorials/image/mnist/convolutional.py

Workflow 2: Conda
-----------------

.. note:: The flight environment will need to be activated before the environments can be created so be sure to run ``flight start`` or `setup your environment to automatically activate the flight environment <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment>`_.

Installing TensorFlow with Conda
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Create a conda software environment::

    [flight@gateway1 (scooby) ~]$ flight env create conda

- Activate the environment::

    [flight@gateway1 (scooby) ~]$ flight env activate conda

- Create a Python environment for tensorflow::

    <conda> [flight@gateway1 (scooby) ~]$ conda create -n tensorflow python=3.6

- Activate the Python environment::

    <conda> [flight@gateway1 (scooby) ~]$ source activate tensorflow

- Install the tensorflow package::

    <conda> [flight@gateway1 (scooby) ~]$ pip install tensorflow==1.15

Running the Job
^^^^^^^^^^^^^^^

- Download the example job models::

    <conda> [flight@gateway1 (scooby) ~]$ git clone https://github.com/tensorflow/models.git

- Execute the job with python::

    <conda> [flight@gateway1 (scooby) ~]$ python ./models/tutorials/image/mnist/convolutional.py

