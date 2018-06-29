RadxPrint
=========

RadxPrint allows you to print data header from any of the files
supported by Radx, such as CfRadial and sweep format.

Prerequisite
------------

-  RadxConvert output files

Running RadxPrint
-----------------

To check all command line options for RadxPrint, type the following
command into a bash：

.. code:: bash

    lrose -- RadxPrint -h

-  To print the data with CfRadial format in a generic form, type:

.. code:: bash

    lrose -- RadxPrint -f CfRadial_file

-  To print the data with sweep format in a generic form, type:

.. code:: bash

    lrose -- RadxPrint -f sweep_file

If the user prefers to store the printed information in a .txt file,
type:

.. code:: bash

    lrose -- RadxPrint -f CfRadial_file > file_name.txt

In addition, RadxPrint also allows you to print out a specific field.
For example, print the information of REF field onto a .txt file:

.. code:: bash

    lrose -- RadxPrint -f CfRadial file -field REF > file_name.txt
