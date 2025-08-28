
Platform for searching and monitoring



Index - The set of data you're trying to search

Source Type - The source within the data (Eg. Sourcetype=Zeek)

Time Range (important) - The date ranges of the time the data was ingested. THIS IS NOT TO BE CONFUSED AS THE ARTEFACT TIME (x2)

Index = Eventlogs sourcetype=WinEventLog:Security

Index = host sourcetype=velociraptor


Filtering and fields

Example:

```python
index = Eventlogs sourcetype=WinEventLog:Security
EventCode=4625 user="*jane*"
```

```python
index = Eventlogs sourcetype=WinEventLog:Security
EventCode=4625 user="*jane*" AND user="*smith*"
```

```python
index = Eventlogs sourcetype=WinEventLog:Security
EventCode=4625 OR EventCode=4624 AND user="*jane*" OR user="*smith*"
```

Format the output

- stats
- table
- top/rare
- dedup
- eval
- rename

```python
index = Eventlogs sourcetype=WinEventLog:Security
EventCode=4625 user="*jane*" | table user | dedup user
```

[vaquarkhan/splunk-cheat-sheet](https://github.com/vaquarkhan/splunk-cheat-sheet)






# 🔐 VM Access Details

**VM Password:** `Password1`

If prompted with permission issues, click **"Take Ownership"** and then confirm with **"I Copied It"**.

If the VM requires a reboot, proceed with rebooting.

If the screen resolution appears incorrect or small, click the **"Resize"** button in the VMware toolbar (furthest right option at the top).



### **1 Entry & Initial Execution**

 One process launches another process that is rarely spawned by web browsers.
    
    - Which process pair stands out as unusual and why?
    
```python
index="velociraptor" source="Velociraptor_ETW_ProcessCreation_Flat.json"
|  table result.CommandLine result.Image result.ParentProcessId
```
OR
```python
index="velociraptor" source="Velociraptor_ETW_ProcessCreation_Flat.json"
|  stats count by result.CommandLine result.Image result.ParentProcessId
```
![[Pasted image 20250828134534.png]]


    
    - What user account was responsible for this?

![[Pasted image 20250828134626.png]]


using zeek im trying to find out Which process pair stands out as unusual and why? using the index and source provided. index="velociraptor" source=*








### **2 Network Activity**

Which process establishes an outbound connection to an unfamiliar domain?
    
    - How can you determine whether this domain is suspicious?
        

 Which network connection state would indicate that this communication is actively occurring?
    






### **3 Persistence Mechanisms**

Do you see any new or modified tasks or services configured on the host?
    
    - Which one(s) stand out as suspicious and why?
        
Where on the system is the binary or executable being used for persistence located?
    
    - Is this a typical location for legitimate software?
        

---

### **4️ Data Staging & Exfiltration**

Are there any new archive files on the system that may contain collected data?
    
    - Which one appears suspicious and why?
        
 Do you notice any evidence of these files being prepared for transmission?
    
    - Which user seems involved?
        


---

### **5️ Obfuscation and Detection**

Do you find any command lines or scripts that seem to be attempting to hide their true intent?
  
Which artifacts or fields could help you confirm if the file transfer was successful?
    
 Based on the timeline of events, which action would you have been able to detect first if you had the right detection in place? ( no wrong answers ) 
