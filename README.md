# Mu - Telemetry Exporter for iRacing
Developed by Patrick Moore (patrickwmoore@gmail.com)
Last update: 11/12/2014


Requirements
------------------------------------------------------------------------------
.NET Framework 4.0 must be installed prior to installing Mu.


Installation
------------------------------------------------------------------------------
Run MuInstaller.msi and follow any prompts. The installer will automatically
update any prior version of Mu.

The following files are installed in your <Program Files>\Mu directory:
 - Mu.exe
 - Mshldaq.dll
 - daq.dll
 - Readme.txt 
 
The following files are created automatically:
 - <Local Settings>\Application Data\Mu\Mu\Mu-????\user.config (Mu's settings)


Notes
------------------------------------------------------------------------------
- Mu will automatically export iRacing's .ibt telemetry files into MoTeC's
  format.  .ibt files are created by activating telemetry within iRacing by
  pressing Alt-L before entering your car on the track.

- GPS Telemetry data is exported in 3 channels (Degrees, Minutes, Seconds), 
  and must be combined by MoTeC Maths into the channels GPS Latitude and 
  GPS Longitude.  The Math formula you should use is as follows:

  GPS Latitude - Quantity: Angle  Display Unit: degree  Decimal: 8 
                 Result Unit: Degree
				 Expression: 'Latitude Degrees' + 'Latitude Minutes' / 60.0 
				             + 'Latitude Minute - fraction' / 3600
  
  GPS Longitude - Quantity: Angle  Display Unit: degree  Decimal: 8 
                  Result Unit: Degree
			      Expression: 'Longitude Degrees' + 'Longitude Minutes' / 60.0 
				  + 'Longitude Minute - fraction' / 3600.0

- Currently Tire information is only exported for cars that use iRacing's new
  tire model. 
  
- Mu will update automatically if a newer version is available. You can also
  check if there is an update by right-clicking and selecting 'Check For 
  Update'.
  
- Double clicking on the System Tray icon for Mu will open the settings and
  log.
  
- By default, the export directory will be set to 
  <My Documents>\iRacing\telemetry.  This can be modified in the settings.  A
  directory must exist for it to be used.
  
- Exported telemetry can be read by MoTeC's i2 Pro.  This software can be
  downloaded for free from MoTeC's website.  Mu is not a MoTeC product or
  supported by MoTeC.  I accept no responsibility for how Mu's exported
  telemetry is used.
  
- In MoTeC, it will appear as though brake data is not working.  You will need 
  to change the channel from the default of Brake Pressure to Brake Position.
  
- Mu supports loading of car information from an configuration file.  To
  define the configuration file, create a text file with the name 
  'vehicleinfo.cfg' in the same directory as the Mu executable, the import 
  directory, or the export directory.  The file is a yaml file with the 
  following format:
  
---
Vehicles:
- name: formulamazda
  Attributes:
    Vehicle Weight: 650 kg
    Fuel Tank Capacity: 72 l
    Vehicle Track: 1485 mm
    Vehicle Wheelbase:: 2522 mm

- name: rt2000
  Attributes:
    Vehicle Weight: 664 kg
    Fuel Tank Capacity: 19684 ml
    Vehicle Track: 1562 mm
    Vehicle Wheelbase: 2459 mm

- name: rileydp
  Attributes:
    Vehicle Weight: 2275 lb
    Fuel Tank Capacity: 20 USgal
    Vehicle Track: 78 in
    Vehicle Wheelbase: 110 in
    Maximum Speed: 200 mph

Constants:
  Minimum Laps: 2
  Acceleration of Gravity: 9.8 m/s^2
  


  Additional cars can be added on as long as the format is followed.  The car's
  name must be identical to the iRacing directory name of the car.  Vehicle
  Weight, Fuel Tank Capacity, Vehicle Track, and Vehicle Wheelbase are
  specially named in MoTeC and appear in the Detail section along with being
  used in Maths.
  
  Additional attributes and constants can be added as long as the format is
  followed.
  
  Units can be given in the following quantities. Usage of quantities not 
  explicitly labeled below will result in incorrect data in MoTeC:
  
  - Volume
	  cc
	  l
	  ml
	  USfloz
	  USgal
	  
  - Length & Distance
      cm
      ft
      in
      km
      m
      mil
      mile
      mm
      
  - Mass
      cin
      g
      kg
      lb
      mg
      oz
	
  
Change Log
------------------------------------------------------------------------------

<<<<< Changes for 1.6.7.0 - 11/12/2014 >>>>>

 - Fixed issue with saved setup option always being disabled on startup.


<<<<< Changes for 1.6.6.0 - 11/2/2014 >>>>>

 - Fixed issue with exported telemetry not loading in i2 Pro v1.1.0.0768.


<<<<< Changes for 1.6.5.0 - 10/6/2014 >>>>>

 - Fixed parsing issue with Unit Conversion system in parsing kPa and psi.


<<<<< Changes for 1.6.4.1 - 9/22/2014 >>>>>

 - Fixed parsing issue with Unit Conversion system in parsing mm.


<<<<< Changes for 1.6.4.0 - 8/23/2014 >>>>>

 - Cleaned old code and improved performance for machines with less than
   4 cores.

 - Created new Unit Conversion system which is faster and more robust than the
   old system.

 - Fixed small memory leak.

 - Fixed issue where the exporting of CSV files were not reporting errors.


<<<<< Changes for 1.6.3.0 - 5/7/2014 >>>>>

 - Fixed issue with FastLaps not extracting.

 - Added feature that will copy the current setup into the same directory as
   a newly created telemetry file.

 - Updated to use irsdk v1.06.


<<<<< Changes for 1.6.2.0 - 2/21/2014 >>>>>

 - Removed change that reduced beacon channel size to fix issue it was causing
   with the calculation of lap times.


<<<<< Changes for 1.6.1.0 - 2/19/2014 >>>>>

 - Fixed issue with the update thread not terminating correctly if Mu shuts
   down during an update.

 - Updated YAML library.  Performance in parsing has been increased.  Some
   have reported an error when loading vehicle info.  Check to make sure your
   format is correct (example above).


<<<<< Changes for 1.6.0.0 - 1/29/2014 >>>>>

 - Added setting to choose not to show the Settings screen on startup.

 - Processing and export speed are faster by ~10%.

 - Fixed issue where Mu would process an invalid FastLap.

 - Fixed issue where sometimes the Log window would not update.

 - Fixed issue where a file would not be automatically exported during a session.


<<<<< Changes for 1.5.2.0 - 4/26/2013 >>>>>

 - Fixed issue in fastest lap export which caused the fastest lap to revert to
   the first lap of the first stint.


<<<<< Changes for 1.5.1.0 - 2/16/2013 >>>>>

 - Fixed issue with processing files that were still being created.

 - Fixed issue with not processing other files after an error occurs.


<<<<< Changes for 1.5.0.0 - 2/11/2013 >>>>>
 
 - Mu is once again compatible with Windows XP.

 - Added option to be able to extract the fastest lap from an ibt file.  The 
   fast lap telemetry will show up as another ibt file in the import 
   directory.

 - Updated the Log window to be more efficient plus allowing to copy the
   contents to the Windows Clipboard.

 - Added Rescan option to the SysTray app icon to force a rescan of the Import
   Directory.

 - Fixed issue with the user.config getting corrupted on upgrades.

 - Optimized the writing out of CSV files.

 - Furthur optimized the importing and exporting of telemetry.


<<<<< Changes for 1.4.4.0 - 12/5/2012 >>>>>

 - Fixed beacon timings to resolve incorrect lap times.


<<<<< Changes for 1.4.3.0 - 11/17/2012 >>>>>

 - Fixed auto-enabling of telemetry for the 64bit version of iRacing.


<<<<< Changes for 1.4.2.0 - 11/6/2012 >>>>>
 
 - Added VS110 C++ redistributable to the installer.  This fixes
   the System.IO.FileNotFound exception.

 - Fixed GPS and precision issues.


<<<<< Changes for 1.4.1.0 - 11/5/2012 >>>>>

 - Fixed race condition with auto-updater that would throw an exception on
   program start.


<<<<< Changes for 1.4.0.0 - 11/4/2012 >>>>>

 - Added export of GPS channels.  *Please see notes on incorperating GPS data 
   in MoTeC

 - Added new channels exposed by iRacing.

 - Incorperated beacons into the channels that allows MoTeC to generate lap
   files without the .ldx file being present.

 - Updated to .NET 4.0.


<<<<< Changes for 1.3.2.0 - 8/5/2012 >>>>>

 - Fixed telemetry auto-enable to work on keyboards with alternate layouts.
 
 
<<<<< Changes for 1.3.1.0 - 8/3/2012 >>>>>

 - Auto-Enable Telemetry will now turn telemetry on when entering your car on
   the track.  This should bypass issues where telemetry was not being turned
   on.
   
 - Mu will now only check for new telemetry files while you are not on the
   track.
 
 
<<<<< Changes for 1.3.0.0 - 6/23/2012 >>>>>

 - Added Csv export.
 
 - Removed 'Export All Channels' option.  All channels are now exported by
   default.
   
 - Reduced memory usage during export.
 
 - Fixed possible config file corruption after upgrading.
 

<<<<< Changes for 1.2.9.0 - 6/8/2012 >>>>>

 - Moved defined constants to be constituted as channels.  This will allow
   MoTeC global maths to be able to use these values.

 - Modified the internal method of handling the data to improve performance.
 
 
<<<<< Changes for 1.2.8.0 - 4/24/2012 >>>>>
 
 - Added CFSRrideHeight channel.  It will appear as Ride Height FS in MoTeC.
 
 - Changed cfg file format and name.  Please see the readme section on the cfg
   file for more information.  The old carinfo.cfg will still work.  The new
   format will apply to files named vehicleinfo.cfg.


<<<<< Changes for 1.2.7.0 - 2/21/2012 >>>>>

 - Now exports Fuel Density as a Math Constant.
 
 
<<<<< Changes for 1.2.6.0 - 12/25/2011 >>>>>

 - Settings window now saves and restores its location and size.
 
 
<<<<< Changes for 1.2.5.0 - 12/8/2011 >>>>>
 
 - Fixed issue with vehicle id not being set.
 
 - Fixed issue with deleting exported ibt files.
 
 
<<<<< Changes for 1.2.4.0 - 12/6/2011 >>>>>

 - Fixed issue with kPa not converting correctly.
 
 - Fixed issue with Nm not converting correctly.
 
 
<<<<< Changes for 1.2.3.0 - 11/11/2011 >>>>>

 - Fixed invalid string position error.
 
 
<<<<< Changes for 1.2.2.0 - 11/10/2011 >>>>>

 - Fixed crash.
 
 - Added Velocity and Yaw/Pitch/Roll channels.
 
 
<<<<< Changes for 1.2.1.0 - 11/9/2011 >>>>>

 - Added ability to delete telemetry files that are under the set threshold.
 
 
<<<<< Changes for 1.2.0.0 - 11/9/2011 >>>>>

 - Added ability to delete telemetry files that have already been exported.
 
 - Added ability to not export telemetry files whose laps are below a threshold.

 - Increased precision of recorded data from 16bits to 32bits.
 
 - Added ability to automatically calculate dps.
 
 - Refactored the importer to abstract ability to process real-time and exported telemetry.
 
 - Optimized the importer.
  
 - Optimized iterating over telemetry files in the source directory.
 
 - Fixed error with fasted lap time calculation.
 

<<<<< Changes for 1.1.1.0 - 6/27/2011 >>>>>

 - Increased precision for the tire pressure channel.
 
 
<<<<< Changes for 1.1.0.0 - 6/23/2011 >>>>>

 - Added channel mappings for Tire Temps and Pressures.
 
 
<<<<< Changes for 1.0.0.0 - 6/16/2011 >>>>>

 - Cleaned up code. Minor performance increase.
    

<<<<< Changes for 0.10.0.0 - 6/5/2011 >>>>>

 - Added Unicode support. System's running non-English character sets (ie
   Cyrillic, Kanji, etc.) will no longer have issues.
 
 - Fixed pathing issue with placing the carinfo.cfg in the import or export
   directory.
   

