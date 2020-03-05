.. _jupyter-notebook:

Jupyter Notebook
================

About
-----

Jupyter Notebooks are a web-based development and visualisation environment. It provides flexible integration of notebooks, code and data in a portable and secure manner.

Workflow
--------

Installing Jupyter with Conda
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: The flight environment will need to be activated before the environments can be created so be sure to run ``flight start`` or `setup your environment to automatically activate the flight environment <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment>`_.

- Create a conda software environment::

    [flight@gateway1 (scooby) ~]$ flight env create conda

- Activate the environment::

    [flight@gateway1 (scooby) ~]$ flight env activate conda

- Install Jupyter::

    <conda> [flight@gateway1 (scooby) ~]$ conda install jupyter

Launch a Jupyter Notebook
^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: These commands will need to be run from a graphical desktop session as it will launch a web browser. This is out of scope for this documentation, for more information on launching desktops, see the `use documentation <https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-desktop.html#launch-a-desktop-session>`_

- Download the example notebook::

    <conda> [flight@gateway1 (scooby) ~]$ curl -L http://tiny.cc/jupyterexample > ipython.ipynb

- Launch the notebook::

    <conda> [flight@gateway1 (scooby) ~]$ jupyter notebook ipython.ipynb

- A web browser will launch with the notebook displayed

    .. image:: jupyter_notebook_1.png
       :alt: Jupyter Notebook Web Browser

