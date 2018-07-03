HawkEye
=======

HawkEye is a next generation lidar and radar display tool.
It can display real-time and archived CfRadial data either in BSCAN, PPI, or RHI geometry.
Editing capability will be added in future releases.

Running HawkEye
---------------

While relatively new to the research community, HawkEye is a mature viewing tool that has been powering real-time displays for NCAR S-Pol, HIAPER Cloud Radar, and the CSWR Doppler on Wheels for several years.
As part of the LROSE project the tool has been updated to work in a research mode with archived CfRadial files.
Like the Radx tools, HawkEye can be run in the Virtual Toolbox or compiled as a native application.
The look and feel of HawkEye will be slightly different depending on the window environment, but the functionality remains the same across platforms.

To run HawkEye as a basic viewer it is not necessary to create a parameter file, but like the LROSE tools there is more functionality provided via the parameter options.
In its simplest invocation:

.. code:: bash

    lrose -- HawkEye -f </path/to/CfRadial_files>

If the data is organized under the YYYYMMHH date directory in the path, the
user can specify specific time span to display:

.. code:: bash

    lrose -- HawkEye -archive_url /scr/rain1/rsfdata/projects/pecan/CfRadial/kddc/moments -start_time "2015 06 26 00 00 00" -time_span 7200

This command would start it up to look at the specified data location,
from the specified start time, for a time span of 2 hours.
In this case, since we are searching by time, you are required to have a
day directory in the path, so that actual data would be in the 20150626 subdirectory underneath the 'moments' directory.

To check all command line options for HawkEye, type the following
command into a bash.

.. code:: bash

    lrose -- HawkEye -h

To obtain the default parameter file for more options, use the following command:

.. code:: bash

    lrose -- HawkEye -print_params > $PWD/HawkEye.params

While HawkEye will do its best to display data properly, the parameter file can force the viewer to use POLAR_DISPLAY for PPI and RHI display and BSCAN_DISPLAY for BSCAN mode.

Colors
~~~~~~

HawkEye supports many different color scales for different fields that can be specified via external files.
Default color palettes are applied to variable names with commonly used meanings (ie. ZDR), but can be overridden by the user.

While most of the GUI viewing options are intuitive, additional documentation on all the details of the HawkEye GUI is under development.
