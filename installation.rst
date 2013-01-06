.. _installation-oclint:

Installation
============

Installation of OCLint is pretty easy, please sure you already download the pkg installer.

Terminal Installation
---------------------

.. code-block:: bash

    sudo installer -pkg oclint-0.4.3.pkg -target /

GUI Installation
----------------

Double click the pkg installer to start the installation. Please agree the BSD license and grant permission to installer for writing OCLint to your system.

.. image:: _static/installation-steps/1.png
.. image:: _static/installation-steps/2.png
.. image:: _static/installation-steps/3.png
.. image:: _static/installation-steps/4.png
.. image:: _static/installation-steps/5.png

For your interest, no matter you install OCLint via terminal or GUI, installer will write OCLint binary file to ``/usr/bin/oclint``, and related libraries to ``/usr/lib/oclint``.

After installation, you can `invoke OCLint in terminal <command.html>`_.

At this stage of development, OCLint is only pre-compiled for Mac OS X Lion/Snow Leopard users. For Linux users, please read `how to compile <compile.html>`_ to build OCLint.
