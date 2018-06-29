HawkEye
=======

The HawkEye application is available for the user to display real-time
data and previously stored data either in BSCAN-type display or
polar-typle display.

Prerequisites
-------------

The following item are required: - HawkEye - RadxConvert output files
(CfRadial)

Parameter file
--------------

The parameter file will need to be updated to change the display mode
set by the user.

Ensure parameter file is up to date
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To obtain the default parameter file, use the following command:

.. code:: bash

    lrose -- HawkEye -print_params > /path/to/param_file_name

If you already have a parameter file and simply want to check for (and
add) updated parameters while retaining current parameters, use the
following command:

.. code:: bash

    lrose -- HawkEye -params orig_param_file_name -print_params > new_param_file_name

Specific parameters to edit
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Caution: this is not an exhaustive list. We urge each user to read
through the entire parameter file carefully.

-  display mode: specify the display mode. It supports POLAR_DISPLAY for
   normal PPI and RHI display and BSCAN_DISPLAY for BSCAN mode.

Running HawkEye
---------------

To check all command line options for HawkEye, type the following
command into a bash.

.. code:: bash

    lrose -- HawkEye -h

Once your parameter file is complete, specify the location of CfRadial
files to run the application:

.. code:: bash

    lrose -- HawkEye -params param_file_name -f /path/to/CfRadial_files

One thing worth noticing is that it’s not necessarily to create a
parameter file. If the user have no specific requirement and no day
directory in the path, you can start HawkEye without a param file and
specified timeframe:

.. code:: bash

    lrose -- HawkEye -f /path/to/CfRadial_files

If the user store the data under the day directory in the path (You can
obtain the default directory setting by performing RadxConvert), the
user can specify specific time span to display:

.. code:: bash

    lrose -- HawkEye -archive_url /scr/rain1/rsfdata/projects/pecan/CfRadial/kddc/moments -start_time "2015 06 26 00 00 00" -time_span 7200

This command would start it up to look at the specified data location,
from the specified start time, for a time span of 2 hours.

In this case, since we are searching by time, you are required to have a
day directory in the path, so that actual data would be in:

.. code:: bash

    /scr/rain1/rsfdata/projects/pecan/CfRadial/kddc/moments/20150626/
