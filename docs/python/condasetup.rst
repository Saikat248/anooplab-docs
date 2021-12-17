.. _condasetup:

Conda Python
=============

Anaconda is a python distribution. It also has its own package manger ``conda``.
You can install python and other softwares/packages through conda. Main advantage is that 
it comes with most of the necessary packages. 
Here we will tell you how to install anaconda python in paramshakti. 

Installation
------------

Goto the download page for anaconda individual `edition <https://www.anaconda.com/products/individual>`_.
Download the ``Anaconda3-20XX.XX-Linux-x86_64.sh`` file and copy it to your paramshakti ``\home`` directory.

Run it 

.. code-block:: bash

	bash Anaconda3-20XX.XX-Linux-x86_64.sh

Accept the terms and condition by typing ``yes``
You can set up your custom install directory or default location is also fine.
It will take some time to install 

At the end it will ask you 

.. code-block:: bash

	Do you wish the installer to initialize Anaconda3
	by running conda init? [yes|no]

Although the default is ``no`` type ``yes``.

Now logout and login again. You will find there is ``(base)`` in front of login prompt.
you can disable it by 

.. code-block:: bash

	conda config --set auto_activate_base false

Don't worry it will go away next time you login

you can also notice there are some config in your ``~/.bashrc`` file written by conda installer don't remove it.
If you install it in your home directory it will be something like this

.. code-block:: bash

	# >>> conda initialize >>>
	# !! Contents within this block are managed by 'conda init' !!
	__conda_setup="$('/home/username/anaconda3/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
	if [ $? -eq 0 ]; then
	    eval "$__conda_setup"
	else
	    if [ -f "/home/username/anaconda3/etc/profile.d/conda.sh" ]; then
	        . "/home/username/anaconda3/etc/profile.d/conda.sh"
	    else
	        export PATH="/home/username/anaconda3/bin:$PATH"
	    fi
	fi
	unset __conda_setup
	# <<< conda initialize <<<

Now you can activate base environment by 

.. code-block:: bash

	conda activate base 

and deactivate it by 

.. code-block:: bash

	conda deactivate


You can also install different environment environment with required package.
Details documentation is `here <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_.

.. tip:: 

	We strongly recommend to create new environment each time when you work on a different projects. 

You can read more documentation here 

`<https://docs.anaconda.com/anaconda/user-guide/getting-started/>`_



