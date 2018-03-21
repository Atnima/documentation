# Major Update - 4.4.0

**New Feature:** Driver application using Deployment Image Servicing and Management <br>
>There have been a number of failures reported due to the way drivers are applied during the image. These failures are sporadic and extremely inconsistent. To alleviate the issue, driver application steps have been completely reworked to utilise DISM prior to the first boot into Windows instead of using an EXE package or the unattend xml to apply drivers.<br><br>Given the significant change this introduces, as well as newer driver versions, please report any suspected issues as soon as possible. SVMHS Windows 7 Builds will continue to use the existing process until a future release.

**New Driver Pack:** Hewlett-Packard ProDesk 600 G3 <br>
>The HP ProBook 600 G3 can now be built to Windows 10.

**Feature Changes:** <br>
>- Due to space constraints, USMT data will now only be stored for seven (7) days following a successful migration. Please ensure you confirm data is restored within this period.

**Fixes**
>- USMT will now use a Network Access Account if it fails to connect to a State Migration Point.
>- Fixed an issue where USMT would fail when non-standard local accounts were present. USMT will now recreate any local accounts and restore data to those accounts. The account will be disabled and will need to be re-enabled and have its password reset prior to use.
>- Fixed an issue where deployment source would be pulled from the Melbourne distribution point regardless of device location.
>- Fixed an issue where AD Group Migration would run twice under certain scenarios.
>- Corrected a permissions issue in the Build UI feature.
>- Corrected a permissions issue in the AD Group Migration feature.
>- Corrected a permissions issue an the Error Logging scenario.
>- Cleaned up task sequence steps and removed deprecated features.

### **Drivers**

>The new driver application feature requires repackaging all drivers. Please see driver package details below. Any other models will continue to use existing methods and will be migrated at a later date.
<center>

>Manufacturer | Model | Generation | Driver Pack | Driver Date 
> :--- | :--- | :---: | :---: | :---: |
>Hewlett-Packard | EliteDesk 800 | G1 | sp69541<sup>^ | 2014-10-19
> |  |  | G2 | sp81982 | 2017-10-16
> |  |  | G3 | sp85276 | 2018-02-20
> |  | ProDesk 800 | G3 | sp85276 | 2018-02-20
> |  | Elite X2 1012 | G1 | sp83806 | 2017-11-18
> |  | EliteBook x360 1030 | G2 | sp84730 | 2018-01-16
> |  | EliteBook 840 | G3 | sp84739 | 2018-01-16
> |  |  | G4 | sp84737 | 2018-01-16
> |  | ProBook 640 | G3 | sp84732 | 2018-01-16
> |  | EliteOne 800 | G1 | sp69541<sup>^ | 2014-10-19
> |  |  | G2 | sp85475 | 2018-02-20
> |  |  | G3 | sp85276 | 2018-02-20
> |  | EliteBook Revolve 810 | G3 | sp79221 | 2017-02-24
> Lenovo | ThinkCentre M700 | - | tc_m700 | 2016-12-21
> |  | ThinkCentre M800 | - | tc_m800 | 2016-12-21
> |  | ThinkCentre M900 | - | tc_m900 | 2016-12-21
>^ Drivers are not available for Windows 10. Windows 8 / 8.1 drivers have been used.
</center>


# Minor Update - 4.3.1
Minor updates and fixes

**Updates** 
- To assist in reducing unnecessary file migration USMT Restore will now only migrate user profiles that have been active within 90 days. (Suggested by Brendan - Thank you)
- Cisco AnyConnect Secure Mobility Client updated to 4.5.04029.
- Added step to print task sequence version in the log file to assist troubleshooting.

# Major Update - 4.3.0

**New Feature:** SVPHM Application Set <br>
To provide a single experience across SVHA, SVPHM specific apps that were previously deployed using an alternate sequence have been incorporated into the national build sequence.

In order to build with the SVPHM application included, select Melbourne as the intended time zone on the first page, this will trigger a second page asking whether just the standard National app set is required or if the SVPHM apps should be included.

**New Feature:** USMT Restore [BETA] <br>
You can now back-up and restore user profiles during the build. This will allow user data from a device to be automatically migrated without the need for manual intervention. <br>
*IMPORTANT: Please see attached documentation prior to use.*

**Updated Feature:** AD Group Migration [BETA] <br>
The AD Group Migration feature previously triggered a powershell script that required user input for the existing asset number. This has now been incorporated into the UI for consistency.

**Fixes**
* Vastly improved PXE boot speed across a number of sites (~88% improvement).
* The Build UI will now show immediately upon starting the task sequence rather than after hard drive formatting.
* Fixes for "in-OS" builds (starting the build within Windows).
* Changes aimed at improving build experience for 800 G2 devices.
* Added the ability to use the following (in addition to the existing) naming conventions to assist rebuilds of existing devices: <br>
    * A#####
    * CPQ##-S###
    * LT-####
    * SV_SP##
    * SV-SP##

*Note: Please use the new naming convention where possible (fill in the 6 digit asset tracking number and tick the "automatic name" box).*

