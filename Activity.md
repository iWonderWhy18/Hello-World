
Load the Windows VM  
hcmadmin
Password1
Rules:
ONLY POWERSHELL CAN BE USED

Do not read any of the artefacts source code (its a powershell activity not an incident response)
(eg. do not use "cat file.xx")



 1. Identify the suspicious "flag" on the system and provide the command used ( hint, it isn't "flag.txt" but it might be close to that)

ANSWER: 
```powershell
Get-ChildItem C:\ -Recurse -Include flag* -ErrorAction SilentlyContinue
```
Directory: C:\Users\usertwo\Music\flag.txt.txt
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        26-Jun-25  11:07 AM              0 flag.txt.txt

ANSWER: 
```powershell
Get-ChildItem C:\ -Recurse -Include *flag* -ErrorAction SilentlyContinue
```
Directory: C:\Users\Public\Music
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        26-Jun-25  11:17 AM             28 theflag.txt



2. Discover active suspicious processes and provide the command used to find it

```powershell
Get-Process | Select-Object -Property ProcessName, Id, Path
```
python - 1324 - C:\Users\hcmadmin\AppData\Local\Programs\Python\Python313\python.exe
pythonw - 4708 - C:\Users\hcmadmin\AppData\Local\Programs\Python\Python313\pythonw.exe

```powershell
Get-ItemProperty -Path HKCU:\Software\Microsoft\Windows\Currentversion\Run
```
run4eva               : pythonw.exe "C:\Users\hcmadmin\AppData\Local\Temp\run4eva.py"

```powershell
Get-CimInstance Win32_Process | Select-Object Name, ProcessId, CommandLine
```


3. Identify how persistence is maintained and which commands you used to find it

```powershell
Get-ItemProperty -Path HKCU:\Software\Microsoft\Windows\Currentversion\Run
```
run4eva               : pythonw.exe "C:\Users\hcmadmin\AppData\Local\Temp\run4eva.py"


```powershell
Get-ScheduleTask
```
TaskPath                                       TaskName                          State
--------                                       --------                          -----
\                                              FlagDropper                       Ready





4. Correlate and collect all related artifacts (submit to instructor for eradication)

Nuke both users





5. Clean the system and provide the commands used to remove the files. 





# cat flag.txt
Flag dropped at 07/31/2025 13:58:01
Flag dropped at 07/31/2025 14:01:01
Flag dropped at 08/11/2025 10:10:01
Flag dropped at 08/11/2025 10:13:01
Flag dropped at 08/11/2025 10:16:01
Flag dropped at 08/11/2025 10:19:01
Flag dropped at 08/11/2025 10:22:01
Flag dropped at 08/11/2025 10:25:01
Flag dropped at 08/11/2025 10:28:01
Flag dropped at 08/11/2025 10:31:01
Flag dropped at 08/11/2025 10:34:01
Flag dropped at 08/11/2025 10:37:01
Flag dropped at 08/11/2025 10:40:01
Flag dropped at 08/11/2025 10:43:01
Flag dropped at 08/11/2025 10:46:01
Flag dropped at 08/11/2025 10:49:01
Flag dropped at 08/11/2025 10:52:01
Flag dropped at 08/11/2025 10:55:01
Flag dropped at 08/11/2025 10:58:00
Flag dropped at 08/11/2025 11:01:00
Flag dropped at 08/11/2025 11:04:00
Flag dropped at 08/11/2025 11:07:00
Flag dropped at 08/11/2025 11:10:00
Flag dropped at 08/11/2025 11:13:00
Flag dropped at 08/11/2025 11:16:00
Flag dropped at 08/11/2025 11:19:00
Flag dropped at 08/11/2025 11:22:00
Flag dropped at 08/11/2025 11:25:00
Flag dropped at 08/11/2025 11:28:00
Flag dropped at 08/11/2025 11:31:00
Flag dropped at 08/11/2025 11:34:00
Flag dropped at 08/11/2025 11:37:00
Flag dropped at 08/11/2025 12:46:01
Flag dropped at 08/11/2025 12:49:01
Flag dropped at 08/11/2025 12:52:01
Flag dropped at 08/11/2025 12:55:01
Flag dropped at 08/11/2025 12:58:01
Flag dropped at 08/11/2025 13:01:01
Flag dropped at 08/11/2025 13:04:01
Flag dropped at 08/11/2025 13:07:01
Flag dropped at 08/11/2025 13:10:01
Flag dropped at 08/11/2025 13:13:01
Flag dropped at 08/11/2025 13:16:00
Flag dropped at 08/11/2025 13:19:00
Flag dropped at 08/11/2025 13:22:00
Flag dropped at 08/11/2025 13:25:00
Flag dropped at 08/11/2025 13:28:00
Flag dropped at 08/11/2025 13:31:00
Flag dropped at 08/11/2025 13:34:00
Flag dropped at 08/11/2025 13:37:00
Flag dropped at 08/11/2025 13:40:00
Flag dropped at 08/11/2025 13:43:00
Flag dropped at 08/11/2025 13:46:01
Flag dropped at 08/11/2025 13:49:01
Flag dropped at 08/11/2025 13:52:00
Flag dropped at 08/11/2025 13:55:00
Flag dropped at 08/11/2025 13:58:00
Flag dropped at 08/11/2025 14:01:00
Flag dropped at 08/11/2025 14:04:00
Flag dropped at 08/11/2025 14:07:00
Flag dropped at 08/11/2025 14:10:00
Flag dropped at 08/11/2025 14:13:00
Flag dropped at 08/12/2025 09:04:01
Flag dropped at 08/12/2025 09:07:01
Flag dropped at 08/12/2025 09:10:01
Flag dropped at 08/12/2025 09:13:01
Flag dropped at 08/12/2025 09:16:01
Flag dropped at 08/12/2025 12:37:02
Flag dropped at 08/12/2025 12:40:01

# CPU Useage
ProcessName   Id       CPU
-----------   --       ---
SearchUI    2224 55.515625
MsMpEng     1956 43.828125
svchost      880  40.59375
System         4 36.171875
taskhostw   3780  20.40625
WmiPrvSE    2228    6.5625
svchost      692  6.109375
svchost     1576   5.78125
svchost      896  5.671875
explorer    3972       5.5







path to run process
ppid for processes
