
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


```powershell
Enter-PSSession -ComputerName REMOTEPC (Get-Credential)

Invoke-Command -ComputerName REMOTEPC {Get-Process}

Get-WMIObject -Class Win32_Process -ComputerName REMOTEPC

Enable-PSRemote -Force
```

[Get-WmiObject (Microsoft.PowerShell.Management) - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1)


## Scripting 

Scripting Concepts
- Variables: $name="john"
- Arrays: $items = @("apple", "pear", "banana")
- Loops: foreach, for, while
- Conditionals: if, else, elseif
- Functions: Invoke-Pingsweep {xyz}

#### Step 1: Variables

```powershell
$subnet = "192.168.1." #Variable 
$range = 1..10 #Array
```

#### Step 2: Variables and Loops (Foreach)

```powershell
Foreach ($host in $range) {       #$host is being defined here
	$ip = "$subnet$host"
	Write-Output "Pinging $ip..."
}
```


#### Step 3: Conditionals (if/ else)

```powershell
if (Test-Connection -ComputerName $ip -count 1 -Quiet) {
	Write-Output "$ip is online"
} else {
	write-output "$ip is unreachable"
	}
```


#### Step 4: Output it to a file

```powershell
$results = "C:\temp\pingsweep_results.txt"
foreach ($host in $range){
	$ip = "$subnet$host"
	$status = if (test-connection -ComputerName $ip -count 1 -quiet){
		"$ip is online"
	}else{
	"$ip is unreachable"
	}
	Add-Content -Path $results -Value $status
}
```


#### Step 5: Turn it into a function


```powershell
Function Invoke-Pingsweep{
	param(
		[string]$subnet = "192.168.1.",
		[int]$start = 1,
		[int]$end = 10,
		[string]$OutputPath = "C:\Temp\pingsweep_result.txt"
	)

	$range = $Start..$End         #1,2,3,4,5,6,7,8,9,10
	Foreach ($host in $range){    #will iterate through range
		$ip = "$subnet$host"      #192.168.1.$host
		$status = if (test-connection -ComputerName $ip -count 1 -Quiet){
			"$ip is online"       #nice for troubleshooting
		}else{
			"$ip is unreachable"
		}
		Add-Content -Path $OutputPath -Value $status #adding it to the file
	}
	Write-Output "Pingsweep done, results saved to $outputPath"
}
```

Part 2 - Main script
```powershell
$range = $Start..$End         #1,2,3,4,5,6,7,8,9,10
Foreach ($host in $range){    #will iterate through range
	$ip = "$subnet$host"      #192.168.1.$host
	$status = if (test-connection -ComputerName $ip -count 1 -Quiet){
		"$ip is online"       #nice for troubleshooting
	}else{
		Add-Content -Path $OutputPath -Value $status #adding it to the file
	}
	Write-Output "Pingsweep done, results saved to $outputPath"
}
```






Script Idea's

Get-Process

output a file for any process that has a higher pid then 4
or
for each process display it in .txt file
or 
check which files/programs are in the run and runonce registry keys

Scripting Concepts
- Variables: $name="john"
- Arrays: $items = @("apple", "pear", "banana")
- Loops: foreach, for, while
- Conditionals: if, else, elseif


## Python script for getting items out of run and runonce keys and displays in .txt file

```powershell
$location = $location1, $location2, $location3, $location4, $location5, $location6, $location7, $location8

$location1 = "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
$location2 = "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce"
$location3 = "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
$location4 = "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce"
$location5 = "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run"
$location6 = "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce"
$location7 = "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run"
$location8 = "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce"


Foreach ($file in $location) {       
	$document = "$location$file"
	Write-Output "checking $document..."
}

```

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce

```powershell
# Define registry locations to check
$locations = @(
    "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run",
    "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce",
    "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run",
    "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce"
)

# Get the path to the current user's desktop
$desktopPath = [Environment]::GetFolderPath("Desktop")
$outputFile = Join-Path $desktopPath "RunRegistryEntries.txt"

# Create or clear the output file
Set-Content -Path $outputFile -Value "Run and RunOnce Registry Entries:`n"