#### Known Issues
**SVPHM - OU Changes**
<br>Impact - *Consistent // Low*
<br>There was a step in the existing SVPHM task sequence that moved it into the SVPHM OU within the SVHA domain. I'm unsure if this was functioning correctly in the existing task sequence but it has been confirmed as not working in the new sequence. I will be recreating this functionality in the future however it was not ready for this release and new objects will need to be moved manually. Apologies for the inconvenience.

# Minor Update - 4.2.1
Minor update including fixes for the 800 G2 and incomplete build notification.

**Fixes** 
- Fixed an issue where 800 G2 devices were not initialising fast enough on first boot to Windows causing the build to fail
- Fixed an issue where the Incomplete Build Notification wasn't showing after the WinPE volume is removed

*Please Note - The 800G2 issue appears to be isolated to this particular model and in this instance was caused by a significant delay in components initialising after the first boot to Windows. While I believe this fix should resolve the issue, please report any issues you have with builds as soon as possible.*


# Major Update - 4.2.x (.0)

This is a major update focussed on a release of the Windows 10 Fall Creators Update, fixes for some issues occuring sporadically during builds, an incomplete build notification screen and a redesign of the automated log upload system.

**New Feature:** Windows 10 - The Fall Creators Update <br>
Windows 10 version 1709 will now be the default for all future Windows 10 MOE builds.

**New Feature:** Incomplete Build Notification <br>
To improve visibility when a build fails, a custom script will now display on screen until dismissed, preventing the task sequence from rebooting into Windows making it hard to see at a glance whether it completed.

**New Feature:** Automatic Name Generation <br>
There is now an option to automatically generate the asset name using the newly agreed standard. If using this option please ensure you only enter the 6 digit IT Tracking Number in the name field and tick the option. This will then generate the name automatically (D###### and N###### for Desktops and Laptops respectively).

**New Feature:** AD Group Migration [BETA]<br>
A new option to migrate AD groups from the old computer object to the new one has been added. Please note this feature is in testing and while working in isolated lab builds, AD Groups will need to be confirmed as successfully transferred when using on any production devices. Please touch base if you would like any more information.

**Redsigned:** Automated Log Upload
The automated log upload (released in 4.1.17) has be re-written and improved upon by incorporating it into the incomplete build notification. It will now timestamp the log upload and append the asset ID obtained during the Build UI screen.

**Fixes**
- Fixed an issue where EliteDesk 800 G2 devices would not build on 1607
- Fixed an issue where certain devices, when building Windows 10, would fail citing an RPC error
- Improved EXE driver application to reduce unexpected failures
- Optimised power management changes during build


# Minor Update - 4.1.x (.17)

This is a minor update focussed on correcting issues identified in the SVMHS build and improving the ability for remote troubleshooting.

**New Feature:** Automated log upload <br>
To assist in root cause analysis of any future issues, the task sequence will now automatically upload certain logs in the event the task sequence fails.

**Fixes**
- Fixed an issue where SVMHS builds would fail applying critical network drivers.
- Fixed an issue where device specific drivers would fail in the SVMHS build citing an RPC unavailable error.

# Release Notes - 4.1.x (.14 - RC1)

4.1 is focussed on improvements to the Tivoli build replacement for SVMHS. There were a number of issues identified early that have been resolved in this release.
- Office 2013 not licencing on SVMHS builds has been resolved
- Region settings have been corrected in SVMHS builds
- Language settings have been corrected in SVMHS builds
- Local admin password was randomised in an SVMHS build and was not retrievable
- Surface Pro 2017 (aka New Surface Pro) now has available drivers <br> *note this requires the device be built to Windows 10 1709, until 1709 enters full production this can be found in the development section. New Surface Pro's (the 2017 one with rounded edges) should not be built to the standard image as they will not function as expected.
- Updated drivers and firmware for Surface Pro 4
- High performance power management has been set in build to speed up deployment
- Monitor timeout is now set to prevent the monitor going to sleep in longer builds
- Minor corrections to functionality within the in-build UI

#### Known Issues
**Surface Pro devices have no network connectivity post build.**
<br>Impact - *Infrequent // Low*
<br>Due to a significant change in driver and firware level with a new build, both for the Surface Pro and the connected dock, I have seen 2 instances in testing where the Surface Pro had no ethernet or WiFi connection despite being connected to a dock. This is due to the firmware upgrades included in the build. The upgrades apply over a number of reboots and a final reboot (or two) will resolve.

**Password scrambler not functioning on SVMHS build**
<br>Impact - *Consistent // Low*
<br>With the replacement Tivoli build the intent was to use the password scrambler to improve security on any new builds, unfortunately I have been unable to get this to work. Until it can be looked at, SVMHS builds will continue to use the existing local administrator password.



### Office not activating
It was quickly identified that Office was not activating for users and, on first use, was warning the user they were unlicenced. This has been tracked to a function of Office licencing whereby Office unlicences itself in the case of major hardware change (to prevent a licenced copy from being moved to a different PC).

Because Office was installing on what is essentially the first ever boot of Windows, it was registering hardware changes on the second boot causing the issue. This is a limitation in Windows 7.

This has been resolved by adding a second reboot in for Windows 7 builds and forcing a licence rearm after that.
































