.. _bowtie:

Bowtie
======

About
-----

Bowtie is a sequencing toolset for aligning sets of DNA into large genomes.

Workflow
--------

Installing Bowtie with Spack
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: The flight environment will need to be activated before the environments can be created so be sure to run ``flight start`` or `setup your environment to automatically activate the flight environment <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment>`_.

- Create a spack software environment::

    [flight@gateway1 (scooby) ~]$ flight env create spack

- Activate the environment::

    [flight@gateway1 (scooby) ~]$ flight env activate spack

- Install bowtie::

    <spack> [flight@gateway1 (scooby) ~]$ spack install bowtie

Running a Bowtie Job
^^^^^^^^^^^^^^^^^^^^

- Download example ecoli data::

    <spack> [flight@gateway1 (scooby) ~]$ wget -O ecoli.fq http://tiny.cc/ecoli

- Create a job script in the current working directory::

    <spack> [flight@gateway1 (scooby) ~]$ cat << EOF > mybowtiejob.sh
    #!/bin/bash -l
    #SBATCH -N 1
    flight env activate spack
    spack load bowtie
    bowtie-build ecoli.fq e_coli
    EOF

- Submit the job to the queue::

    <spack> [flight@gateway1 (scooby) ~]$ sbatch mybowtiejob.sh

The results can then be reviewed from the slurm output file for the job in the current working directory. 
