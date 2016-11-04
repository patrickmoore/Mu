# Mu - Telemetry Exporter for iRacing
Developed by Patrick Moore (patrickwmoore@gmail.com)  
Last update: 11/4/2016


Overview
------------------------------------------------------------------------------
Mu is a telemetry exporter that converts iRacing telemetry files (.ibt) into
to files that can be read by MoTeC's i2 software for analysis. i2 and i2 Pro
are available for free on MoTeC's website. MoTeC has no affiliation with
iRacing. Please do not ask them for support.

Mu has the following features:
 - Can export to MoTeC
 - Can export to CSV
 - Can export Metric or Imperial units
 - Automatically turns on telemetry capture in iRacing
 - Saves a copy of the setup used to generate the telemetry


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
```
  GPS Latitude - Quantity: Angle  Display Unit: degree  Decimal: 8  
		 Result Unit: Degree  
		 Expression: 'Latitude Degrees' + 'Latitude Minutes' / 60.0 + 'Latitude Minute - fraction' / 3600.0  
  
  GPS Longitude - Quantity: Angle  Display Unit: degree  Decimal: 8 
		  Result Unit: Degree  
		  Expression: 'Longitude Degrees' + 'Longitude Minutes' / 60.0 + 'Longitude Minute - fraction' / 3600.0  
```
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

```
---
Vehicles:
- name: formulamazda
  Attributes:
    Vehicle Weight: 650 kg
    Fuel Tank Capacity: 72 l
    Vehicle Track: 1485 mm
    Vehicle Wheelbase: 2522 mm

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
```


  Additional cars can be added on as long as the format is followed.  The car's
  name must be identical to the iRacing directory name of the car.  Vehicle
  Weight, Fuel Tank Capacity, Vehicle Track, and Vehicle Wheelbase are
  specially named in MoTeC and appear in the Detail section along with being
  used in Maths.
  
  Additional attributes and constants can be added as long as the format is
  followed.
  
  Units can be given in the following quantities. Usage of quantities not 
  explicitly labeled below will result in incorrect data in MoTeC:

```
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
```
  
Latest Changes
------------------------------------------------------------------------------

 - Added sanitization of malformed yaml from iRacing.

 - Reworked installer to try and fix updating issues.
    

Acknowledgements
------------------------------------------------------------------------------
- iRacing.com Motorsport Simulations for creating the best PC racing
  simulation.
  
- MoTeC for their excellent telemetry analysis program i2 Pro.
