.. _OPENMPIsetup:

-------
Openmpi
-------

This guide leads to the setup openmpi in 
paramshakti supercomputing facility in user's
own account

.. contents::

Requirement
===========
gcc, g++, and gfortran compiler

In paramshakti try this

.. code-block:: bash
	
	module avail | grep gcc

This will output all the available gcc versions.
Load the latest (preferably) version or any other 
depending on your requirement. I loaded gcc 10.2.0

.. code-block:: bash
	
	module load compiler/gcc/10.2.0

Getting the Program
===================

Goto the `openmpi  <https://www.open-mpi.org/>`_
website. Register yourself if you are new or login.
Download the required version for Linux x86 and copy it 
to your account. Now create a ``apps/`` directory inside your ``home``
and move the tar file there and untar it. I am writing this tutorial
for openmpi v `4.1.1`. 

.. code-block:: bash
	
	mkdir -p ~/apps
	mv  ~/apps
	cd ~/apps
	tar -xzvf openmpi-4.1.1.tar.gz 

This will create a directory `openmpi-4.1.1`. It amy be different depending upon
the version. Now create an installation directory. I created with the name
`openmpi411` and copy the path to this directory. For my case the path will be
`/home/<username>/apps/openmpi411`

Now go to the `openmpi-4.1.1` directory and follow the code below

.. code-block:: bash
	
	cd openmpi-4.1.1
	./configure --prefix=/home/<username>/apps/openmpi411 CC=gcc CXX=g++ F77=gfortran FC=gfortran
	make -j10
	make install

This will take some time. If it's finished then the installation is successfully,
otherwise check the error log for details.
After finishing this go to `openmpi411` directory.
You wil find several directories, `bin`, `lib`, `etc`, `include`, `share`.

Next step is to create a modulefile for openmpi 4.1.1.

Module File setup
-----------------

Packages in paramshakti are usually maintained by using the ``module`` system. You can easily maintain multiple version
of same/different packages with this system.
First create a ``modulefiles`` directory inside your ``\home``

.. code-block:: bash
	
	mkdir -p ~/modulefiles/openmpi
	cd ~/modulefiles/openmpi

create a file with your preferred name e.g ``411`` (usually same with the openmpi version)

Here is a sample modulefile(``411``)

.. code-block:: bash

	#%Module1_0
	## ORCA modulefile
	##
	proc ModulesHelp { } {

    	puts stderr "\tAdds OPENMPI to your environment"
	}

	module-whatis   "Adds OPNMPI to your environment"

	module try-add compiler/gcc/10.2.0

	set openmpiversion  4.1.1
	set MPI_HOME    /home/17cy91r04/apps/openmpi411

	prepend-path    LD_LIBRARY_PATH /home/<username>/apps/openmpi411/lib
	prepend-path    PATH /home/<username>/apps/openmpi411/bin

Modify these variables according to your account 

Now modulefile for openmpi is created and module path needs to be set in the environment ``~/.bashrc``

open ``~/.bashrc`` file with an editor and paste this 

.. code-block:: bash

	export MODULEPATH=$MODULEPATH:/home/<username>/modulefiles

save it and ``source`` it

.. code-block:: bash

	source ~/.bashrc

try this in command line  

.. code-block:: bash

	module load openmpi/411

if no error is coming out try 

.. code:: bash

	$ which mpirun

it should print out

.. code-block:: bash

	$ ~/apps/openmpi411/bin/mpirun

Congratulation !! You have successfully installed ORCA in your account.

.. tip:: 

	If anything goes wrong, you have find what is the problem and after fixing the issue
	you have to follow all the steps from `configure` step.
	Before configuring do `make clean` first, otherwise it will take the old configuration
	setup.

Still having problem ? Don't worry, create an issue with proper error output `here <https://github.com/Saikat248/anooplab-docs/issues>`_.

We are happy to help!!

:Date: 14.05.2022
:Authors: - saikat R