<<<<< Changes for 0.9.3.0 - 6/3/2011 >>>>>

 - Updated the XXSHshockDefl and XXshockDefl channels to export to the
   channels specified by Eric Hudec in this post: 
   http://members.iracing.com/jforum/posts/list/1477193.page#3396551
   
 - Raw telemetry now contains all the channels (including those already mapped
   to MoTeC equivalents) that iRacing exports.
   
 - Performed another round of optimizations; reducing export time by 1/3.
 

<<<<< Changes for 0.9.2.0 - 6/2/2011 >>>>>

 - Fixed % conversion.


<<<<< Changes for 0.9.1.0 - 6/2/2011 >>>>>

 - Added small delay to auto-enabling telemetry so as to give iRacing a chance
   to catch it.
   
   
<<<<< Changes for 0.9.0.0 - 6/1/2011 >>>>>

 - Added ability for Mu to automatically turn Telemetry in iRacing on when the
   simulation starts.
   
 - Added ability to select 'None' for an exporter.  This will allow users to
   use Mu without having MoTeC telemetry exported.
   
 - Optimized the exporter to be even faster.
 

<<<<< Changes for 0.8.2.0 - 5/25/2011 >>>>>

 - Set the create/modified/and last access for exported files to be the same
   as imported files.
   
 - Moved CRRideHeight into its own channel to avoid conflicts.
 
 - Fixed problem where the yaml parser would crash when driver indexes were
   not sequential.
   

