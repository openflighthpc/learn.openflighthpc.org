.. _openfoam:

OpenFOAM
========

About
-----

OpenFOAM is a popular engineering application toolbox. It's open source and is used for simulating fluid flow around objects. 

.. image:: openfoam_about_1.png
   :alt: OpenFOAM Output Example

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

.. note:: After pressing 'y' to accept the installation. Gridware will install various dependencies for OpenFOAM to ensure it runs

Checking OpenFOAM is Working
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Load the OpenFOAM module::

    <gridware> [flight@gateway1 (scooby) ~]$ module load apps/openfoam

- Check an OpenFOAM command can be seen by viewing the help page::

    <gridware> [flight@gateway1 (scooby) ~]$ icoFoam -help

Running a Simple OpenFOAM Job
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Create a job script in the current working directory::

    <gridware> [flight@gateway1 (scooby) ~]$ cat << 'EOF' > myfoamjob.sh
    #!/bin/bash
    #SBATCH -N 1

    # Activate environment and load OpenFOAM module
    flight env activate gridware
    module load apps/openfoam

    # Create job directory from example job
    cp -r $FOAM_TUTORIALS/incompressible/icoFoam/cavity/cavity $HOME/.
    cd $HOME/cavity

    # Calculate fluid pressure with OpenFOAM tools
    blockMesh
    checkMesh
    icoFoam
    EOF

- Submit the job to the queue system::

    <gridware> [flight@gateway1 (scooby) ~]$ sbatch myfoamjob.sh

- Check that the job is running (iit will take 1-2 minutes to complete)::

    <gridware> [flight@gateway1 (scooby) ~]$ squeue

Viewing the Results
^^^^^^^^^^^^^^^^^^^

Once the cavity job has finished running, the results can be visualised through a desktop session.

- Connect to VNC desktop (this is out of scope for this documentation, for more information on launching desktops, see the `use documentation <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-desktop.html#launch-a-desktop-session>`_)

- In a terminal on the desktop session, ensure that the OpenFOAM module is loaded::

    [flight@gateway1 (scooby) ~]$ flight env activate gridware
    <gridware> [flight@gateway1 (scooby) ~]$ module load apps/openfoam

- Navigate to the cavity directory and launch the paraFoam viewer::

    <gridware> [flight@gateway1 (scooby) ~]$ cd cavity
    <gridware> [flight@gateway1 (scooby) cavity]$ paraFoam

- In the window that opens, scroll down to "Mesh parts" and select all the boxes, then click apply

    .. image:: openfoam_parafoam_1.png
       :alt: paraFoam View 1

- Next, change the display to 'U' in the dropdown menu, click play to change the timestamp and then click and drag to rotate the subject

    .. image:: openfoam_parafoam_2.png
       :alt: paraFoam View 2

