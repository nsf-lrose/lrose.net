RadxPrint Parameter Descriptions
================================

 Prints out radial RADAR/LIDAR data.

DEBUGGING
---------


debug
~~~~~


 Debug option.

 If set, debug messages will be printed appropriately.


 Type: enum

Options:

+      DEBUG_OFF

+      DEBUG_NORM

+      DEBUG_VERBOSE

+      DEBUG_EXTRA


**debug = DEBUG_OFF;**

DATA RETRIEVAL CONTROL
----------------------


path
~~~~


 Path string - full path specified.

 File will be read from this path.


 Type: string


**path = ".";**

specify_file_by_time
~~~~~~~~~~~~~~~~~~~~


 Option to specify file by time.

 If true, paths for reads and writes are based on time and the data 
   directory. If false, reads and writes use the specified path.


 Type: boolean


**specify_file_by_time = FALSE;**

dir
~~~


 Data directory.

 Used to locate file if specify_file_by_time is true.


 Type: string


**dir = ".";**

read_search_mode
~~~~~~~~~~~~~~~~


 Mode for searching for data in time domain.

 For all except LATEST, you must specify the search time and the 
   search margin.


 Type: enum

Options:

+      READ_LATEST

+      READ_CLOSEST

+      READ_FIRST_BEFORE

+      READ_FIRST_AFTER

+      READ_RAYS_IN_INTERVAL


**read_search_mode = READ_LATEST;**

read_search_time
~~~~~~~~~~~~~~~~


 Data time string.

 Time for data requested. Format is YYYY MM DD HH MM SS.


 Type: string


**read_search_time = "1970 01 01 00 00 00";**

read_search_margin
~~~~~~~~~~~~~~~~~~


 Margin around search time (secs).

 Applies to all search modes except LATEST.


 Type: int


**read_search_margin = 3600;**

read_start_time
~~~~~~~~~~~~~~~


 Start time for rays search.

 Applies to READ_RAYS_IN_INTERVAL mode.


 Type: string


**read_start_time = "1970 01 01 00 00 00";**

read_end_time
~~~~~~~~~~~~~


 End time for rays search.

 Applies to READ_RAYS_IN_INTERVAL mode.


 Type: string


**read_end_time = "1970 01 01 00 00 00";**

read_dwell_secs
~~~~~~~~~~~~~~~


 Dwell width (secs).

 Applies to READ_RAYS_IN_INTERVAL mode.


 Type: double


**read_dwell_secs = 1;**

read_dwell_stats
~~~~~~~~~~~~~~~~


 Method for computing stats on the dwell.

 Applies to READ_RAYS_IN_INTERVAL mode. MIDDLE refers to the middle 
   ray in the dwell sequence.


 Type: enum

Options:

+      DWELL_STATS_MEAN

+      DWELL_STATS_MEDIAN

+      DWELL_STATS_MAXIMUM

+      DWELL_STATS_MINIMUM

+      DWELL_STATS_MIDDLE


**read_dwell_stats = DWELL_STATS_MIDDLE;**

READ CONTROL OPTIONS
--------------------


read_meta_data_only
~~~~~~~~~~~~~~~~~~~


 Option to only read the meta data.

 In this case sweep and field metadata will be read, but the ray and 
   field data will not be read.


 Type: boolean


**read_meta_data_only = FALSE;**

read_set_field_names
~~~~~~~~~~~~~~~~~~~~


 Option to set field names.


 Type: boolean


**read_set_field_names = FALSE;**

read_field_names
~~~~~~~~~~~~~~~~


 Field name list.


 Type: string
 1D array - variable length.


**read_field_names = {**


**};**

read_set_fixed_angle_limits
~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to set fixed angle limits.

 If 'read_apply_strict_angle_limits' is set, only read sweeps within 
   the specified fixed angle limits. If strict checking is false and no 
   data lies within the limits, return the closest applicable sweep. 
   NOTE - fixed angles are elevation in PPI mode and azimuth in RHI 
   mode.


 Type: boolean


**read_set_fixed_angle_limits = FALSE;**

read_lower_fixed_angle
~~~~~~~~~~~~~~~~~~~~~~


 Lower fixed angle limit - degrees.


 Type: double


**read_lower_fixed_angle = 0;**

read_upper_fixed_angle
~~~~~~~~~~~~~~~~~~~~~~


 Upper fixed angle limit - degrees.


 Type: double


**read_upper_fixed_angle = 90;**

read_set_sweep_num_limits
~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to set sweep number limits.

 If 'read_apply_strict_angle_limits' is set, only read sweeps within 
   the specified limits. If strict checking is false and no data lies 
   within the limits, return the closest applicable sweep.


 Type: boolean


**read_set_sweep_num_limits = FALSE;**

read_lower_sweep_num
~~~~~~~~~~~~~~~~~~~~


 Lower sweep number limit.


 Type: int


**read_lower_sweep_num = 0;**

read_upper_sweep_num
~~~~~~~~~~~~~~~~~~~~


 Upper sweep number limit.


 Type: int


**read_upper_sweep_num = 0;**

read_apply_strict_angle_limits
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to apply strict checking for angle or sweep number limits on 
   read.

 If true, an error will occur if the fixed angle limits or sweep num 
   limits are outside the bounds of the data. If false, a read is 
   guaranteed to return at least 1 sweep - if no sweep lies within the 
   angle limits set, the nearest sweep will be returned.


 Type: boolean


**read_apply_strict_angle_limits = TRUE;**

read_set_radar_num
~~~~~~~~~~~~~~~~~~


 Option to set the radar number.

 See read_radar_num.


 Type: boolean


**read_set_radar_num = FALSE;**

