RadxConvert
===========

RadxConvert allows you to convert data stored in one format to a
different format.

Supported Lidar and Radar Data Formats
--------------------------------------

+------------------------------------+-------------+--------------+
| Format                             | Read Access | Write Access |
+====================================+=============+==============+
| CfRadial-1                         | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| CfRadial-2 (WMO) (in development)  | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| BUFR (in development)              | Yes(partial)| No           |
+------------------------------------+-------------+--------------+
| CFARR                              | Yes         | No           |
+------------------------------------+-------------+--------------+
| DORADE - NCAR/EOL                  | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| D23R                               | Yes         | No           |
+------------------------------------+-------------+--------------+
| DOE ARM netCDF (precedes CfRadial) | Yes         | No           |
+------------------------------------+-------------+--------------+
| EEC-Edge                           | Yes(partial)| No           |
+------------------------------------+-------------+--------------+
| Foray-1 netCDF - NCAR/EOL          | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| GAMIC                              | Yes         | No           |
+------------------------------------+-------------+--------------+
| Gematronik Rainbow                 | Yes         | No           |
+------------------------------------+-------------+--------------+
| HSRL (Lidar)                       | Yes         | No           |
+------------------------------------+-------------+--------------+
| HRD (Hurricane Research Division)  | Yes         | No           |
+------------------------------------+-------------+--------------+
| Leosphere (LIDAR ASCII format)     | Yes         | No           |
+------------------------------------+-------------+--------------+
| MDV radial - NCAR/RAL              | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| NEXRAD Level 2                     | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| NEXRAD Level 1, 3                  | Yes         | No           |
+------------------------------------+-------------+--------------+
| NOXP                               | Yes         | No           |
+------------------------------------+-------------+--------------+
| NSSL-MRD                           | Yes         | No           |
+------------------------------------+-------------+--------------+
| ODIM-H5 (in development)           | Yes         | Yes          |
+------------------------------------+-------------+--------------+
| RAPIC - BOM Australia              | Yes         | No           |
+------------------------------------+-------------+--------------+
| SIGMET - raw format (Vaisala)      | Yes         | No           |
+------------------------------------+-------------+--------------+
| TDWR                               | Yes         | No           |
+------------------------------------+-------------+--------------+
| TWOLF                              | Yes         | No           |
+------------------------------------+-------------+--------------+
| UF - Universal Format              | Yes         | Yes          |
+------------------------------------+-------------+--------------+

Running RadxConvert
-------------------

RadxConvert uses the Radx engine as a backend to convert between many different data formats.
Since RadxPrint, RadxConvert, and Radx2Grid all have the same backend engine, they work seamlessly together.
Many researchers spend a lot of time writing code just to get their data into a format they can use with their analysis software, and RadxConvert solves that problem for many common lidar and radar data formats.
At a basic level, RadxConvert can do a simple conversion from one format to another, but it has a lot of flexibility and power options for advanced use cases.
To see all command line options for RadxConvert, type the following command into a terminal:

.. code:: bash

    lrose -- RadxConvert -h

**Important Note:** If you just type 'RadxConvert' on the command line without any options it goes into 'REALTIME' mode and waits for streaming data to come in.
For most use cases with data files stored locally the preferred mode of operation is to use command line arguments or a parameter file.
This can be a little confusing for first time users.
If you forget the '-f' or '-params' flag then this can also trigger REALTIME mode, and can appear like the conversion is taking a long time when in fact it is just waiting for data.
While accidentally using REALTIME mode can occasionally cause some confusion, it allows for a powerful streaming capability to convert data directly from an instrument into a different format in real time.

For most applications, user's will have the data stored locally and want to convert to CfRadial or another data format.
There are two different ways to specify the output file format, either on the command line or in a parameter file.
If you don’t have specific requirements for the conversion settings, the easiest way to convert data to CfRadial format is to just use the command line '-f' option, which specifies a list of files:

.. code:: bash

    lrose -- RadxConvert -f <path/to/data/file_name>

For example, to convert a NEXRAD Level 2 file from the Miami radar into CfRadial and place the file in an 'output' subdirectory:

.. code:: bash

    lrose -- RadxConvert -f $PWD/Level2_KAMX_20161006_1906.ar2v -outdir $PWD/output

Note that RadxConvert will create the output subdirectory if it doesn't exist.

**Important Note:** We encourage users to not move the converted data from the date subdirectory directory or rename the files.
Many data file formats (such as both CfRadial and DORADE) keep metadata in the filename, and other LROSE tools such as HawkEye will work better when the data is organized by date at the subdirectory level.
RadxConvert will automatically name and sort the files chronologically, and will organize the converted data by date into subdirectories with a YYYYMMDD naming convention.

We recommend migrating your workflow to use the CfRadial netCDF format for your data analysis.
CfRadial has well defined metadata standards and version 2.0 has been selected by the World Meteorological Organization (WMO) as the new international standard for lidar and radar data.
The format has many advantages over older formats such as UF or DORADE, and works well with other open source radar packages such as PyART.
Users are also encouraged to compile their CfRadial files as an aggregation of sweep files that make up a single volume scan.
This is the default for file types that the Radx engine can recognize as volume scans (such as NEXRAD Level 2 archives), and can prescribed via the parameter file in other cases.

RadxConvert does support the conversion to DORADE sweep format which can still be utilized by Solo users.
CfRadial files can be displayed by HawkEye, but cannot yet be directly edited in that program.
Editing capability for HawkEye is currently in development and will continue to add more functionality to eventually replace soloii and solo3.
In the meantime, data can be converted to sweepfiles for interactive editing using:

.. code:: bash

    lrose -- RadxConvert -dorade -f <path/to/data/file_name>


A parameter file can also be generated and modified similarly to the other LROSE tools.

.. code:: bash

    lrose -- RadxConvert -print_params > $PWD/RadxConvert.params

The user can specify the specific output format in RadxConvert.params file. For example:

Open RadxConvert.params in the terminal and find the line with 'output_format'. Set the desired output format as one of the options. For example, to choose CfRadial:

.. code:: bash

    output_format = OUTPUT_FORMAT_CFRADIAL

or for DORADE:

.. code:: bash

    output_format= OUTPUT_FORMAT_DORADE

Use the following command to convert using the settings provided by the parameter file:

.. code:: bash

    lrose -- RadxConvert -f <path/to/data/file_name> -params $PWD/RadxConvert.params

The next page of the documentation has all the options for RadxConvert automatically generated from the default parameter file.
If you've had enough of format conversion, you can move on to the next step of the workflow and display_ your data in CfRadial exchange format.

.. _display: howtorun_hawkeye.html
