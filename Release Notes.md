# Bug Fix Release - 5.1.5

**Fixes:**

> - Updated I219-LM drivers (12.17.8.7 - 29/09/2017) for ProDesk 600 G3 devices to resolve an issue with network disconnections.
> <br><sup> Credit: Brenden Vanderstam

<br>

--------------------------------

# Driver Release - 5.1.4

**Updated Boot Image**
> A boot image update will go live tonight to accomodate PXE booting the z440 Workstations which were made available in 5.1.2.
>
> This update will mean a new version of the boot image is required. Please source the latest boot image from the following location tomorrow morning and update any USB's you have.
>
> \\\sccm-pr9-01\temp$\
> Image name: SVHA-Builds_5.1.4.iso

**New Windows 10 Drivers**
>
> The following devices can now be built to Windows 10.
>
>Manufacturer | Model | Generation | Driver Pack | Driver Date 
> :--- | :--- | :---: | :---: | :---: |
>Microsoft | Surface Book 2 | - | surfacebook_win10_16299 | 2018-01-01

**New Windows 7 Drivers**
>
> The following devices can now be built to Windows 7
>Manufacturer | Model | Generation | Driver Pack | Driver Date 
> :--- | :--- | :---: | :---: | :---: |
>Hewlett-Packard | ProOne 600 | G3 | sp85281 | 2018-02-02
<br>

--------------------------------

# Bug Fix Release - 5.1.3

**Fixes:**

> - Restored functionality lost in a previous release (4.3.0) where St Vincent's Private Hospital Melbourne devices would be moved to an alternate OU. <br> 
> <sup> Credit: Aalap Gandhi - Thank you for reminding me
> - Improved BitLocker activation steps during build to only apply to required devices.

<br>

--------------------------------

# Driver Release - 5.1.2

> The following devices can now be built to Windows 10.
>
>Manufacturer | Model | Generation | Driver Pack | Driver Date 
> :--- | :--- | :---: | :---: | :---: |
>Hewlett-Packard | z440 Workstation | - | sp84798 | 2018-02-21

<br>

--------------------------------

# Bug Fix Release - 5.1.1

**Fixes:**

> - Fixed an issue preventing Surface Pro driver MSI's from installing <br> 
> <sup> Credit: Aalap Gandhi - Thank you for catching this

<br>

--------------------------------

# Minor Update - 5.1.0

**New Feature:** Data#3 UI Skip

> To assist Data#3 with the large volume of rebuilds required at their site, the UI will be skipped for any builds kicked off on their subnet. 
>
> For SVHA stes, this currently presents as a powershell window that should exit after a brief period and will continue on to display the UI.
>
> For Data#3 the script will set the options usually collected during the UI and check the BIOS has been set to a standard asset tag format.

**New Feature:** App Install Script

> To assist with apps that fail to install cleanly using an unattended installation within SCCM, a script has been written to install these apps while allowing error information to show for technicians. This will intially be used to assist with the sporadic Java failures.
>
> This is currently only live for Windows 10 as time constraints have prevented testing on Windows 7. This will be added to Windows 7 in a future update.

**New Driver Packs**

> The following devices can now be built to Windows 10.
>
>Manufacturer | Model | Generation | Driver Pack | Driver Date 
> :--- | :--- | :---: | :---: | :---: |
>Microsoft | Surface Book | - | surfacebook_win10_16299 | 2018-01-01
>Hewlett-Packard | ProBook 650 | G2 | sp84740 | 2018-01-16
> | | z240 Workstation | - | sp84799 | 2018-02-21
>Lenovo | ThinkPad T460S | - | tp_t460s | 2017-11-13

**April Patches**

> April 2018 patches have been applied to both the Windows 10 and 7 images.


**Fixes:**

