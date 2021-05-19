# ThisWillCrash
This is a simple MFC project that is designed to demonstrate creation of postmortem (.dmp) crash dumps

This feature is not enabled by default. Enabling the feature requires administrator privileges. To enable and configure the feature, 
use the following registry values under the 

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps key.

Value	Description	Type	Default value
DumpFolder	The path where the dump files are to be stored. If you do not use the default path, then make sure that the folder contains ACLs that allow the crashing process to write data to the folder. For service crashes, the dump is written to service specific profile folders depending on the service account used. For example, the profile folder for System services is %WINDIR%\System32\Config\SystemProfile. For Network and Local Services, the folder is %WINDIR%\ServiceProfiles.
REG_EXPAND_SZ	%LOCALAPPDATA%\CrashDumps
DumpCount	The maximum number of dump files in the folder. When the maximum value is exceeded, the oldest dump file in the folder will be replaced with the new dump file.	REG_DWORD	10
DumpType	Specify one of the following dump types:
0: Custom dump
1: Mini dump
2: Full dump
REG_DWORD	1
CustomDumpFlags	The custom dump options to be used. This value is used only when DumpType is set to 0.
The options are a bitwise combination of the MINIDUMP_TYPE enumeration values.
REG_DWORD	MiniDumpWithDataSegs | MiniDumpWithUnloadedModules | MiniDumpWithProcessThreadData.


These registry values represent the global settings. You can also provide per-application settings that override the global settings. 

To create a per-application setting, create a new key for your application under 

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows Error Reporting\LocalDumps 

(for example, HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows Error Reporting\LocalDumps\MyApplication.exe). 

Add your dump settings under the MyApplication.exe key. 
If your application crashes, WER will first read the global settings, and then will override any of the settings with your application-specific settings.


https://docs.microsoft.com/en-us/windows/win32/wer/collecting-user-mode-dumps

Explains more  
