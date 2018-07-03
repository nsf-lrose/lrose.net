RadxPrint
=========

RadxPrint allows you to print data header from any of the files
supported by Radx, such as CfRadial and sweep format.
It is one of the simplest, but most useful tools in the LROSE Virtual Toolbox.

Prerequisites
-------------

- A working LROSE Blaze installation is required. Complete the free registration_ and follow the install instructions.

- Throughout the documentation, terms in brackets should be replaced with actual path and/or file names.

- The following instructions assume you are using the Virtual Toolbox. Any supported LROSE Blaze command can be invoked in the toolbox using 'lrose -- <command>'. The lrose script automatically maps your home directory to the toolbox, but requires absolute paths in order to find files. Use the $PWD environmental variable to designate the current path in a terminal.

- For native LROSE Blaze apps installed in your executable path, just drop 'lrose -- ' or replace with the absolute path to the location where the binaries are installed.

- The Radx Engine that powers LROSE can handle 24 radar and lidar formats_ (and counting). To see if your data works with LROSE, first use RadxPrint to query the metadata.

.. _registration: ../../../software.html

.. _formats: howtorun_radxconvert.html#supported-lidar-and-radar-data-formats

Running RadxPrint
-----------------

At a basic level, the primary function of RadxPrint is to query a file to find out if it is supported by LROSE, and to look at the metadata.
To print the data for a file in a generic form, type the following command into a terminal:

.. code:: bash

    lrose -- RadxPrint -f </path/to/data/file_name>

Printing data with any Radx supported format works the same way. For example, a CfRadial file in the current directory from the Miami NEXRAD can be examined:

.. code:: bash

    lrose -- RadxPrint -f $PWD/cfrad.20161006_190750.006_to_20161006_191339.679_KAMX_Surveillance_SUR.nc

Sometimes the output can be too long to read, so you can pipe to 'more':

.. code:: bash

    lrose -- RadxPrint -f </path/to/CfRadial_filename> | more

or store the printed information in a .txt file. For example:

.. code:: bash

    lrose -- RadxPrint -f $PWD/Level2_KAMX_20161006_1906.ar2v > KAMX_20161006_1906_metadata.txt

In addition, RadxPrint also allows you to print out a specific field.
For example, print the information of REF field onto a .txt file:

.. code:: bash

    lrose -- RadxPrint -field REF -f $PWD/Level2_KAMX_20161006_1906.ar2v > KAMX_20161006_1906_metadata.txt > KAMX_20161006_1906_REF.txt

RadxPrint supports many different command line options. To see all the command line options for RadxPrint, type：

.. code:: bash

    lrose -- RadxPrint -h

In addition to command line options, even greater control can be achieved using a "parameter" file.
The parameter file is self-describing, but a formatted version is also included in this documentation.
To produce a parameter file, just print the parameters and pipe them to a text file:

.. code:: bash

    lrose -- RadxPrint -print_params > RadxPrint.params


You can modify the parameter file using any text editor.
A RadxPrint parameter file is particularly helpful if you want to do the same command over and over again, for example to extract specific metadata, set time limits, or print extra information.
Once you have the parameters set the way you like, then just add the '-params' flag to the command.
A app-specific parameter file and -params flag is a common feature of all the Radx engine tools.

.. code:: bash

    lrose -- RadxPrint -params RadxPrint.params -f </path/to/CfRadial_filename>

The next page of the documentation has all the options for RadxPrint automatically generated from the default parameter file.
If you've seen enough metadata, you can move on to the next step of the workflow and convert_ your data to CfRadial exchange format.

.. _convert: howtorun_radxconvert.html