<<<<< Changes for 0.8.1.0 - 5/23/2011 >>>>>

 - Fixed issue problem where the existance check for the config file would
   return back false even if it existed.
   
 - Added ability for the config file to reside in the import directory or
   export directory as well as the exe directory.
   
 - Set the timestamps of the exported files to be the same as the import
   file.
   
 - Added more logging.
 
 
<<<<< Changes for 0.8.0.0 - 5/22/2011 >>>>>

 - Added ability to define car info such as fuel capacity, wheelbase, track,
   and weight through a configuration file.  See the Notes for details.
   
 - Added session weather information into the MoTeC file.
 
 - Fixed 'miles' unit label that would give problems with MoTeC.
 
 - Changed the SHShockDefl channel to export as Susp Pos.
 

<<<<< Changes for 0.7.9.0 - 5/17/2011 >>>>>

 - Fixed error that could happen if a discontinuity is detected in 
   consecutive sequences.
   
 - Added check to make sure that user entered Import and Export directories 
   are in fact valid directories.


<<<<< Changes for 0.7.8.0 - 5/17/2011 >>>>>

 - Fixed the stint detection code to handle cases where there is only 1 
   sequence to parse.  This should fix the 'vector<T>' error some are
   experiencing.
   
 - Fixed issue with Mu aborting all exports if there in an error. It will
   now add the bad export file to an exclusion list and carry on with
   exporting the other telemetry files.
    
 - Changed Steered Angle to Steering Wheel Angle.
    
    