read_radar_num
~~~~~~~~~~~~~~


 Set the radar number for the data to be extracted.

 Most files have data from a single radar, so this does not apply. The 
   NOAA HRD files, however, have data from both the lower fuselage (LF, 
   radar_num = 1) and tail (TA, radar_num = 2) radars. For HRD files, by 
   default the TA radar will be used, unless the radar num is set to 1 
   for the LF radar.


 Type: int


**read_radar_num = 0;**

aggregate_sweep_files_on_read
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to aggregate sweep files into a volume on read.

 If false, and the input data is in sweeps rather than volumes (e.g. 
   DORADE), the sweep files from a volume will be aggregated into a 
   volume.


 Type: boolean


**aggregate_sweep_files_on_read = FALSE;**

aggregate_all_files_on_read
~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to aggregate all files in the file list on read.

 If true, all of the files specified with the '-f' arg will be 
   aggregated into a single volume as they are read in. This only 
   applies to FILELIST mode. Overrides 'aggregate_sweep_files_on_read'.


 Type: boolean


**aggregate_all_files_on_read = FALSE;**

ignore_antenna_transitions
~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to ignore rays with antenna transition flag set.

 The transition flag is set when the antenna is moving between sweeps. 
   If this parameter is true, rays containing the transition flag will 
   not be read in.


 Type: boolean


**ignore_antenna_transitions = FALSE;**

load_volume_fields_from_rays
~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to load up fields on the volume by combining the fields from 
   the rays into a single array.

 If false, the fields will be left managed by the rays.


 Type: boolean


**load_volume_fields_from_rays = FALSE;**

trim_surveillance_sweeps_to_360deg
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to trip surveillance sweeps so that they only cover 360 
   degrees.

 Some sweeps will have rays which cover more than a 360-degree 
   rotation. Often these include antenna transitions. If this is set to 
   true, rays are trimmed off either end of the sweep to limit the 
   coverage to 360 degrees. The median elevation angle is computed and 
   the end ray which deviates from the median in elevation is trimmed 
   first.


 Type: boolean


**trim_surveillance_sweeps_to_360deg = FALSE;**

remove_rays_with_all_data_missing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to remove rays for which all data is missing.

 If true, ray data will be checked. If all fields have missing data at 
   all gates, the ray will be removed after reading.


 Type: boolean


**remove_rays_with_all_data_missing = FALSE;**

remove_rays_with_antenna_transitions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to remove rays taken while the antenna was in transition.

 If true, rays with the transition flag set will not be used. The 
   transiton flag is set when the antenna is in transtion between one 
   sweep and the next.


 Type: boolean


**remove_rays_with_antenna_transitions = FALSE;**

set_max_range
~~~~~~~~~~~~~


 Option to set the max range for any ray.


 Type: boolean


**set_max_range = FALSE;**

max_range_km
~~~~~~~~~~~~


 Specified maximim range - km.

 Gates beyond this range are removed.


 Type: double


**max_range_km = 9999;**

preserve_sweeps
~~~~~~~~~~~~~~~


 Preserve sweeps just as they are in the file.

 Applies generally to NEXRAD data. If true, the sweep details are 
   preserved. If false, we consolidate sweeps from split cuts into a 
   single sweep.


 Type: boolean


**preserve_sweeps = FALSE;**

remove_long_range_rays
~~~~~~~~~~~~~~~~~~~~~~


 Option to remove long range rays.

 Applies to NEXRAD data. If true, data from the non-Doppler long-range 
   sweeps will be removed.


 Type: boolean


**remove_long_range_rays = FALSE;**

remove_short_range_rays
~~~~~~~~~~~~~~~~~~~~~~~


 Option to remove short range rays.

 Applies to NEXRAD data. If true, data from the Doppler short-range 
   sweeps will be removed.


 Type: boolean


**remove_short_range_rays = FALSE;**

set_ngates_constant
~~~~~~~~~~~~~~~~~~~


 Option to force the number of gates to be constant.

 If TRUE, the number of gates on all rays will be set to the maximum, 
   and gates added to shorter rays will be filled with missing values.


 Type: boolean


**set_ngates_constant = FALSE;**

change_radar_latitude_sign
~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to negate the latitude.

 Mainly useful for RAPIC files. In RAPIC, latitude is always positive, 
   so mostly you need to set the latitiude to the negative value of 
   itself.


 Type: boolean


**change_radar_latitude_sign = FALSE;**

apply_georeference_corrections
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


 Option to apply the georeference info for moving platforms.

 For moving platforms, measured georeference information is sometimes 
   available. If this is set to true, the georeference data is applied 
   and appropriate corrections made. If possible, Earth-centric azimuth 
   and elevation angles will be computed.


 Type: boolean


**apply_georeference_corrections = FALSE;**

PRINT CONTROL
-------------


print_mode
~~~~~~~~~~


 Print mode option.

 Controls details of the printing. Generally set in response to the 
   command line args.


 Type: enum

Options:

+      PRINT_MODE_NORM

+      PRINT_MODE_NATIVE

+      PRINT_MODE_DORADE_FORMAT


**print_mode = PRINT_MODE_NORM;**

print_rays
~~~~~~~~~~


 Option to print out ray meta data.

 If false, only sweep and calib information will be printed.


 Type: boolean


**print_rays = FALSE;**

print_ray_summary
~~~~~~~~~~~~~~~~~


 Option to print summary for each ray.

 The main metadata will be printed, followed by the ray summary.


 Type: boolean


**print_ray_summary = FALSE;**

print_ray_table
~~~~~~~~~~~~~~~


 Option to print a space-delimited angle table.

 If true, prints space-delimited table of ray properties.


 Type: boolean


**print_ray_table = FALSE;**

print_data
~~~~~~~~~~


 Option to print out data.

 If true, data values will be printed.


 Type: boolean


**print_data = FALSE;**

