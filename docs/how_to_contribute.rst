.. _how_to_contribute:

How to Contribute
=================

This website is build with the help of `readthedocs.org <https://readthedocs.org/>`_ and `Sphinx <https://www.sphinx-doc.org/en/master/>`_
with ``sphinx_rtd_theme``

You can read their documentation for details.

Installation
------------

Clone the github repo

.. code:: console

	$ git clone https://github.com/Saikat248/anooplab-docs.git

and install this two packages 

.. code:: console

	$ pip install sphinx
	$ pip install sphinx_rtd_theme


Navigate to ``anooplab-docs/docs`` directory 

there is a ``Makefile`` and start

.. code:: console

	$ make html 

It will create a ``_build`` directory and the ``html`` files

.. code:: console 

	$ firefox _build/html/index.html

The whole website will run locally.
Go ahead start editing the documents and before pushing make sure the build is successful.

Enjoy !!