<<<<< Changes for 0.7.7.0 - 5/11/2011 >>>>>

 - Fixed issue with miles not being converted due to typo in the converter's
   lookup table.
   
 - Fixed copy error that resulted in metric units label being applied to
   english units.
   
 - Fixed issue with the metric dps being applied to english units.
 
 
<<<<< Changes for 0.7.6.0 - 5/10/2011 >>>>>

 - Fixed problem with exporter causing MoTeC to crash.
 
 - Fixed issue with importer that would sometimes incorrectly split stints.
 
 - Fixed problems that would arise when the Laps channel would decrement.
 
 - Added more checks to avoid including '0' sequence data that would come from
   iRacing on a reset.
   
 - Updated to use irsdk v1.02
  
 
<<<<< Changes for 0.7.5.0 - 5/8/2011 >>>>>
 
 - Added support to export multiple stints of MoTeC files based on the user
   resetting the car.  This will fix a slew of problems with MoTeC failing
   to correctly report the car's telemetry due to it teleporting.
   
 - Changed exporter to avoid exporting data that would cause MoTeC to crash.

 - Optimized the unit conversion routine. Mu should export ~50% faster.
 
 - Changed importer to cull sequences of 0 data when resetting the car.
 
 - Fixed the reporting of the Fastest Lap.
 
 - Fixed problem with the wrong decimal precision being applied to certain channels.
 
   
<<<<< Changes for 0.7.4.0 - 5/7/2011 >>>>>
 
 - Added option to export all channels iRacing delivers. Note however that those
   channels not supported by Mu will display the data as how iRacing exports it.
   
 - Added support for the shock deflection channels for the COT.
 
 - Added support for the center ride height channel for the FW31.
 
   
