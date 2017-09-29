# Mu - Telemetry Exporter for iRacing
Developed by Patrick Moore (patrickwmoore@gmail.com)
Version 1.8.2.0
Last update: 12/20/2016

Overview
------------------------------------------------------------------------------
Mu is a telemetry exporter that converts iRacing telemetry files (.ibt) into
to files that can be read by MoTeC's i2 software for analysis. i2 and i2 Pro
are available for free on MoTeC's website. MoTeC has no affiliation with
iRacing. Please do not ask them for support.

Mu has the following features:
 - Can export to MoTeC and CSV formats
 - Can export Metric or Imperial units
 - Automatically turns on telemetry capture in iRacing
 - Saves a copy of the setup used to generate the telemetry


Usage
------------------------------------------------------------------------------
Mu can be run with iRacing or on its own.  Mu will monitor the Import 
Directory and export any telemetry automatically. Exported telemetry can then
be analyzed by the software of your choice.

When Mu is run in conjunction with iRacing, Mu can automatically turn on
Telemetry Capture and save the setup that was used to generate the telemetry. 

Mu has a user interface (UI) that will appear when launched. Additionally, it
will continue to run in the background if the UI is closed. Mu is accessible
from the Windows system tray, and right-clicking will display a dialogue with
options for exiting the program, displaying the UI, and other functions.


GPS
------------------------------------------------------------------------------
GPS in iRacing allows for an alternative way to determine the position of the
car on the track, the generation of laps, and the generation of the trackmap.

Due to precision of the MoTeC data, GPS data needs to be combined from
multiple channels (actual race teams need to do this as well).  GPS Telemetry 
data is exported in 3 channels (Degrees, Minutes, Seconds), and must be 
combined by MoTeC Maths into the channels GPS Latitude and GPS Longitude.  The 
Math formula you should use is as follows:

```
  GPS Latitude - Quantity: Angle  Display Unit: degree  Decimal: 8 
                 Result Unit: Degree
				 Expression: 'Latitude Degrees' + 'Latitude Minutes' / 60.0 
				             + 'Latitude Minute - fraction' / 3600
  
  GPS Longitude - Quantity: Angle  Display Unit: degree  Decimal: 8 
                  Result Unit: Degree
			      Expression: 'Longitude Degrees' + 'Longitude Minutes' / 60.0 
				  + 'Longitude Minute - fraction' / 3600.0
```


Additional Configuration - vehicleinfo.cfg
------------------------------------------------------------------------------
Mu supports loading of car information from an configuration file.  To
define the configuration file, create a text file with the name 
'vehicleinfo.cfg' in either the same directory as the Mu executable, the 
import directory, or the export directory.  The file must be in YAML format.

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


####Vehicle Information
Additional vehicle information can be exported into MoTeC that can be used in
Maths or just general information.  An example of a vehicle entry is as follows

```
  Vehicles:
  - name: formulamazda
    Attributes:
      Vehicle Weight: 650 kg
      Fuel Tank Capacity: 72 l
```

Additional vehicles and attributes can be added.  See the sample below for a
complete example of how to add more vehicles and attributes.  Only the values
for the vehicle used in generating the telemetry will be included in the export.


####Constants
Constants are similar to vehicle information except that the values are exported
for all telemetry.

```
  Constants:
    Minimum Laps: 2
    Acceleration of Gravity: 9.8 m/s^2
```


####Filtering Channels
Channels can be filtered by adding a ChannelFilter entry and listing the name
of each channel to be filtered.  Note that if you filter a channel needed by
Motec, you could end up with missing / erronous telemetry.

```
  ChannelFilter:
    - ChannelName1
    - ChannelName2
```


####Sample vehicleinfo.cfg
Below is a sample configuration used by Mu.  The following can be cut-n-pasted
to vehicleinfo.cfg

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
    
  ChannelFilter:
    - RPM
    - Gear
```


Acknowledgements
------------------------------------------------------------------------------
- iRacing.com Motorsport Simulations for creating the best PC racing
  simulation.
  
- MoTeC for their excellent telemetry analysis program i2 Pro.
