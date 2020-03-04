.. _openfoam:

OpenFOAM
========

About
-----

OpenFOAM is a popular engineering application toolbox. It's open source and is used for simulating fluid flow around objects. 

Workflow
--------

Installing OpenFOAM with Gridware
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: The flight environment will need to be activated before the environments can be created so be sure to run ``flight start`` or `setup your environment to automatically activate the flight environment <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment>`_.

- Create a gridware software environment::

    [flight@gateway1 (scooby) ~]$ flight env create gridware

- Activate the environment::

    [flight@gateway1 (scooby) ~]$ flight env activate gridware

- Locate available OpenFOAM versions::

    <gridware> [flight@gateway1 (scooby) ~]$ gridware search openfoam

- Install OpenFOAM 4.1::

    <gridware> [flight@gateway1 (scooby) ~]$ gridware install apps/openfoam/4.1

