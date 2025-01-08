I've put together a list of useful URL's and exclusions you may require for your Defender for Servers deployments;


# Defender for Servers activation on resource level

https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level

https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers-select-plan


# MDEAnalyzer

## Windows

https://aka.ms/MDEAnalyzer

Run MDEClientAnalyzer.cmd /? 
For a list of available parameters (available from https://aka.ms/MDEAnalyzerSwitches)

## Linux

https://aka.ms/XMDEClientAnalyzer


# Advanced deployment guidance for Microsoft Defender for Endpoint on Linux

https://github.com/MicrosoftDocs/defender-docs/blob/public/defender-endpoint/comprehensive-guidance-on-linux-deployment.md

# Configuring a Windows Network File Share to download Intelligence Files to

The following PowerShell script is required 

https://www.powershellgallery.com/packages/SignatureDownloadCustomTask/1.4


# Common Questions

https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-servers


# Windows Server 2012 R2 Exclusions

## Hyper-V

The following table lists the file type exclusions, folder exclusions, and process exclusions that are delivered 
automatically when you install the Hyper-V role.

| Exclusion Type  | Specifics |
| ------------- | ------------- |
| File Types | *.vhd, *.vhdx, *.avhd, *.avhdx, *.vsv, *.iso, *.rct, *.vmcx, *.vmrs  |
| Folders | %ProgramData%\Microsoft\Windows\Hyper-V |
|                | %ProgramFiles%\Hyper-V |
|                | %SystemDrive%\ProgramData\Microsoft\Windows\Hyper-V\Snapshots |
|                | %Public%\Documents\Hyper-V\Virtual Hard Disks |
| Processes  | %systemroot%\System32\Vmms.exe  |
|            | %systemroot%\System32\Vmwp.exe  |

## SYSVOL Files

%systemroot%\Sysvol\Domain\*.adm
%systemroot%\Sysvol\Domain\*.admx
%systemroot%\Sysvol\Domain\*.adml
%systemroot%\Sysvol\Domain\Registry.pol
%systemroot%\Sysvol\Domain\*.aas
%systemroot%\Sysvol\Domain\*.inf
%systemroot%\Sysvol\Domain\*Scripts.ini
%systemroot%\Sysvol\Domain\*.ins
%systemroot%\Sysvol\Domain\Oscfilter.ini

## AD - NTDS Database Files

The database files are specified in the registry key 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters\DSA Database File

%windir%\Ntds\ntds.dit
%windir%\Ntds\ntds.pat

## AD - The AD DS Transaction Log Files

The transaction log files are specified in the registry key 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters\Database Log Files Path

%windir%\Ntds\EDB*.log
%windir%\Ntds\Res*.log
%windir%\Ntds\Edb*.jrs
%windir%\Ntds\Ntds*.pat
%windir%\Ntds\TEMP.edb

## AD - The NTDS Working Folder

This folder is specified in the registry key 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters\DSA Working Directory

%windir%\Ntds\Temp.edb
%windir%\Ntds\Edb.chk

## AD - Process Exclusions for AD DS and AD DS-related support files

%systemroot%\System32\ntfrs.exe
%systemroot%\System32\lsass.exe

## AD - DHCP Server Exclusions

This section lists the exclusions that are delivered automatically when you install the DHCP Server role. 
The DHCP Server file locations are specified by the DatabasePath, DhcpLogFilePath, and BackupDatabasePath parameters in the registry key 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\DHCPServer\Parameters

%systemroot%\System32\DHCP\*\*.mdb
%systemroot%\System32\DHCP\*\*.pat
%systemroot%\System32\DHCP\*\*.log
%systemroot%\System32\DHCP\*\*.chk
%systemroot%\System32\DHCP\*\*.edb

## DNS - File and Folder Exclusions for DNS Server Role

%systemroot%\System32\Dns\*\*.log
%systemroot%\System32\Dns\*\*.dns
%systemroot%\System32\Dns\*\*.scc
%systemroot%\System32\Dns\*\BOOT


## DNS - Process exclusions for DNS Server role

%systemroot%\System32\dns.exe

## File and Storage Services exclusions

This section lists the file and folder exclusions that are delivered automatically when you install the File and Storage Services role. 
The exclusions listed below don't include exclusions for the Clustering role.

%SystemDrive%\ClusterStorage
%clusterserviceaccount%\Local Settings\Temp
%SystemDrive%\mscs

## Print Server exclusions

This section lists the file type exclusions, folder exclusions, and the process exclusions that are delivered automatically 
when you install the Print Server role.

*.shd
*.spl

### Folder exclusions
This folder is specified in the registry key

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Printers\DefaultSpoolDirectory

%system32%\spool\printers\*

### Process Exclusions

spoolsv.exe

## Web Server Exclusions

This section lists the folder exclusions and the process exclusions that are delivered automatically when you 
install the Web Server role.

### Folder Exclusions

%SystemRoot%\IIS Temporary Compressed Files
%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files
%SystemDrive%\inetpub\temp\ASP Compiled Templates
%systemDrive%\inetpub\logs
%systemDrive%\inetpub\wwwroot

### Process exclusions

%SystemRoot%\system32\inetsrv\w3wp.exe
%SystemRoot%\SysWOW64\inetsrv\w3wp.exe
%SystemDrive%\PHP5433\php-cgi.exe

## Turning off scanning of files in the Sysvol\Sysvol folder or the SYSVOL_DFSR\Sysvol folder

The current location of the Sysvol\Sysvol or SYSVOL_DFSR\Sysvol folder and all the subfolders is the file system reparse 
target of the replica set root. The Sysvol\Sysvol and SYSVOL_DFSR\Sysvol folders use the following locations by default:

%systemroot%\Sysvol\Domain
%systemroot%\Sysvol_DFSR\Domain

The path to the currently active SYSVOL is referenced by the NETLOGON share and can be determined by the SysVol value 
name in the following subkey: 

HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Netlogon\Parameters

Exclude the following files from this folder and all its subfolders:

*.adm
*.admx
*.adml
Registry.pol
Registry.tmp
*.aas
*.inf
Scripts.ini
*.ins
Oscfilter.ini

## Windows Server Update Services exclusions

This section lists the folder exclusions that are delivered automatically when you install the Windows Server Update 
Services (WSUS) role. The WSUS folder is specified in the registry key.

HKEY_LOCAL_MACHINE\Software\Microsoft\Update Services\Server\Setup

%systemroot%\WSUS\WSUSContent
%systemroot%\WSUS\UpdateServicesDBFiles
%systemroot%\SoftwareDistribution\Datastore
%systemroot%\SoftwareDistribution\Download

# Built-in Exclusions

Because Microsoft Defender Antivirus is built into Windows, it doesn't require exclusions for operating system files 
on any version of Windows.

## Windows “temp.edb” files

%windir%\SoftwareDistribution\Datastore\*\tmp.edb
%ProgramData%\Microsoft\Search\Data\Applications\Windows\windows.edb

## Windows Update files or Automatic Update files

%windir%\SoftwareDistribution\Datastore\*\Datastore.edb
%windir%\SoftwareDistribution\Datastore\*\edb.chk
%windir%\SoftwareDistribution\Datastore\*\edb\*.log
%windir%\SoftwareDistribution\Datastore\*\Edb\*.jrs
%windir%\SoftwareDistribution\Datastore\*\Res\*.log

## Windows Security Files

%windir%\Security\database\*.chk
%windir%\Security\database\*.edb
%windir%\Security\database\*.jrs
%windir%\Security\database\*.log
%windir%\Security\database\*.sdb

## Group Policy Files

%allusersprofile%\NTUser.pol
%SystemRoot%\System32\GroupPolicy\Machine\registry.pol
%SystemRoot%\System32\GroupPolicy\User\registry.pol

## File Replication Service (FRS) exclusions

Files in the File Replication Service (FRS) working folder. The FRS working folder is specified in the registry key

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NtFrs\Parameters\Working Directory

%windir%\Ntfrs\jet\sys\*\edb.chk
%windir%\Ntfrs\jet\*\Ntfrs.jdb
%windir%\Ntfrs\jet\log\*\*.log

### FRS Database log files. 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Ntfrs\Parameters\DB Log File Directory
%windir%\Ntfrs\*\Edb\*.log

### The FRS staging folder. 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NtFrs\Parameters\Replica Sets\GUID\Replica Set Stage
%systemroot%\Sysvol\*\Ntfrs_cmp*\

### The FRS preinstall folder.

Replica_root\DO_NOT_REMOVE_NtFrs_PreInstall_Directory
%systemroot%\SYSVOL\domain\DO_NOT_REMOVE_NtFrs_PreInstall_Directory\*\Ntfrs*\

### The Distributed File System Replication (DFSR) database and working folders. 

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\DFSR\Parameters\Replication Groups\GUID\Replica Set Configuration File

%systemdrive%\System Volume Information\DFSR\$db_normal$
%systemdrive%\System Volume Information\DFSR\FileIDTable_*
%systemdrive%\System Volume Information\DFSR\SimilarityTable_*
%systemdrive%\System Volume Information\DFSR\*.XML
%systemdrive%\System Volume Information\DFSR\$db_dirty$
%systemdrive%\System Volume Information\DFSR\$db_clean$
%systemdrive%\System Volume Information\DFSR\$db_lostl$
%systemdrive%\System Volume Information\DFSR\Dfsr.db
%systemdrive%\System Volume Information\DFSR\*.frx
%systemdrive%\System Volume Information\DFSR\*.log
%systemdrive%\System Volume Information\DFSR\Fsr*.jrs
%systemdrive%\System Volume Information\DFSR\Tmp.edb

## Process exclusions for built-in operating system files

%systemroot%\System32\dfsr.exe
%systemroot%\System32\dfsrs.exe

## Common Mistakes to Avoid

Microsoft recommend you avoid excluding the following folder locations, file extensions and processes as they could be 
exploited by malicious code or attacks.

### Folder Locations

%systemdrive%
C:, C:\, or C:\*
%ProgramFiles%\Java or C:\Program Files\Java
%ProgramFiles%\Contoso\, C:\Program Files\Contoso\, %ProgramFiles(x86)%\Contoso\, or C:\Program Files (x86)\Contoso\
C:\Temp, C:\Temp\, or C:\Temp\*
C:\Users\ or C:\Users\*
C:\Users\<UserProfileName>\AppData\Local\Temp\ or C:\Users\<UserProfileName>\AppData\LocalLow\Temp\.

Note the following important exceptions for SharePoint: Do exclude

C:\Users\ServiceAccount\AppData\Local\Temp
or
C:\Users\Default\AppData\Local\Temp

when you use file-level antivirus protection in SharePoint

%Windir%\Prefetch, C:\Windows\Prefetch, C:\Windows\Prefetch\, or C:\Windows\Prefetch\*
%Windir%\System32\Spool or C:\Windows\System32\Spool
C:\Windows\System32\CatRoot2
%Windir%\Temp, C:\Windows\Temp, C:\Windows\Temp\, or C:\Windows\Temp\*

### File Exclusions 

.7z
.bat
.bin
.cab
.cmd
.com
.cpl
.dll
.exe
.fla
.gif
.gz
.hta
.inf
.java
.jar
.job
.jpeg
.jpg
.js
.ko or .ko.gz
.msi
.ocx
.png
.ps1
.py
.rar
.reg
.scr
.sys
.tar
.tmp
.url
.vbe
.vbs
.wsf
.zip

### Processes

AcroRd32.exe
addinprocess.exe
addinprocess32.exe
addinutil.exe
bash.exe
bginfo.exe
bitsadmin.exe
cdb.exe
csi.exe
cmd.exe
cscript.exe
dbghost.exe
dbgsvc.exe
dnx.exe
dotnet.exe
excel.exe
fsi.exe
fsiAnyCpu.exe
iexplore.exe
java.exe
kd.exe
lxssmanager.dll
msbuild.exe
mshta.exe
ntkd.exe
ntsd.exe
outlook.exe
psexec.exe
powerpnt.exe
powershell.exe
rcsi.exe
svchost.exe
schtasks.exe
system.management.automation.dll
windbg.exe
winword.exe
wmic.exe
wscript.exe
wuauclt.exe

### Linux

bash
java
python and python3
sh
zsh