<<<<< Changes for 0.7.3.0 - 5/4/2011 >>>>>

 - Fixed issue when exporting telemetry to a directory other than the default.
 
 - Fixed issue when changing directories in the middle of an export.
 
 - Changed behavior so that Mu doesn't attempt to spam-export a failed export.
   

<<<<< Changes for 0.7.2.0 - 5/4/2011 >>>>>

 - Added Ride Height Center channel.
 
 - Fixed issue with MoTeC Exporter when a channel didn't have channel data.
 
 - Changed metric units for Ride Height and Damper Position to mm.
  

<<<<< Changes for 0.7.1.0 - 5/3/2011 >>>>>

 - Fixed race-condition crash (heh..heh..) where Mu would attempt to read telemetry
   files while iRacing was still writing them.
   
 - Fixed issue with DriverInfos returning the wrong driver.
 

<<<<< Changes for 0.7.0.0 - 5/3/2011 >>>>>

 - Support for irsdk v1.01.
 
 - Redesigned the engine to parse iRacing .ibt files including retreiving data from iRacing.
 
 - Redesigned the exporter.
 
 - Removed iWrap (no longer needed with the new iRacing SDK).


<<<<< Changes for 0.6.2.0 - 11/11/2010 >>>>>

 - Fixed issue with LatG overflowing when using the FW31.
 

<<<<< Changes for 0.6.1.0 >>>>>

 - Fixed RL tire tempurature typo.
 
 - Fixed issue with LongG overflowing when using the FW31.
 

<<<<< Changes for 0.6.0.0 >>>>>

 - Support for iRacing Season 4 2010
 
 - Support for iWrap version 1.0.0.2
 
 - Added ability to export new data exposed by iRacing, including 
   Tire Temp and Pressure data.
 
 - Refactored connection logic to fix errors with iRPS Proxy servers.
 

<<<<< Changes for 0.5.1.0 >>>>>

 - Included latest iWrapClient.dll. 
 
 
<<<<< Changes for 0.5.0.0 >>>>>

 - Added support for iWrap Proxy.  Pre-release only.
 

<<<<< Changes for 0.4.1.0 >>>>>

 - Fixed exporter compatibility for MoTeC i2 Pro v1.10.0035.


<<<<< Changes for 0.4.0.0 >>>>>

 - Changed metric export option to export degrees.
 
 - Implemented better algorithm for determining player information.
 
 - Fixed issue with incorrect vehicle being exported if the user changed
   cars.
 

<<<<< Changes for 0.3.3.0 >>>>>

 - Fixed issue with Velocity Y overflowing.
 

<<<<< Changes for 0.3.2.0 >>>>>

 - Fixed issue with steering torque.
 

<<<<< Changes for 0.3.1.0 >>>>>

 - Added option to turn off voice cues.
 
 - Fixed problem with setting the export directory.
 
 
<<<<< Changes for 0.3.0.0 >>>>>

 - Added ability to export in English units.
 
 - Removed limit for logging telemetry.  Telemetry will now continue to
   record until exported or the system runs out of memory.
 

<<<<< Changes for 0.2.3.0 >>>>>

 - Fixed issue with lap beacons not reseting between stints.
 
 - Fixed issue with MoTeC interpreting 60Hz as 61.440Hz.
                   

<<<<< Changes for 0.2.2.0 >>>>>

 - Changed temporary download location to fix issue with Win7/Vista not 
   updating correctly.

   
<<<<< Changes for 0.2.1.0 >>>>>

 - Fixed issue with settings not propogating during upgrading.
 
 - Added sanity checks when choosing the export directory.
 
 - Added automatic setting to the default directory if the current set 
   directory doesn't exist.
   
 - Fixed connection failed and export failed sounds.
    

Acknowledgements
------------------------------------------------------------------------------
- iRacing.com Motorsport Simulations for creating the best PC racing
  simulation.
  
- MoTeC for their excellent telemetry analysis program i2 Pro.

- Special thanks to fellow iRacers Dan Rasch, Remy Lozza, and Austin Hervias for their
  feedback and suggestions.