# Loop through each registry location
foreach ($location in $locations) {
    Write-Output "Checking $location..."

    # Try to get the registry key
    try {
        $key = Get-Item -Path "Registry::$location" -ErrorAction Stop
        $values = Get-ItemProperty -Path "Registry::$location"

        # If there are values, process them
        foreach ($property in $values.PSObject.Properties) {
            if ($property.Name -ne "PSPath" -and $property.Name -ne "PSParentPath" -and $property.Name -ne "PSChildName") {
                # Get creation time of the registry key
                $creationTime = (Get-Item -Path "Registry::$location").LastWriteTime

                # Format output
                $entry = "Location: $location`nValue Name: $($property.Name)`nValue Data: $($property.Value)`nLast Modified: $creationTime`n"
                Add-Content -Path $outputFile -Value $entry
                Add-Content -Path $outputFile -Value "-----------------------------`n"
            }
        }
    } catch {
        Write-Output "Failed to access $location or no data found."
    }
}

Write-Output "Scan complete. Results saved to $outputFile"
```




## Python script for getting processes into .txt file

Get-Process

```powershell
Get-CimInstance Win32_Process | Select-Object Name, ProcessId, CommandLine > test.txt

$processes = Get-CimInstance Win32_Process | Select-Object Name, ProcessId, CommandLine >

Foreach ($process in $processes) {      
	$ip = "$subnet$host"
	Write-Output "Checking $ip..."


Foreach ($host in $range) {       #$host is being defined here
	$ip = "$subnet$host"
	Write-Output "Pinging $ip..."

```

Get-Process | Select-Object -Property ProcessName, Id, Path
Get-CimInstance Win32_Process | Select-Object Name, ProcessId, CommandLine


## Kill A Process

```powershell
#NOTWORKING

Get-Process

function ProcessKiller

	$processtokill = Read-Host "What process would you like to kill?"

	$processes = Get-WmiObject Win32_Process
		Where-Object { $_.Name -like "*processtokill*"}
		
	if (Stop-Process $processes "ProcessName" -Force) {}
		Write-Output "Process has been stopped '$processtokill'"
		return
	}

	  foreach ($proc in $pocesses) {
        [pscustomobject]@{
            Name = $proc.Name
            PID  = $proc.ProcessId
            Path = $proc.ExecutablePath
        }
    }

```

```powershell
function ProcessKiller{

	# Prompt the user to enter the name of the process they want to kill
	$processtokill = Read-Host "What process would you like to kill?"

	# Get all running processes and filter those whose name matches the input
	$processes = Get-Process |
		Where-Object { $_.Name -like "*$processtokill*" }

	# If matching processes are found, attempt to stop each one
	if ($processes) {
		foreach ($proc in $processes) {
			# Forcefully stop the process using its Process ID
			Stop-Process -Id $proc.Id -Force

			# Output confirmation that the process has been stopped
			Write-Output "Process has been stopped '$($proc.Name)'"
		}
	} else {
		# If no matching process is found, notify the user and exit
		Write-Output "No matching process found for '$processtokill'"
		return
	}

	# Display details of the processes that were matched
	foreach ($proc in $processes) {
		[pscustomobject]@{
			Name = $proc.Name              # Name of the process
			PID  = $proc.Id                # Process ID
			Path = $proc.Path              # Path may be null in Get-Process
		}
	}
}
```






### Indy Script

```powershell
function ProcessChecker {


    $checked = Read-Host "What process would you like to check?"

    $BadProcesses = Get-WmiObject Win32_Process |
        Where-Object { $_.Name -like "*$checked*" }

    if (-not $BadProcesses) {
        Write-Output "No processes matching '$checked'"
        return
    }

    foreach ($proc in $BadProcesses) {
        [pscustomobject]@{
            Name = $proc.Name
            PID  = $proc.ProcessId
            Path = $proc.ExecutablePath
        }
    }


}

```








