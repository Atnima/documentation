### MOSAIQ Notes

## Reg Fix

//*********************************************************************************************************************
//** INSTALLS Registry Fix for Mosaiq Practice Test Use.
//*********************************************************************************************************************



delete __createfile 
delete temp.reg

createfile until _end_reg
	Windows Registry Editor Version 5.00
	
	[HKEY_LOCAL_MACHINE\SOFTWARE\First DataBank\NDDF Framework 3.1i]
	"DBConnectString"="Provider=SQLOLEDB;User ID=fdbuser;password=FDBimpac;Initial Catalog=FDBDatabaseInt; Data Source=mosaiqdr01.stvincents.com.au;Connect Timeout=5"
	"DBUsername"=""
	"DBPassword"=""

_end_reg
copy __createfile temp.reg
//copy __createfile c:\localapps\temp.reg
waithidden regedit /s temp.reg



# Success Criteria

(NOT (exists keys "HKEY_LOCAL_MACHINE\SOFTWARE\First DataBank\NDDF Framework 3.1i" whose (exists values whose(name of it = "DBConnectString" AND it as string as lowercase = "Provider=SQLOLEDB;User ID=fdbuser;password=FDBimpac;Initial Catalog=FDBDatabaseInt; Data Source=mosaiqdr01.stvincents.com.au;Connect Timeout=5" as lowercase ) of it) of registry) )


## NDDF Addon

//*********************************************************************************************************************
// Install NDDF Framework
//*********************************************************************************************************************
delete __createfile
delete run.bat

// Use .bat to set working directory to packages root, for setup command.
createfile until _end_
	@ECHO OFF
	cd "{parameter "baseFolder"}"
	rem // See comments at the beginning of this action for an explanation of the comment markers.
	mkdir "{parameter "logFolder"}"
	echo %time% >> "{parameter "logFolder"}/{parameter "logFile"}"
	echo Action ID: {id of active action} >> "{parameter "logFolder"}/{parameter "logFile"}"
	echo Application: NDDF Framework 3.1i Install >> "{parameter "logFolder"}/{parameter "logFile"}"
	echo Command: "Setup.exe" >> "{parameter "logFolder"}/{parameter "logFile"}"
	"Setup.exe" >> "{parameter "logFolder"}/{parameter "logFile"}" 2>&1
	rem //**End Command Marker
	
	echo Return code: %errorlevel% >> "{parameter "logFolder"}/{parameter "logFile"}"
	echo. >> "{parameter "logFolder"}/{parameter "logFile"}"
_end_

move __createfile run.bat
if{name of operating system as lowercase starts with "win"}
	override wait
	hidden=true
	completion=job
	wait run.bat
else
	override wait
	completion=job
	wait run.bat
endif
//*********************************************************************************************************************