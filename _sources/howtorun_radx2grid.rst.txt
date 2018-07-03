Radx2Grid
=========

Radx2Grid performs coordinate transformations for ground-based radars from a spherical grid on
which radar data is collected to a regular grid.

The following regular grids are supported:

-  Cartesian grid in (Z,Y,X)
-  PPI grid in (EL, Y, Z) - performs Cartesian transformation on each
   elevation angle separately
-  Polar grid, regular in (EL, AZ, RANGE)

Running Radx2Grid
-----------------

All of the LROSE tools presented so far (RadxPrint, RadxConvert, and HawkEye) work directly on lidar or radar data in its native coordinate system.
For many workflows it is desirable to put the data onto a regular grid for scientific analysis.
The workflow steps to this point have not modified data, but gridding can be considered the first *analysis* step in that scientific decisions have to be made about how to project the data from spherical coordinates to a regular grid.
Note that quality control tools (which also involve scientific decision making) will be added in the next update to Blaze, which can be applied either before or after gridding.

Radx2Grid uses a SPRINT-style interpolation that is suitable for ground-based radars and vertically pointing airborne lidar and radar data.
It is a well-established interpolation method that was designed to have minimal impact for subsequent analysis.
More details on the interpolation method can be found in the original user's guide for SPRINT_, and will be added to this documentation in the near future.

.. _SPRINT: https://wiki.ucar.edu/download/attachments/41487211/sprint.99feb_doc.pdf

**Important Note:**: Due to the more complex geometry of airborne scanning radars such as ELDORA and the NOAA P-3 tail radar the current interpolation method is not appropriate and Radx2Grid will not work properly.
Stay tuned for FRACTL (Fast Reorder and CEDRIC Technique in LROSE) which will do both gridding and multi-Doppler synthesis for airborne radars which will be released later in 2018.

Recent software development in Radx2Grid has streamlined options in parameter file for typical use cases, but with extensive flexibility for power users.
To check all command line options for Radx2Grid, including debugging options and file paths, the typical '-h' flag can be invoked:

.. code:: bash

    lrose -- Radx2Grid -h

Likewise, to obtain the default parameter file, use the following command:

.. code:: bash

    lrose -- Radx2Grid -print_params > Radx2Grid.params

While there are many options for Radx2Grid, a basic gridding technique can be accomplished simply:

.. code:: bash

    lrose -- Radx2Grid -f <path/to/data/file_name> -outdir $PWD/grid

Recall that during the RadxConvert step the CfRadial files can be created as an aggregation of sweep files that make up a single volume scan.
Assuming that option was invoked (which is the default for NEXRAD Level II files) you should now have a Cartesian gridded volume in NetCDF format in the 'grid' subdirectory to use for further analysis.
Note that if you first convert data to DORADE sweep files for editing in soloii, and then convert to CfRadial you must explicitly aggregate the sweeps during that conversion.
A common source of confusion is that only a single sweep is gridded into the volume if the CfRadial file only contains a single sweep.

The Radx2Grid Parameter file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Radx2Grid is a large application with many parameters available for controlling its operation.
This makes the use of the parameter file confusing to a new user. Therefore, the parameters are separated into sections.
The more common sections are at the top of the file, and the less common parameters lower down in the file.

Each section is preceded by a header starting and ending with a line of ======================== characters.

The documentation on the next page has been auto-generated from the default parameter file and reformatted for display.

A few key parameters to look for are listed below.

-  start_time, end_time: set the start time and end time for ARCHIVE mode analysis. The format should be ‘yyyy mm dd hh mm ss’.

-  input_dir: input directory for searching for files. Files will be searched for in this directory.

-  interp_mode: set the interpolation mode. There are five different modes that you can choose.

-  grid_z_geom: specify vertical grid levels. nz, minz, dz represent the number of levels, the lowest level, and constant spacing of the vertical level respectively.

-  grid_xy_geom: similar as grid_z_geom. It specifies the grid parameters in x and y.

-  netcdf_style: specify different format of netCDF. If output_format is CFRADIAL, specify the netCDF format.

-  ncf_title: title string for netCDF file.

-  ncf_institution: institution string for netCDF file.

-  ncf_source: source string for netCDF file.

From here, you can read in the CfRadial or gridded netCDF file using Julia, Python, or other programming language for further analysis.
Additional LROSE tools for analysis including applications for QC, Echo, and Wind workflows will be released in the coming months.
Stay tuned!
