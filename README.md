# Touch Portal Plugin for Open Hardware Monitor

TouchPortal Plugin to Utilize Statistics from Open Hardware Monitor - for Windows

- [Touch Portal Plugin for Open Hardware Monitor](#touch-portal-plugin-for-open-hardware-monitor)
  - [Current Sensors and Values Available](#current-sensors-and-values-available)
        - [Data Types](#data-types)
      - [CPU](#cpu)
      - [GPU](#gpu)
      - [RAM](#ram)
  - [Gauges and Graphs ++New in v4](#gauges-and-graphs-new-in-v4)
  - [Sample Page](#sample-page)
  - [Sample Buttons for Bargraphs and Gauges ++New in v4](#sample-buttons-for-bargraphs-and-gauges-new-in-v4)
  - [Events](#events)
    - [CPU Total Load Status](#cpu-total-load-status)
    - [Memory Load Status](#memory-load-status)
    - [CPU Package Temperature Status](#cpu-package-temperature-status)
    - [GPU Core Load Status](#gpu-core-load-status)
    - [GPU Memory Load Status](#gpu-memory-load-status)
    - [GPU Core Temperature Status](#gpu-core-temperature-status)
    - [GPU Memory Temperature Status](#gpu-memory-temperature-status)
  - [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installing](#installing)
  - [Updating](#updating)
    - [** Note for v5 **](#-note-for-v5-)
    - [Pre-v5 upgrade to v5](#pre-v5-upgrade-to-v5)
  - [Configuration](#configuration)
  - [Troubleshooting](#troubleshooting)
  - [Notes](#notes)
  - [Built With](#built-with)
  - [Build It](#build-it)
  - [Versioning](#versioning)
  - [Authors](#authors)
  - [License](#license)
  - [Acknowledgments](#acknowledgments)

## Current Sensors and Values Available

__*NOTICE*__: Not all sensors configured will work with your computer, there may be some that don't show anything, and other sensors that I didn't know about were even available so have to be configured to work.  If there is one I missed open an Issue with your attached OHM report and the sensor you are requesting and it will get put on the log.

These are the current sensors and values available via this plugin. This information will be transmitted back to Touch Portal every 1 seconds. If this becomes a problem I'll probably extract this out into a configuration file so it can be controlled by you.

##### Data Types

- Percentage - values 0.0 - 100.0
- Treshold - Coded by sensor and documented below to return "grouped" status data
- SmallData - values are in MB
- Data - values are in GB
- Clock - values are in MHz
- Temperature - values are in °C
- Power - values are in W (watts)

_Note: All Decimals are to the tenths place. I chose not to include the symbol and only the numbers so you can choose how they display_

#### CPU

- **Total CPU Load** - Percentage
  - state id is `tpohm_cpu_total_load_val`
- **CPU Status** (based on Total Load) - Threshold
  - state id is `tpohm_cpu_total_load_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 45% of CPU is used
      - `Medium` is when &lt; 85% of CPU is used
      - `High` is when &gt;= 85% of CPU is used
- **CPU Core Load Values 1-16 Cores** - Percentage
  - state ids are `tpohm_cpu_core_1_load_val` - `tpohm_cpu_core_16_load_val`
- **CPU Core Clock Values 1-16 Cores** - Clock
  - state ids are `tpohm_cpu_core_1_clock_val` - `tpohm_cpu_core_1_clock_val`
- **CPU Package Temperature** - Temperature
  - state id is `tpohm_cpu_package_temp_val`
- **CPU Package Temperature Status** - Threshold
  - state id is `tpohm_cpu_package_temp_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 45°C
      - `Medium` is when &lt; 65°C
      - `High` is when &gt;= 65°C
- **CPU Package Power** - Power
  - state id is `tpohm_cpu_package_power_val`

#### GPU

- **Total GPU Load** - Percentage
  - state id is `tpohm_gpu_core_load_val`
- **GPU Status** (based on Total GPU Load) - Threshold
  - state id is `tpohm_gpu_core_load_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 45% of GPU is used
      - `Medium` is when &lt; 85% of GPU is used
      - `High` is when &gt;= 85% of GPU is used
- **Total GPU Memory Load** - Percentage
  - state id is `tpohm_gpu_memory_load_val`
- **GPU Memory Status** (based on Total GPU Memory Load) - Threshold
  - state id is `tpohm_gpu_memory_load_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 40% of GPU Memory is used
      - `Medium` is when &lt; 85% of GPU Memory is used
      - `High` is when &gt;= 85% of GPU Memory is used
- **GPU Core Clock** - Clock
  - state id is `tpohm_gpu_core_clock_val`
- **GPU Memory Clock** - Clock
  - state id is `tpohm_gpu_memory_clock_val`
- **GPU Shader Clock** - Clock
  - state id is `tpohm_gpu_shader_clock_val`
- **GPU Core Temperature** - Temperature
  - state id is `tpohm_gpu_core_temp_val`
- **GPU Core Temperature Status** - Threshold
  - state id is `tpohm_gpu_core_temp_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 40°C
      - `Medium` is when &lt; 60°C
      - `High` is when &gt;= 60°C
- **GPU Power** - Power
  - state id is `tpohm_gpu_power_val`
- **GPU Memory Free** - SmallData
  - state id is `tpohm_gpu_free_memory_val`
- **GPU Memory Used** - SmallData
  - state id is `tpohm_gpu_used_memory_val`
- **GPU Memory Temperature** - Temperature - Maybe AMD Only
  - state id is `tpohm_gpu_memory_temp_val`
- **GPU Memory Temperature Status** - Threshold - Maybe AMD Only
  - state id is `tpohm_gpu_memory_temp_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 40°C
      - `Medium` is when &lt; 60°C
      - `High` is when &gt;= 60°C

#### RAM

- **Total Memory Load** - output the raw current percentage (to 1 decimal point) of Memory Load
  - state id is `tpohm_memory_load_val`
    - Values are: 0.0 - 100.0
- **Memory Status** (based on Total Load) - called a Threshold in the code
  - state id is `tpohm_memory_load_status`
    - Final Values are: `Low, Medium, High`
      - `Low` is when &lt; 40% of Memory is used
      - `Medium` is when &lt; 85% of Memory is used
      - `High` is when &gt;= 85% of Memory is used
- **Used Memory** - Data
  - state id is `tpohm_used_memory_val`
- **Available Memory** - Data
  - state id is `tpohm_avail_memory_val`

## Gauges and Graphs ++New in v4

With the SDK update to 2 and 2.2 of Touch Portal being released, you can now have images sent from plugins back to Touch Portal.

So with that I wanted to test out (minimal at first) with a few different options. 

**CPU and GPU Load Bar Graph**

You can now have an icon updated on your screen with a bar graph representation of each reading from OHM. This is accomplished by using this action and event combination on the button you want to have the icon shown on.

![TP OHM CPU Load Bargraph](images/tp_ohm_cpu_load_bargraph.png)
![TP OHM GPU Load Bargraph](images/tp_ohm_gpu_load_bargraph.png)

*NOTE*: This updates every time the plugin runs an update, so again if your mobile device is struggling, maybe increase the time between sends in the config file.

**CPU and GPU Load Gauge**

You can now have an icon updated on your screen with a gaguge representation of each reading from OHM. This is accomplished by using this action and event combination on the button you want to have the icon shown on.

![TP OHM CPU Load Gauge](images/tp_ohm_cpu_load_gauge.png)
![TP OHM GPU Load Gauge](images/tp_ohm_gpu_load_gauge.png)

*NOTE*: Unlike the bar graph, this only updates if the previous value is different than the next read value.

## Sample Page

I have created a sample page that can be imported directly into Touch Portal and consume all possible values state values (feel free to edit how you see fit or just use this as a guide).
Download and import this page: [TP OHM Page](resources/OHM%20Page%20Example.tpz)

![TP OHM Screenshot](images/tp_ohm_screenshot.png)

Here is a gif of it in action on my phone (*note:* slightly different than existing page):

![TP OHM Example on iPhone XSMax](images/tp_ohm_page_on_phone.gif)

## Sample Buttons for Bargraphs and Gauges ++New in v4

These are all 1x1 buttons but were on a 4 x 3 landscape screen

CPU Load Gauge - import this button: [TP OHM CPU Load Gauge Button](resources/tp_ohm_cpu_load_gauge.tpb)

CPU Load Bargraph - import this button: [TP OHM GPU Load Bargraph Button](resources/tp_ohm_cpu_load_bargraph.tpb)

GPU Load Gauge - import this button: [TP OHM GPU Load Gauge Button](resources/tp_ohm_gpu_load_gauge.tpb)

GPU Load Bargraph - import this button: [TP OHM GPU Load Bargraph Button](resources/tp_ohm_gpu_load_bargraph.tpb)


## Events

### CPU Total Load Status

This event is triggered off the state id `tpohm_cpu_total_load_status`

Example:

![TP OHM CPU Total Status](images/tp_ohm_cpu_total_status_event.png)

### Memory Load Status

This event is triggered off the state id `tpohm_memory_load_status`

Example:

![TP OHM Memory Status](images/tp_ohm_memory_status_event.png)

### CPU Package Temperature Status

This event is triggered off the state id `tpohm_cpu_package_temp_status`

Example:

![TP OHM CPU Temperature Status](images/tp_ohm_cpu_temperature_status_event.png)

### GPU Core Load Status

This event is triggered off the state id `tpohm_gpu_core_load_status`

Example:

![TP OHM GPU Core Load Status](images/tp_ohm_gpu_core_load_status_event.png)

### GPU Memory Load Status

This event is triggered off the state id `tpohm_gpu_memory_load_status`

Example:

![TP OHM GPU Memory Load Status](images/tp_ohm_gpu_memory_load_status_event.png)

### GPU Core Temperature Status

This event is triggered off the state id `tpohm_gpu_core_temp_status`

Example:

![TP OHM GPU Temperature Status](images/tp_ohm_gpu_temperature_status_event.png)

### GPU Memory Temperature Status

This event is triggered off the state id `tpohm_gpu_memory_temp_status`

NOTE: This may be AMD GPU only

Example:

![TP OHM GPU Memory Temperature Status](images/tp_ohm_gpu_memory_temperature_status_event.png)

## Getting Started

If you use [Touch Portal](https://touch-portal.com) and are interested in having a "dashboard" display of some base computer statistics, these instructions will help get that setup for you.

If you don't use Touch Portal - how dare you, you should!

## Prerequisites

Download and run Open Hardware Monitor - you can find it here: https://openhardwaremonitor.org/
Current tested version is 0.9.5

Location of where it is downloaded and run from do not matter, as long as it is running and writing sensor data it can run from anywhere on the computer.

After download, run the OpenHardwareMonitor.exe file, for this plugin to run correctly, please enable the following "Options" menu items:

![OHM Options](images/ohm_options.png)

## Installing

_**NOTE**_: Default install path is dictated by Touch Portal, for newer users it is in %APPDATA%\TouchPortal\plugins, for older users it is in C:\Users\(window user name)\Documents\TouchPortal\plugins\ (or wherever your documents folder is)

**Step 1** Make sure you have Open Hardware Monitor installed - go to Prequisites if you did not install it

**Step 2** Download the Touch Portal Plugin [TP_OHM_Plugin.tpp](installer/TP_OHM_Plugin.tpp) file from the github repo installer folder. This contains everything needed for TouchPortal and the Plugin

**Step 3** Open Touch Portal GUI, go to the Wrench, and chose "Import plug-in"

![TP Import Plug-In](images/tp_import_plugin.png)

**Step 4** Navigate to where youd downloaded the .tpp file from Step 1, select it and click "Open"

**Step 5** You then should see this, click "Okay"

![TP Import Plug-In Success](images/tp_import_plugin-success.png)

**Step 6** Now restart the Touch Portal app

 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; _**NOTE**_: Make sure you fully close Touch Portal using System Tray icon to exit

**Step 7** After Touch Portal is back open and this is your first time installing TP Open Hardware Monitor you will be presented with a "trust" screen - code here is all open source - if you trust the plugin, select "Trust Always" or else everytime you open the app it will ask you:

![TP Plug-In Trust](images/tp_plugin_trust.png)

**Step 8** Now that we are trusted, click on an empty button and if you scroll down in the "Add Actions" list, you should see:

![Open Hardware Monitor Info Events](images/open_hardware_monitor_events.png)

**Step 8** Now you can move onto the Sample Page or start creating your own buttons to use this data.

## Updating

### ** Note for v5 ** 
These steps will no longer be necessary after getting to version 5, the plugin will now respond to TouchPortal's Close command on shutdown of TouchPortal, loading of an updated plugin .tpp, as well as when using the Stop button in the Settings->Plugins
You will just be able to import a new plugin without worrying about manually stopping it

### Pre-v5 upgrade to v5
For previous versions to v5 you will still have to follow these instructions

When an update is put out, please follow these instructions to install

**Step 1** Open Windows Task Manager

**Step 2** Locate tp_ohm.exe running (you may see 2 listed but only 1 is actually running) and end the task, kill the one that actually is consuming CPU the one with the camel icon in the picture)

![TP OHM Exe Task Manager](images/tp_ohmexe_task_manager.png)

**NOTE**: If you don't see it running under Java like above, scroll down in your task manager to find it by itself

**Step 3** Download the newest .tpp from the install directory

**Step 4** to to Step 3 of the install guide and load the plugin

## Configuration
The config file is in the plugins\OpenHardwareMonitor folder and it is called tp_ohm.cfg. It is a JSON formatted file. 

The file looks like below, and the value is in milliseconds. So by default, the update Interval is every 2000 milliseconds, or 2 seconds.  

```json
{
    "updateInterval": "2000",
    "needleColor":[0,0,255],
    "barGraphColor": [0,0,255]
}
```

**Configuration Options**

* updateInterval - how often (in ms) do you want updates sent to TouchPortal.  Realistically every 2 seconds is fine, older mobile devices may not handle the updates to a page well that often, so I suggest lowest is 2000, and raise that if your mobile device is having issue rendering the data. 
    * __*NOTE: Changing this is at your own risk. Your computer may not handle this as well as others, and it may cause higher than normal CPU usage if you are trying to update faster than every 2000 milliseconds.*__

* needleColor - the needle color of the gauge icon that is rendered. this is [ R, G, B ] format - so find the color you want, find the RGB value, and put each value in the correct position here. (default: 0,0,255 is blue)

* barGraphColor - the bar graph line color that is rendered. this is [ R, G, B ] format - so find the color you want, find the RGB value, and put each value in the correct position here. (default: 0,0,255 is blue)

To edit the file just open in notepad or your favorite text editor and modify the number only. If you break the formatting it will kill the program, at the next restart

Once you are done editing save the file, and then close and reopen Touch Portal, as tp_ohm.exe does not re-read this file every execution cycle (*because that would be silly... or would it.. maybe another time*)


## Troubleshooting

Touch Portal will log that it attempted to load the plugin in it's log file
%APPDATA%\TouchPortal\log.txt

when it loads the Plugin it should look like this

```
00:48:02 - [LOG] (Plugin System) Searching and loading plugins...
00:48:02 - [LOG] (Plugin System) (127.0.0.1) Waiting for request on port 12136...
00:48:02 - [LOG] (Plugin System) Added Category: Open Hardware Monitor Info
```

and a little lower you should see something like this:

```
00:48:08 - [LOG] (Plugin System) Executing plugin service: "C:\Users\<USERNAME>\AppData\Roaming\TouchPortal\plugins\OpenHardwareMonitor\tp_ohm.exe"
```

There is also a logfile under the OpenHardwareMonitor plugin folder, %APPDATA%\TouchPortal\plugins\OpenHardwareMonitor\tp_ohm.log

```
[START] tp_ohm is starting up, and about to connect
[FATAL] Cannot create socket connection : ##
```
- Verify your Touch Portal is actually running

```
[START] tp_ohm is starting up, and about to connect
[FATAL] Unable to connect to WMI...
```

- Verify you followed the Prequisite section and installed Open Hardware Monitor, otherwise your user may not have access to read from WMI - please follow [this link](https://docs.bmc.com/docs/display/public/btco100/Setting+WMI+user+access+permissions+using+the+WMI+Control+Panel), but for OpenHardwareMonitor folder instead of CIMV2 to set your user up to access WMI

If you do not see those messages, make sure you followed the Prerequisites section, otherwise visit the #tp-ohm channel on the Touch Portal Discord and we can troubleshoot it when I'm available

_INFO: more notes will be added here as we have to troubleshoot_

## Notes

- this has only been tested on Windows 10 Pro, your mileage my vary
- this was tested on a single CPU Desktop machine, your mileage may vary.
- If you experience issues with the plugin please submit an issue with a saved copy of your Open Hardware Monitor report (File -> Save Report), and it will be reviewed as time permits

## Built With

- [StrawberryPerl](http://strawberryperl.com/) - Coding Language
- [PAR::Packaging](https://metacpan.org/pod/pp) - EXE Packaging Utility
- [Win32::OLE](https://metacpan.org/pod/Win32::OLE) - Used to access the WMI information

## Build It

Building reqiures Par::Packaging (pp) for Perl - and to be located in the src/perl directory of the project

```shell
pp @libs.txt tp_ohm.pl -p tp_ohm.exe
```

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/spdermn02/tpohm_plugin/tags).

## Authors

- **Jameson Allen** - _Initial work_ - [Spdermn02](https://github.com/spdermn02)

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details

## Acknowledgments

- Thank you to Open Hardware Monitor for writing your statstics somewhere accessible
- Thank you to Ty and Reinier for creating and developing Touch Portal
