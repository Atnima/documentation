# Build Revisions

This will act as a changelog for the "OSD - Deploy - SVHA Builds x.x.xx" task sequence. Changes here will be detailed to ensure easy understanding and rollback.

## Major Version 4.1
This release was intended to fully update the Windows 7 image in use for a number of reasons:
- Updates were not complete, while somewhat patched there were critical patches missing that were being resolved once picked up in SCCM
- Language and Region settings were not correct
- Office was presenting the user with an "unlicenced" prompt when attempting to use any Office product for the first time.
- The password scrambler was not working in Windows 7 and the local admin password was not known
- Updated Firmware and Drivers to latest MSFT supplied MSI's as at 20/01/2018

High Performance Power Management has been added to both the Windows 10 and Windows 7 builds to improve build times. Reports indicate builds can be up to 40% faster using this method. The sequence activates High Performance settings after any system reset and sets the defaults (balanced) at the end of the sequence. Benchmarking on SVHA devices has not been completed.

#### *Known Issues*
- Surface Pro devices that are not running the latest firmware on the device itself or the dock, may have no network connectivity on completion of the build. This is due to the firmware upgrade process that needs to run over a number of reboots. A reboot should resolve the issue.
- Password scrambler isnt working for Windows 7, the root cause is unknown and until it can be resolved we will continue to use the existing SVMHS local administrator password.

### 4.1.17
- Release Version

### 4.1.16
- Added log collection in for failed task sequences
- Modified critical driver application in Win7 to apply using DISM with the recurse tag to resolve error
- Added restart for Windows 7 post unattend application reboot due to sporadic issue with RPC server being unavailable

### 4.1.15
- Attempted to move driver application step to resolve issue in NSW where the device was failig to apply critical network and storage (win7)

### 4.1.14
- Release Candidate 1

### 4.1.13
- Added monitor timeout fix to prevent the screen going to sleep during OSD.
- Removed password scrambler for Windows 7 for now - using existing static local admin password.

### 4.1.12
- Moved password scrambler to after the second reboot for Windows 7 - the thinking is that it isnt setting or is reverting due to it being the first boot into windows.
- Removed Group Policy updater script after finding evidence that all group policy related actions are surpressed during an OSD and therefore do not take affect.
- Added the "SMSTSPostAction" task sequence variable and set it to reboot on TS completion to allow Group Policy to fully apply and any system changes (such as the IE11 install in Windows 7) to complete.

### 4.1.11
- Attempted adjusting the Password Scrambler command line to include the cscript.exe component.

### 4.1.10
- Added an extra reboot to Windows 7 to ensure the OS has settled and forced an activation of Office post restart.

### 4.1.9
- Resolved issues with RunOnce key and quotations.

### 4.1.8
- Attempted to add a RunOnce key to activate Office. Noticed that quotations were being removed when the key was added. Need to add / before each special.

## Major Version 4.0

This release was intended to create and merge a Windows 7 task sequence in to the build to allow Sydney to build following the failure of the Tivoli OSD component and an extremely complex recovery.

A windows 7 build was included, it bypasses the Office and region selected in the UI++ options prompt, applies Sydney time zones and Office 2013 x86 VLK. The option of Office 2016 was considered and rejected due to the impending Windows 10 migration and incompatibilities between their TRIM plugins and Office 2016.

This release also provided the capability to build from within Windows. When kicked off from within OS the UI++ dialogue would prompt after reboot preventing someone from rebuilding remotely. An extra UI++ step was included pre reboot into WinPE. The TS variable OptionsHaveRun is used to ensure it doesnt prompt a second time in WinPE.

Minor updates in this version included:
- Redesigned UI++ layout
- Self contained driver packages added
- Drivers added for the *"New Surface Pro"* (added as Surface Pro 2017 for easy identification) for 1703+ added
- Testing performed on an OSD Tattoo'ing and timing attempted but ultimately proved too time consuming.
- Added direct application of the WIM rather than download and apply to ensure faster build times
- Added domain join workaround for models affected by domain join bug. Issue is resolved in 1709 and will be deprecated at that time.
- Added options to choose AEST or AEDT timezones during build

**No minor version notes are available for 4.0*

