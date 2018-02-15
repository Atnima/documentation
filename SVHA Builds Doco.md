# SVHA Builds Doco - Last updated 4.2.x

## Summary

The SVHA Builds have been incorporated into a single task sequence for ease of use. The build includes a UI++ based user interface allowing customisation of timezone and office version, and also manages the device name input and matches it against a required format.

There are currently requirements for multiple Windows versions within SVHA, namely Windows 10 for new builds for national migrated devices, however NSW devices are still on a Windows 7 platform with a 6 month timeframe for completion (Q3 2018).

## Automated Builds

The ability to build a device automatically with no user input has been incorporated into the SVHA Builds from version 4.2. In order to accomplish this the device must satisfy all normal requirements for an automated build (such as power management etc), but the collection must also have 2 collection variables set to ensure the UI is skipped and the correct version of Office is installed.

When setting up the collection please set the following two collection variables:
- SchedDeploy <br>
This must be set to TRUE to skip the UI++ dialogue
- SchedDeployOffice <br>
This can be one of (currently) two values. "365" will install Office 365 as part of the OSD. "2016x86" will install 32-bit Office 2016.

The collection variables can be spread across multiple collections if required. For example you could have collections indicating which office version seperate from collections that set SchedDeploy to "True" with the OSD advertised.

## Variables
There are a number of variables used within both the Task Sequence and the UI++ application, for the purposes of this documentation and simplicity, only the variables used within the task sequence will be detailed.

- SVHAApplyDirect <br>
*True // False* <br>
This variable sets whether or not the task sequece should use a new, EXE type driver package. If this is set to true the task sequence will apply a "Critical Network and Storage Drivers" package to ensure network connectivity after the boot into Windows, but will skip applying SCCM based driver packages. The EXE driver package, to be detailed later, will then apply.

- WindowsVersion <br>
*10 // 7* <br>
Sets which version of Windows will be applied during the task sequence.

- SVHABuildVersion <br>
*1607 // 1709* <br>
Sets the version of Windows 10 applied if applicable. Used when a new OS version is under test.

- SVHAOffice <br>
*CTR86 // VLK1386 // VLK86 // VLK64 // NONE* <br>
Sets the version of Office to be installed during the build, this is only applicable for a Windows 10 build.

- SVHALocation <br>
*BRIS // SYD // MEL* <br>
Sets the timezone in the build. This is accomplished using multiple "Apply Windows Settings" steps.

- SVHADomainJoinBug <br>
*True // False* <br>
Determines whether the device should join a domain first and then wait for network connectivity post reboot to join the domain.

- SchedDeploy <br>
*True // Not Set* <br>
This variable is used in an automated build scenario to skip the UI++ dialogues and set key task sequence variables such as Windowsvand Office versions.

- SchedDeployOffice <br>
*365 // 2016x86* <br>
If the build is automated, sets the Office version.































