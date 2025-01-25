## PowerGrid 🔌

### PowerGrid is a collection of Microsoft PowerShell modules that can be used to aid penetration testers during all phases of an assessment. PowerGrid is comprised of the following modules and scripts:

## CodeExecution

**Execute code on a target machine.**

#### `Invoke-DllInjection`

Injects a Dll into the process ID of your choosing.

#### `Invoke-ReflectivePEInjection`

Reflectively loads a Windows PE file (DLL/EXE) in to the powershell process, or reflectively injects a DLL in to a remote process.

#### `Invoke-Shellcode`

Injects shellcode into the process ID of your choosing or within PowerShell locally.

#### `Invoke-WmiCommand`

Executes a PowerShell ScriptBlock on a target computer and returns its formatted output using WMI as a C2 channel.

## ScriptModification

**Modify and/or prepare scripts for execution on a compromised machine.**

#### `Out-EncodedCommand`

Compresses, Base-64 encodes, and generates command-line output for a PowerShell payload script.

#### `Out-CompressedDll`

Compresses, Base-64 encodes, and outputs generated code to load a managed dll in memory.

#### `Out-EncryptedScript`

Encrypts text files/scripts.

#### `Remove-Comment`

Strips comments and extra whitespace from a script.

## Persistence

**Add persistence capabilities to a PowerShell script**

#### `New-UserPersistenceOption`

Configure user-level persistence options for the Add-Persistence function.

#### `New-ElevatedPersistenceOption`

Configure elevated persistence options for the Add-Persistence function.

#### `Add-Persistence`

Add persistence capabilities to a script.

#### `Install-SSP`

Installs a security support provider (SSP) dll.

#### `Get-SecurityPackages`

Enumerates all loaded security packages (SSPs).

## AntivirusBypass

**AV doesn't stand a chance against PowerShell!**

#### `Find-AVSignature`

Locates single Byte AV signatures utilizing the same method as DSplit from "class101".

## Exfiltration

**All your data belong to me!**

#### `Invoke-TokenManipulation`

Lists available logon tokens. Creates processes with other users logon tokens, and impersonates logon tokens in the current thread.

#### `Invoke-CredentialInjection`

Create logons with clear-text credentials without triggering a suspicious Event ID 4648 (Explicit Credential Logon).

#### `Invoke-NinjaCopy`

Copies a file from an NTFS partitioned volume by reading the raw volume and parsing the NTFS structures.

#### `Invoke-Mimikatz`

Reflectively loads Mimikatz 2.0 in memory using PowerShell. Can be used to dump credentials without writing anything to disk. Can be used for any functionality provided with Mimikatz.

#### `Get-Keystrokes`

Logs keys pressed, time and the active window.

#### `Get-GPPPassword`

Retrieves the plaintext password and other information for accounts pushed through Group Policy Preferences.

#### `Get-GPPAutologon`

Retrieves autologon username and password from registry.xml if pushed through Group Policy Preferences.

#### `Get-TimedScreenshot`

A function that takes screenshots at a regular interval and saves them to a folder.

#### `New-VolumeShadowCopy`

Creates a new volume shadow copy.

#### `Get-VolumeShadowCopy`

Lists the device paths of all local volume shadow copies.

#### `Mount-VolumeShadowCopy`

Mounts a volume shadow copy.

#### `Remove-VolumeShadowCopy`

Deletes a volume shadow copy.

#### `Get-VaultCredential`

Displays Windows vault credential objects including cleartext web credentials.

#### `Out-Minidump`

Generates a full-memory minidump of a process.

#### `Get-MicrophoneAudio`

Records audio from system microphone and saves to disk

## Mayhem

**Cause general mayhem with PowerShell.**

#### `Set-MasterBootRecord`

Proof of concept code that overwrites the master boot record with the
message of your choice.

#### `Set-CriticalProcess`

Causes your machine to blue screen upon exiting PowerShell.

## Privesc

**Tools to help with escalating privileges on a target.**

#### `PowerUp`

Clearing house of common privilege escalation checks, along with some weaponization vectors.

## Recon

**Tools to aid in the reconnaissance phase of a penetration test.**

#### `Invoke-Portscan`

Does a simple port scan using regular sockets, based (pretty) loosely on nmap.

#### `Get-HttpStatus`

Returns the HTTP Status Codes and full URL for specified paths when provided with a dictionary file.

#### `Invoke-ReverseDnsLookup`

Scans an IP address range for DNS PTR records.

#### `PowerView`

PowerView is series of functions that performs network and Windows domain enumeration and exploitation.

## Recon\Dictionaries

**A collection of dictionaries used to aid in the reconnaissance phase of a penetration test. Dictionaries were taken from the following sources.**

- admin.txt - <http://cirt.net/nikto2/>
- generic.txt - <http://sourceforge.net/projects/yokoso/files/yokoso-0.1/>
- sharepoint.txt - <http://www.stachliu.com/resources/tools/sharepoint-hacking-diggity-project/>

## License

The PowerGrid project and all individual scripts are under the [BSD 3-Clause license](https://raw.github.com/mattifestation/PowerGrid/master/LICENSE) unless explicitly noted otherwise.

## Usage

Refer to the comment-based help in each individual script for detailed usage information.

To install this module, drop the entire PowerGrid folder into one of your module directories. The default PowerShell module paths are listed in the $Env:PSModulePath environment variable.

The default per-user module path is: "$Env:HomeDrive$Env:HOMEPATH\Documents\WindowsPowerShell\Modules"
The default computer-level module path is: "$Env:windir\System32\WindowsPowerShell\v1.0\Modules"

To use the module, type `Import-Module PowerGrid`

To see the commands imported, type `Get-Command -Module PowerGrid`

If you're running PowerShell v3 and you want to remove the annoying 'Do you really want to run scripts downloaded from the Internet' warning, once you've placed PowerGrid into your module path, run the following one-liner:
`$Env:PSModulePath.Split(';') |
 % { if ( Test-Path (Join-Path $_ PowerGrid) )
 {Get-ChildItem $_ -Recurse | Unblock-File} }`

For help on each individual command, Get-Help is your friend.

Note: The tools contained within this module were all designed such that they can be run individually. Including them in a module simply lends itself to increased portability.
