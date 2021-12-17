.. _ORCAsetup:

-----
ORCA
-----

This guide deal with setup ORCA package in 
paramshakti supercomputing facility in user's
own account


.. contents::

Getting the Program
===================

Goto the `orca <https://orcaforum.kofo.mpg.de/app.php/portal>`_
forum website. Register yourself if you are new or login.
Download the preffered version for Linux x86 and copy it 
to your account. Now create a ``apps/`` directory inside your ``home``
and move the tar file there and untar it.

.. code-block:: bash
	
	mkdir -p ~/apps
	mv orca_4_2_1_linux_x86-64_shared_openmpi411.tar.xz ~/apps
	cd ~/apps
	tar -xvf orca_4_2_1_linux_x86-64_shared_openmpi411.tar.xz


Installation
============

ORCA is distributed as  precompiled binary files. So there is nothing to install other than the 
environment paths.

To run ORCA in parallel it requires OpenMPI package library. So either you have
to load OpenMPI by ``module`` system in paramshakti (easy way!!) or you have to install OpenMPI. 
Please visit the OpenMPI installtion for building it from source. In this tutorial we will use the pre-installed
OpenMPI library in paramshakti for ORCA.  The supported MPI version are usually mentioned in the orca folder name
when you extract it
e.g ``orca_4_2_1_linux_x86-64_shared_openmpi314`` means ORCA version is 4.2.1 and supported OpenMPI version is 3.1.4

Module File setup
-----------------

Packages in paramshakti are usually maintained by using the ``module`` system. You can easily maintain multiple version
of same/different packages with this system.
First create a ``modulefiles`` directory inside your ``\home``

.. code-block:: bash
	
	mkdir -p ~/modulefiles/orca
	cd ~/modulefiles/orca

create a file with your preferred name e.g ``421`` (usually same with the orca version)

Here is a sample modulefile(``421``)

.. code-block:: bash

	#%Module1_0
	## ORCA modulefile
	##
	proc ModulesHelp { } {

	        puts stderr "\tAdds ORCA to your environment"
	}

	module-whatis   "Adds ORCA to your environment"
	module try-add compiler/gcc/8.3.0
	module try-add openmpi3/3.1.4

	setenv ORCAPATH /home/<username>/apps/orca_4_2_1_linux_x86-64_shared_openmpi314

	prepend-path    PATH    /home/<username>/apps/orca_4_2_1_linux_x86-64_shared_openmpi314
	prepend-path    LD_LIBRARY_PATH /home/<username>/apps/orca_4_2_1_linux_x86-64_shared_openmpi314

Important points to remember:

- ``module-tryadd`` will load the gcc (version 8.3.0) and openmpi (version 3.1.4) these two are pre-installed.
- ``setenv ORCAPATH`` path to your orca directory. In this case it is located  under ``apps`` subdirectory inside the ``\home``
- ``prepend-path`` usually the same directory required for ORCA

Modify these variables according to your account 

Now modulefile for ORCA is created and module path needs to be set in the environment ``~/.bashrc``

open ``~/.bashrc`` file with an editor and paste this 

.. code-block:: bash

	export MODULEPATH=$MODULEPATH:/home/<username>/modulefiles

save it and ``source`` it

.. code-block:: bash

	source ~/.bashrc

try this in command line  

.. code-block:: bash

	module load module load orca/421

if no error is coming out try 

.. code:: bash

	$ which orca

it should print out

.. code-block:: bash

	$ /home/<username>/apps/orca_4_2_1_linux_x86-64_shared_openmpi314/orca


Congratulation !! You have successfully installed ORCA in your account.

Submit Script for SLURM in paramshakti
--------------------------------------

It's time to test the ORCA Program.

Go to your ``scratch`` directory and submit a test job. Here is a sample submit script.

.. code-block:: bash

	#!/bin/bash
	#SBATCH -J orca-testjob     # name of the job
	#SBATCH -p standard-low     # name of the partition: available options "standard, standard-low, gpu, hm"
	#SBATCH -n 16   	        # no of processes or tasks
	#SBATCH -t 1:00:00          # walltime in HH:MM:SS, Max value 72:00:00
	
	#list of modules you want to use, for example
	module load orca/421
	#name of the executable
	exe=$ORCAPATH/orca
	#run the application
	$exe opt.inp >& result.out

	