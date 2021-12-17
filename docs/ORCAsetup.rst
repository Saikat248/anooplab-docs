.. _ORCAsetup:

-------------------------------
Setup and Installation of ORCA
-------------------------------

This guide deal with setup ORCA package in 
paramshakti supercomputing facility in user's
own account


.. contents::

Getting the Program
===================

Goto the `orca <https://orcaforum.kofo.mpg.de/app.php/portal>`_
forum website. Register yourself if you are new or login.
Download the preffered version for Linux x86 and copy it 
to your account.

Untar/unzip it and placed it somewhere inside in your ``/home``
directory.

Installation
============

ORCA is distributed as  precompiled binary files. So there is nothing to install other than the 
environment paths.

To run ORCA in parallel it requires OpenMPI package library. So either you have
to load OpenMPI by ``module`` system in paramshakti (easy way!!) or you have to install OpenMPI. 
Please visit the OpenMPI installtion for building it from source. In this tutorial we will use the pre-installed
OpenMPI in paramshakti for ORCA.  

Module File setup
-----------------

Packages in paramshakti are usually maintained by using the ``module`` system. You can easily maintain multiple version
of same/different packages with this system.


