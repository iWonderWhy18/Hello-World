
## Types of variables

```powershell
Get-Process | Where-Object {$_.Responding -eq $false}
```
Processes with paths location
```powershell
Get-Process | Select-Object -Property ProcessName, Id, Path
```
```powershell
Get-CimInstance Win32_Process | Select-Object Name, ProcessId, CommandLine
```

```powershell
Get-Variable
```

```powershell
PS C:\Users\user1> $env:COMPUTERNAME
IML-EXAMPLE
```

```powershell
Get-Location – Get the current directory
Set-Location – Get the current directory
Move-item – Move a file to a new location
Copy-item – Copy a file to a new location
Rename – item Rename an existing file
New-item – Create a new file
```

Help Command
```powershell
PS C:\> Get-Command
```

Execution Policy
```powershell
PS C:\>   Set-ExecutionPolicy
```
Change to remote  signed
```powershell
PS C:\> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
```

Running a script
```powershell
PS C:\powershell\mynewscript.ps1
```

Common Commands
```powershell
`cd`: Change Directory. This command is used to change the current working directory. In PowerShell, `Set-Location` can be used as well.

`cls`: Clear Screen. This command clears the screen of the console. In PowerShell, `Clear-Host` or its alias `cls` can be used.

`dir`: Directory. This command lists the files and subdirectories in the directory. In PowerShell, `Get-ChildItem` can be used as well.

`echo`: This command prints text to the console. In PowerShell, `Write-Output` can be used as well.

`copy`: This command copies files. In PowerShell, `Copy-Item` can be used as well.

`del`: Delete. This command deletes one or more files. In PowerShell, `Remove-Item` can be used as well.

`move`: This command moves files from one location to another. In PowerShell, `Move-Item` can be used as well.

`type`: This command displays the contents of a text file. In PowerShell, `Get-Content` can be used as well.

`find`: This command searches for a text string in a file. In PowerShell, `Select-String` can be used as well.

`exit`: This command closes the command prompt or terminal window. It works the same in both Command Prompt and PowerShell.
```




Hostname AND Versions of Windows
```powershell
Get-ComputerInfo
```

```powershell
Get-ComputerInfo | select csname, windowsversion
```

![[Pasted image 20250812095438.png]]


List all user accounts on the machine
```powershell
Get-localuser
```
```powershell
Get-aduser
```
Check who is currently logged on
Check which users are in the administrator group


List all the currently running processes
```powershell
Get-Process
Get-Process -Name "Notepad"
Get-Process -Id 1234
Get-Process | Sort-Object CPU -Descending
```

Check process meta data including paths and arguments


Get version information for process
```powershell
Get-Process -Name pwsh -FileVersionInfo
```

EXTRA: get all services which are running and start automatically


Network traffic they're seeing is coming from the host you're looking at???

Retrieve information about current TCP connections on a system. This cmdlet is part of the `NetTCPIP` module.
```powershell
Get-NetTcpConnection
```

Netstat Help
```powershell
Netstat bnao
```

```powershell
netstat -bnao
```
```powershell
Netstat -a
```



# PowerShell Day 1 


### Persistence

Check registry startup locations
```powershell
Get-ItemProperty -Path HKCU:\Software\Microsoft\Windows\Currentversion\Run
```

HELP MENU FOR GET COMMANDS
```powershell
get -command
```

List Scheduled Tasks
```powershell
Get-ScheduledTask
```


Reg query FIND OUT THIS



Check a common registry startup location


HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce

List Scheduled tasks


Desktop file called "bad.txt"
Command to location the file "bad.txt"
```powershell
Get-ChildItem -Path C:\Users\fcu1\ -Recurse | Where-Object Name -eq "bad.txt"
```


List all the windows logs
```powershell
Get-WinEvent -listlog *
```

What logs might you check to see if PowerShell was run in the past hour?
```powershell
Get-WinEvent -listlog *powershell*
```

```powershell
 Get-WinEvent -log "Windows PowerShell"
```

```powershell
Get-WinEvent -logname "Microsoft-Windows-PowerShell/Operational"
```

Format
```powershell
Get-WinEvent -LogName Security -MaxEvents 50 | Format-Table TimeCreated, Id, Message -AutoSize
```

What command in PowerShell might you run to check that?


Adding Specifics to add to commands
This command is showing the most used items chewing up the CPU
```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 1 -Property ProcessName, ID, CPU
```

Find only established connections
```powershell
Get-NetTCPConnection | Where-Object { $_.State -eq "Established" } | Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, State
```

Find connections to a specific remote address
```powershell
Get-NetTCPConnection -RemoteAddress "192.168.1.50"
```

Find connections on a specific local port
```powershell
Get-NetTCPConnection -LocalPort 80
```

Show only Name, Enabled, and LastLogon
```powershell
Get-LocalUser | Select-Object Name, Enabled, LastLogon
```

Find all enabled local users
```powershell
Get-LocalUser | Where-Object { $_.Enabled -eq $true }
```

last write time 
```powershell
Get-ChildItem -Path "C:\YourDirectory" -File | Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)}
```

```powershell
Get-ChildItem -Path "C:\" -Recurse -ErrorAction SilentlyContinue -File | Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)}
```





# PowerShell Day 2


## Remoting 























































