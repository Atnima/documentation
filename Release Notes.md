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
