> - Further changes to fix an issue with USMT where it would fail to connect to a state store.
> - Fixed missing Bluetooth and LTE drivers in EliteBook x360 1030 driver pack.
> - Further changes to mitigate an issue where Java fails to install during the task sequence.
> - Temporarily resolved known issue in 5.0.0 caused by the failure of the GSSO File/Print server.
> - Resolved missing regex check for device name (CPQ##-M###).
> - Removed PXE password for Data#3 site to assist device builds.

<br>

--------------------------------


# Major Update - 5.0.0

**New Infrastructure:** Melbourne Distribution Point<sup>^

>To assist with the deployment of USMT a new Distribution Point has been commissioned in Melbourne. If there are any issues with OS or application deployment please get in touch.

**New Feature:** Driver application using Deployment Image Servicing and Management (DISM)<br>
>There have been a number of failures reported due to the way drivers are applied during the image. These failures are sporadic and extremely inconsistent. To alleviate the issue, driver application steps have been completely reworked to utilise DISM prior to the first boot into Windows instead of using an EXE package or the unattend xml (inbuilt functionality) to apply drivers.<br><br>Given the significant change this introduces, as well as newer driver versions, please report any suspected issues as soon as possible.

**New Driver Pack:** Hewlett-Packard ProDesk 600 G3 <br>
>The HP ProBook 600 G3 can now be built to Windows 10.

**Changes:** <br>
>- **IMPORTANT:** Due to space constraints, USMT data will now only be stored for seven (7) days following a successful migration. Please ensure you confirm data has been restored successfully within this period. <sup> ^
>- **IMPORTANT:** Windows 7 Builds for SVMHS are now achieved as a later prompt when selecting NSW as the location. Development options are now only required for non-standard names.
>- Windows 10 1607 has now been deprecated and is no longer available under the 'Development Options' screen.
>- Updated SCCM Service start behaviour to significantly improve performance.
>- Cleaned up task sequence steps and removed deprecated features.
>- Removed deprecated "Domain Join Workaround" behaviour related to Windows 10 1607 installs.
>- Updated SVHB Boundary to include newly created DHCP range.<sup>^ (Credit: Brendan Vanderstam)
>- Optimised up a number of WMI queries within the OSD to improve performance.
>- Improved build speed by removing restarts no longer needed with the addition of the new driver application model.
>- Modified offline registry files to prevent a device from trying to connect to Windows Update during OOBE.
>- UI steps are now universal between OS initiated and PXE/USB initiated builds.
>- Significant modifications to the UI configuration XML to remove deprecated features and improve readability.
>- Added the ability to choose between the MaterSyd and SVMHS domains for Windows 7.<sup># 
>- Active Directory Group Migration has left BETA! <br>
>- USMT will now use a Network Access Account if it fails to connect to a State Migration Point.

**Fixes:**
>- Fixed an issue where USMT would fail when non-standard local accounts were present. 
>   - USMT will now recreate any local accounts in a disabled state and restore data to those accounts. The account will need to be re-enabled and have its password reset prior to use.
>- Fixed an issue where deployment files would be sourced from the Melbourne distribution point regardless of device location. <sup>^
>- Fixed an issue where AD Group Migration would run twice under certain scenarios.
>- Corrected a permissions issue in the Build UI feature.
>- Corrected a permissions issue in the AD Group Migration feature.
>- Corrected a permissions issue during an Error Logging scenario.
>- Fixed an issue where some devices would fail when applying certain application packages during OSD citing an 'unspecified error'.
>- Fixed an issue where some devices were not loading drivers correctly.
>- Fixed an issue where significant delays in loading drivers caused components and peripherals to be unresponsive.
>- Fixed missing Bluetooth driver on 800 G3 AiO devices.
>- Corrected outdated UI elements and branding.

 <sup>^ Change or fix went live just prior to this update. </sup><br>
 <sup># The computer object will be placed in the Workstations root and will need to be moved to specific location based OU's post build.


### **Drivers**

>The new driver application feature required a repackaging of all drivers. Please see migrated driver package details below including the date of release by the vendor. Due to the complexity of the change some drivers have not been migrated and are listed later in the notes.

><center> <b>
>Windows 10
></center> </b>
>
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
> |  | Compaq Elite 8300 | - | sp60420 | 2013-01-10
> Lenovo | ThinkCentre M700 | - | tc_m700 | 2016-12-21
> |  | ThinkCentre M800 | - | tc_m800 | 2016-12-21
> |  | ThinkCentre M900 | - | tc_m900 | 2016-12-21
>^ <sup>Drivers are not available for Windows 10. Windows 8 / 8.1 drivers have been used. <br>

><center> <b>
>Windows 7
></center> </b>
>
>Manufacturer | Model | Generation | Driver Pack | Driver Date 
> :--- | :--- | :---: | :---: | :---: |
>Hewlett-Packard | EliteDesk 800 | G1 | sp69540 | 2014-10-29
> |  |  | G2 | sp85469 | 2018-02-14
> |  |  | G3 | sp85281 | 2018-02-02
> |  | Compaq Elite 8300 | - | sp61385 | 2013-04-03
> |  | ProBook 650 | G1 | sp66432 | 2014-05-20
> |  |  | G2 | sp82348 | 2017-10-18
> |  | EliteBook 820 | G1 | sp66432 | 2014-05-20
> |  |  | G2 | sp70143 | 2014-12-17
> |  |  | G3 | sp82346 | 2017-12-05
> |  | EliteBook 840 | G2 | sp70143 | 2014-12-17
> |  |  | G3 | sp82346 | 2017-12-05
> |  | EliteBook 850 | G2 | sp70143 | 2014-12-17
> |  |  | G3 | sp82346 | 2017-12-05
> |  | z240 Workstation | - | sp82547 | 2017-11-14

>The following drivers **have not** been migrated. If you need to rebuild any of these devices please get in touch prior. I will work on having these included in a future release.
>- Lenovo ThinkPad T460s
>- Lenovo ThinkPad X1
>- Lenovo ThinkPad Yoga 370
>- Lenovo ThinkStation P300

**Known Issues** <br>
>**GSSO Distribution Point Failures**
><br>Impact - *Consistent // Medium*
><br>Due to an outage with the GSSO File/Print server during development and test, the OSD task sequence currently will not run from any site running off the NSW Group Office distribution point (William Street) until the driver packages can be distributed to it. This will be done as soon as is practical.

--------------------------------


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
































