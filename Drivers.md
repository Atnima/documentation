# SVHA Drivers

## 1.0 Driver Packaging

Driver packaging is accomplished using a custom powershell script designed to package up a folder of drivers into a single EXE file to be applied during an OSD.

This approach is used for a few key reasons. Primarily, while there is an inbuilt drivers and driver package function within SCCM, it lacks the ability to update drivers easily and in a silo'd fashion. If SCCM detects an updated driver applies to another model, it will update it there, making testing difficult.

### Pre-requisites
In order to package drivers in the above method, the following is required:  
* Inno Setup
* New-EXEDriverPackage Module

### Instructions



## 2.0 Packaged Drivers
Windows | Manufacturer | Model | Generation | Driver Pack | Driver Date 
:---: | :---: | :---: | :---: | :---: | :---: |
Windows 10 | 
| | Hewlett-Packard | EliteDesk 800 | G1 | *sp69541** | 2017-10-29
|  |  |  | G2 | sp79203 | 2017-02-14
|  |  |  | G3 | sp80492 | 2017-05-23
| | | EliteBook 840 | G3 | sp80892 | 2017-06-23
| | | EliteBook 650 | G3 | sp80490 | 2017-05-23
Windows 7 |
| | Hewlett-Packard | 8300 Elite SFF | - | sp61385 | 2013-04-03
| | Hewlett-Packard | EliteDesk 800 | G1 | sp69540 | 2014-10-19
|  |  |  | G2 | sp80307 | 2017-05-31
|  |  |  | G3 | sp80510 | 2017-06-15
| | | ProBook 650 | G1 | **sp66432** | 2014-05-20
|  |  |  | G2 | sp80901 | 2017-06-23
| | | EliteBook 820 | G1 | sp66432^ | 2014-05-20
|  |  |  | G2 | **sp70143** | 2014-12-17
|  |  |  | G3 | **sp80893** | 2017-06-23
| | | EliteBook 840 | G1 | sp66432^ | 2014-05-20
|  |  |  | G2 | sp70143^ | 2014-12-17
|  |  |  | G3 | sp80893^ | 2017-06-23
| | | EliteBook 850 | G2 | sp70143^ | 2014-12-17
| | | z240 Workstation | - | sp82547 | 2017-11-14

*Italics indicate the drivers are for an earlier version of windows.*  
**Bold indicates the driver pack is used for other models**  
^ Indcates the model uses an above driver pack (in bold per above)
