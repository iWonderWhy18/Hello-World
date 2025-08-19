
![[Pasted image 20250814111815.png]]


Deployment

- Group Policy
- Services




## What is Velociraptor?

[Velociraptor](https://docs.velociraptor.app/) is an open-source endpoint monitoring, digital forensics, and cyber response platform owned by [Rapid7](https://www.rapid7.com/). It was created by experts in digital forensics and incident response who required a simpler and more effective approach to look for particular system artifacts and keep track of actions across a fleet of endpoints.

The Velociraptor tool allows analysts to react more skillfully to a variety of digital forensics, incident response (DFIR), and data breach investigations by providing them with the means of being able to collect and hunt for data swiftly and effectively.

Velociraptor works on all major operating systems, including Windows, Linux, and macOS. You can deploy Velociraptor installations by using [SCCM](https://learn.microsoft.com/en-us/mem/configmgr/core/understand/introduction) or [Group Policy](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831791\(v=ws.11\)) with relative ease.

#### Core features

Velociraptor allows analysts to query system information, view running processes, explore the filesystem, view currently connected sockets of any system within their infrastructure, and more. Given how intuitive and feature-rich the Velociraptor tool is, it should come as no surprise that most analysts choose to adopt this tool and have it within their arsenal.

With Velociraptor, you can:

- Reconstruct the actions of an attacker using digital forensics analysis
- Continuously monitor for unusual user behavior, including files being copied to USB devices
- Hunt for indications of sophisticated adversaries positioned within a network
- Identify any private or proprietary information being disclosed outside of the network
- Collect endpoint data over time for use in threat hunting and future DFIR investigations
- Assess malware outbreaks and other abnormal network behavior


![[Pasted image 20250814113303.png]]


## Velociraptor query language

Velociraptor’s query language (VQL) is central to its operation and gives Velociraptor the ability to query endpoints, collect forensic artifacts, and gather information on endpoint state. Based on [SQL](https://www.w3schools.com/sql/), VQL is an expressive query language that's easy to use and simple to understand.

VQL was created to readily adapt to the analyst's needs without requiring any changes to scripts, queries, artifacts, or third-party tooling. VQL incorporates digital forensics knowledge into [artifacts](https://docs.velociraptor.app/docs/vql/artifacts/) (YAML-based, human-readable files) which can then be freely shared and traded among the community.

Understanding and extending Velociraptor to its full capacity depends heavily on having a firm knowledge and understanding of VQL, which will be covered in more depth later in the series.

## Server and agents

Velociraptor works on a server-client model. Clients are installed as an agent on endpoints throughout the network and communicate with the server over TLS to acquire tasking.

A typical deployment would include:

- **Velociraptor server:** The main server component that clients across the network communicate back with
- **Velociraptor client:** Velociraptor agents are installed across all endpoints within the network
- **Web graphical user interface (GUI):** A web application presenting the administrative interface – analysts interact with this daily to gather system artifacts and query system information across endpoints in the network
- **API server:** A server used to push and receive API requests

Unique configuration files are created for every deployment and contain details like connection URLs, DNS names, and special cryptographic keys.

Based on command line arguments used in the installation process, the single binary version of Velociraptor can function as a server, client, or a variety of utility programs. The lack of an external datastore in Velociraptor makes it simple to manage data lifecycles and perform backups because all data is kept in the server's filesystem. No new infrastructure, such as databases or cloud services, is required.

Distributed file systems like [Amazon EFS](https://aws.amazon.com/efs/), [Google Filestore](https://cloud.google.com/filestore), or standard [NFS](https://en.wikipedia.org/wiki/Network_File_System) are all compatible with Velociraptor.

![[Pasted image 20250814113319.png]]


## Getting started with Velociraptor

When opening Velociraptor for the first time, you'll be met with a splash screen welcoming you to the tool! This page will also direct you to some common tasks that you can undertake using the GUI. Ignore these useful links for now, as this series will take you through the discrete parts of the GUI manually.

![[Pasted image 20250814113639.png]]

Clicking on the three bars in the top left (known as the hamburger icon) will expand your options. The first option is **Home**, a dashboard showing the basic information of the Velociraptor server itself. It includes **server status**, **disk space**, **users**, and **server version**, providing quick access to assessing the health of the Velociraptor server. You can edit this dashboard to contain any **server artifacts**, which are artifacts specifically about the internal functions and events on the Velociraptor server itself. You can customize this to see only information important to your setup.

## Interacting with clients

Clicking the **magnifying glass** at the top without any search parameters returns all agents currently and historically connected to the server. Clicking on the **Client ID** brings you to the agent's **host information page**. Here is where you can start interacting with agents and discovering data about them.

![[Pasted image 20250814113658.png]]

When hosts first connect to the server, they are automatically interrogated to gather the metadata you see in the screenshot above. This includes the operating system, Client ID, and timestamps for first seen and last seen, to support investigations and management of the agents. The interrogation can be done again at any time by clicking the **Interrogate** button to generate more up-to-date metadata in case of any changes.

![[Pasted image 20250814113710.png]]

#### VFS

The Virtual File System (VFS) is the remote listing of the file system of the client. This allows you to remotely search through the file system as it was when it was queried by the client. Linux clients will show you **File** and **Artifacts** listings. File allows you to navigate through the file system and find and download any file you want (that can be discovered on it), while Artifacts shows you a list of collected artifacts about the client. Windows clients have a different choice of listings however: **NTFS** is equivalent of File, and there's also a **Registry** option to look through and review any registry keys on the client.

To navigate through the VFS, you can head to each layer of the directories by simply clicking on them. To initially refresh (or for your first time, generate) the listing, click the **folder icon** found in the middle top of the screen. This will generate a listing of just what's contained in that directory. To generate a listing recursively within subdirectories, you can select the **folder icon with the capital R** on it. This may take a while, depending on where you are in the structure of the file system and the number of files and subdirectories there are. You can also recursively download a directory from a client by selecting the **floppy disk icon with the capital R**.

You may notice that after doing a directory listing, or any of the other actions above, the **eye icon becomes selectable**. Clicking this will take you to the collected artifacts menu and show you the specific artifact for generating that listing. The collected artifacts menu is where you can find a comprehensive list of any artifacts that are collected from clients for your review.

Back on the host information page, the next icon is a first aid box, which allows you to **rapidly quarantine a host** and prevent it from communicating with anything except the Velociraptor server. It does this by first adding the **Quarantine** label to the host, which sets off any automatic function to edit the host's firewall to only allow Velociraptor communication. The label is defined server side, which means that the quarantine will maintain through reboots. You can still communicate with it remotely.

## Hunting for artifacts

You can search for evidence during an investigation with Velociraptor. Select **Hunt Manager** from the menus on the left, to see what's available. Initially, you'll find a blank screen with only options to **create a new hunt** (the plus icon) and **delete a hunt** (the bin icon). You can define the metadata, including the description and an expiry of the hunt to prevent it from overrunning. Select the artifact(s) you want to discover on your selected hosts, specify how much of the server's resources you want to commit to the hunt, and then review the JSON structure of the hunt. Finally, save the created hunt using **Launch**. Two more of the options should now be available as a hunt is selected, **running it** (the play button), and **copying it** (the two sheets icon) for further development.

## Hunting for event logs

Event logs are typically one of the first artifacts an investigation can start with. Velociraptor has several pre-made artifacts for discovering specific types of event logs and attacks that can be discovered in them. This includes **PowerShell running**, **RDP auth logs**, **scheduled tasks**, and **kerberoasting**. However, all the event logs on a host can be gathered using the artifact `Windows.EventLogs.Evtx`, which will return a JSON file containing the structured logs from the chosen client. You can also limit which logs are returned using a regex to search through the message field of events if you use the alternative artifact `Windows.EventLogs.EvtxHunter`.

To **gather event logs** using Velociraptor, you first **navigate to the Hunt Manager**. Creating a new hunt, you specify the artifact you're looking for (and any specific clients you want to limit the hunt to) on the **Select Artifacts** tab. You can configure any parameters, such as the time range of the logs and the regex, if you use the `EvtxHunter` artifact on the **Configure Parameters** tab. Select **Launch**, then running this hunt shouldn't take long. You can download the results in the bottom right **Results** box – select the **file storage box icon**, then **Full download** for the complete results of the hunt. This includes the details of the hunt, a file containing all the results, and then a breakdown by client of the artifacts gathered and the artifacts of each client in a subdirectory structure called **Clients**.

![[Pasted image 20250814113738.png]]



# Introduction to Velociraptor: Ep.3 – VQL


## What is VQL?

Velociraptor has many powerful features and applications – as you probably know from the series so far. But you need to learn how these are succinctly **packaged up and made reusable**, most of which is done using **Velociraptor Query Language (VQL)** made into artifacts. VQL is a query language like SQL, used to query structured data sets and discover key information such as **evidence of execution**, where certain parts of **metadata may be inconsistent**, and **systems that make up specific environments**.

Linux.Sys.Services

Type: client

Parse services from `systemctl`

```
LET services = SELECT Stdout FROM execve(argv=['systemctl', 'list-units', '--type=service'])

LET all_services = SELECT grok(grok="%{NOTSPACE:Unit}%{SPACE}%{NOTSPACE:Load}%{SPACE}%{NOTSPACE:Active}%{SPACE}%{NOTSPACE:Sub}%{SPACE}%{GREEDYDATA:Description}", data=Line) AS Parsed
FROM parse_lines(accessor="data", filename=services.Stdout)
        
SELECT * FROM foreach(row=all_services, column="Parsed") WHERE Unit =~ ".service"
```

The fundamental structure is similar to a simplified SQL sentence structure. You `SELECT` the item to search, `FROM` the source you wish to search, `WHERE` your defined (optional) conditions are met. This structure makes up all VQL queries. None of the more complex features exist in other query languages, such as JOIN functions, as the language isn't designed to achieve these results purely programmatically. This potential shortcoming is instead made up of plugins, allowing you to gather and serialize data then use VQL to interact with it programmatically, keeping the outputs consistent and easy to parse.

## Querying using VQL

VQL queries are applied lazily. This means that the execution of the evaluation stages of the query are stopped until the very last moment that they can be. Lazy evaluation in VQL stops Velociraptor from wasting resources doing a larger query when much of the source data can be filtered out from the query by conditions you've added to it. For example:

```
## This will return all the OS' from the data the info plugin gathers
SELECT OS FROM info()

## This will gather all the same data, but will filter out any data that does not have OS matching windows
SELECT OS FROM info() WHERE OS = "Windows"
```

#### Subqueries

VQL can also contain subqueries – queries within queries. This allows you to manage the complexity of queries by limiting them to specific parts of the evaluation and add in more conditional execution. For example, you can use the `if()` plugin to evaluate whether a condition is met and then execute a subquery.

```
LET history_files = SELECT * from foreach(
	row={
		SELECT Uid, Name AS User,
			expand(path=Directory) AS HomeDirectory
		FROM Artifact.Windows.Sys.Users()
		WHERE Name =~ userRegex
	},
	query={
		SELECT User, OSPath, Mtime
		FROM glob(globs=historyGlobs, root=HomeDirectory)
	})
```

Understanding the lifecycle of a query can help you diagnose any logic errors that might occur during execution. Luckily, this process is simple:

1. Plugins are called, and any supplied arguments are passed to them to generate the information for processing the rest of the VQL query.
2. Once the full set of information is received, it's contained in a lazy evaluator to be further processed.
3. The created evaluation is then evaluated against filter conditions to eliminate non-applicable data from the results.
4. The query then returns the data that makes it through the filter to you!

## Programmatic VQL

Like any programming language, VQL contains at least two more expected features: **operators** and **control structures**. Control structures have already been mentioned, where you can use conditional `if` statements to decide on whether a subquery should run, but you can also expect more to use while generating a query:

- `foreach()` – allows you to iterate over individual parts of data (called rows) and apply another query to it.
- `switch()` – allows you to iterate over a list of subqueries in the order they're defined until one returns any data. This then stops evaluation except for the one that's returned data.
- `chain()` – similar to `switch()`, except all queries are evaluated. This is then all combined into one output rather than three.

VQL also contains the operators you'd expect to find in a programming language, including the arithmetic `+ - * /` operators, comparison operators `= != < > <= >=`, the contains operator `in`, the regex operator `=~`, and the associative operator `.`.

## Output complexity

As queries become larger and larger, they become more difficult and, by definition, more complex. Luckily, you can manage the output of queries in a way that cuts down complexity by using the different features mentioned above. However, managing the data during and after a query can be the core of why such complexity exists. VQL contains a syntax called `GROUP BY`, where you can decide how the individual pieces of data are grouped and managed during a query and any subqueries evaluating it by organizing it into bins depending on the condition you've set. For example, if you group by OS, you'll receive the number of each unique bin created and, therefore, the number of each unique OS identifier. You can aggregate this data even further by using built-in aggregate functions, such as: `count()` to add the total number of rows in each bin, `sum()` to add up values, and `enumerate()` to add all the values into an array.

## Applying VQL

VQL is the core of the artifacts functionality in Velociraptor. Each artifact is essentially a YAML file containing a VQL query to execute and reuse as many times as they'd like. This is how VQL is applied into Velociraptor by default – by being the driving function that allows you to search and return any piece of information or data that an OS can possibly recover and return. You can then evaluate that across entire environments quickly and simply. The complexity is written once, becomes repeatable, and supports your investigations across your systems.

But once the information is retrievable and the artifacts are created, Velociraptor can visualize it using the **notebooks** feature. Here you can add in artifacts and create VQL queries on the fly, creating complex and deep-diving discoveries into systems and visualizing them into clear, functioning output for both reporting and further investigation.

![[Pasted image 20250815083847.png]]



# Introduction to Velociraptor: Ep.4 – Searching

## Velociraptor plugins

The previous episode in this series looked at the VQL syntax and how it improves the usability of Velociraptor. But without a strong set of plugins, VQL can't be used to its full potential. The vast amount of VQL plugins and features that are tailored toward effective DFIR investigations and detections are what make Velociraptor so powerful!

This episode introduces you to a Velociraptor plugin for performing the most common operations within a DFIR investigation: **searching for files**.

## Searching filenames

Finding files quickly is one of the most performed tasks during a DFIR investigation. But one of the most commonly asked questions is…

Using Velociraptor, you can search for the filename, file content, file size, and other criteria of the file on any system connected to Velociraptor.

Velociraptor's `glob()` plugin allows you to search for files using a glob expression. This is the most popular method for searching by filename. The glob expression allows Velociraptor to scan the filesystem for matches using wildcards. The following list represents the syntax of the glob expressions:

`*` – A wildcard match (e.g. `*.exe` matches all files ending with `.exe`)

`{}` – Used for searching for multiple alternatives (for example `*.{exe,zip,dll}`)

`**` – Recursive wildcards (for example `C:\Users\**\*.exe`)

#### Conducting a hunt

The first Velociraptor artifact for filename searches on a Windows system is **Windows.Search.FileFinder**. Note that Linux and Mac operating systems have their own specific Velociraptor artifacts used to search for files within their own filesystems.

To use the **Windows.Search.FileFinder** artifact, analysts must first create a **hunt** within Velociraptor. To do this, click the hamburger icon in the top left corner of the Velociraptor GUI, and navigate to **Hunt Manager**.

![[Pasted image 20250815085628.png]]

Clicking the plus icon will open up the **New Hunt** configuration wizard. On this page, you can enter details such as the description of the hunt, select what operating systems to target, and define when the hunt will expire, among other properties. Because you're searching for files within your Windows fleet, it's recommended to set the **Include Condition** to **Operating System** and set **Windows** as the **Operating System Included**.

![[Pasted image 20250815085642.png]]

After setting those properties and writing a brief description, everything else can be left as default.

Navigate to the next tab, **Select Artifacts.** From here, you can search for **Windows.Search.FileFinder**.

The next step is to **Configure Parameters** for each of the selected artifacts used in the hunt. Clicking the **spanner icon** will bring up the configuration page. Within the **SearchFilesGlobTable** parameter, you'll notice that an example search location has already been provided. It's common practice to delete this entry so that you're able to replace it with a more specific location tailored to your hunt. Do this by clicking the **trash can** icon.

![[Pasted image 20250815085656.png]]

The **SearchFilesGlob** parameter is where you tell Velociraptor what to hunt for using glob expressions.

Say you want to search for all text files within a specific user's home directory. Taking what you've previously learned, you could craft a glob expression to search this location and provide a wildcard syntax to search for all text files, such as with the following glob expression:

`C:\Users\IMLUser\Documents\*.txt`

**All other properties can be left as default.** Finally, click the Launch tab to save and create the hunt.

You've just set up your first hunt in Velociraptor!

Next, you need to execute the hunt. By default, all hunts are created in a paused state. Highlight the new hunt entry you just created, and click the **Play** button to kick it off.

![[Pasted image 20250815085708.png]]

Depending on the size of the fleet, executing a hunt should only take a couple of seconds. Because Velociraptor is built on the VQL language, this drastically speeds up the process of mass querying multiple machines at once. When a hunt is complete, the total number of **Finished Clients** must match the number of **Total Scheduled** clients.

![[Pasted image 20250815085718.png]]

Click on the **Notebook** tab to view the results of the hunt. If the hunt discovered any file matching the glob expression criteria, they'll be displayed here, along with other information such as size, creation time, permissions, etc.

![[Pasted image 20250815085731.png]]


# Introduction to Velociraptor: Ep.5 – NTFS

## Analyzing the NTFS using Velociraptor

Approaching the Windows file system is simple. Launch the OS, open the file manager, and you've made it. You can explore, search, and customize to your heart's content. However, dealing with the file system as a forensic artifact containing other artifacts requires you to manage the approach differently. Careful interaction using technical tooling allows you to do this by controlling the metadata impacted by interaction and ensuring every stage of the forensics process is sound and meets the needs of the investigation.

To learn more about digital forensics investigations, take a look at the following lab:

### NTFS primer

Windows has three main options for filesystems that the OS runs on:

- File Allocation Table (FAT)
- High-Performance File System (HPFS)
- New Technology File System (NTFS)

Each of these options has certain features that make them useful for different needs. But the default filesystem used for Windows is NTFS.

NTFS allows the system to be reliable and straightforward by not creating hardware dependencies or things unique to that operating system.

### Master File Table

You can track every file using the Master File Table (MFT), which keeps a record of each file on the filesystem, including itself. Data stored includes the file name, size, timestamps, permissions, and metadata on the content and file.

To learn more about the MFT, take a look at the following lab:

The MFT stores files that are on the filesystem, but also deleted files may be removed from the MFT by the filesystem. Deleted files become marked as “**free**” and the space becomes free to use by other files.

### Volume Shadow Copy

The system also has a feature called Volume Shadow Copy Service (VSS). VSS backs up every file into a **shadow copy,** where they can be rapidly recovered and brought back into functionality in the case of system failures or accidental loss. While this doesn't provide an appropriate enterprise backup, it can be helpful for on-the-fly work where changes can be rapid, such as automatically updating an application. Forensic investigators can recover files deleted during an incident by discovering the files either partially or wholly within the VSS and retrieving the file's contents for review. For more information on VSS, take a look at the following lab:

## Discovering files using Velociraptor

Knowing each of the filesystem's nuances can allow you to gather evidence quickly and effectively.

Velociraptor makes this easy by providing the necessary features to parse different sections of the NTFS at speed.

![[Pasted image 20250815092419.png]]

## NTFS accessor

Velociraptor allows you to parse the raw NTFS from a filesystem with an **NTFS accessor**.

An **accessor** in Velociraptor is simply a driver used to **interact with the system directly** rather than through more abstracted APIs. Direct access allows you to have fewer potential points of contact with other parts of the system the agent is running on. This adds a **layer of protection** against other possible forms of interception. It then parses it into both a human and machine-readable format that makes it easier to perform forensic analysis remotely. Alternative Data Streams (ADS) can also be seen and used for forensic processes from the accessor, showing any other data streams potentially attached to MFT entries and hidden files from this.

By using the accessor alongside the **Windows.Search.FileFinder** artifact, you can find any file matching your requirements. However, discovering files this way is very resource-intensive.

### `parse_mft() + windows.ntfs.mft`

Reading the MFT file is much less intensive, while still providing valuable forensic data. You can use Velociraptor's `parse_mft()` plugin that allows you to access to the MFT parser built into the Velociraptor and build VQL queries using it. This means that rather than downloading files and using many more resources, you can get a summary of each entry in the MFT file, including its timestamp, name, and MFT ID.

This is the first and quickest step you can take to discover files on the system beyond using the interactive filesystem in the admin GUI. However, when you need to learn more information than the `parse_mft()` plugin provides, you may want to use the `parse_ntfs()` function, which takes the ID of the MFT entry and provides all the information concerning the entry, including the file it refers to, files it may have referred to, and any ADS and associated information.

### Accessing MFT as an artifact

A few of the options above can overcomplicate evidence gathering where you may not wish to interact with or write VQL. The **Windows.NTFS.MFT** artifact parses the MFT file and returns the records depending on which switches you've used and edited. This can be used to recover a deleted file by taking the ID of the file you wish to recover from the MFT and providing it to the **Windows.NTFS.Recover** artifact to return the file if it can be recovered.

For more information on Windows.NTFS.MFT, [click here](https://docs.velociraptor.app/artifact_references/pages/windows.ntfs.mft/).

For more information on Windows.NTFS.Recover, [click here.](https://docs.velociraptor.app/artifact_references/pages/windows.ntfs.recover/)

## Timeline analysis

All this information combined can be overwhelming and hard to keep track of, especially when building the story of what happened on the system during the incident being investigated. Evidence is usually visualized with **timelines** to quickly understand what happened and where. Using `ORDER BY` with the timestamp field (alongside any other sub-queries that define the evidence you wish to see) generates a timeline of when events occurred. Evidence was generated to report the story of the incident properly and associate evidence across events.


# Introduction to Velociraptor: Ep.6 – Triage

## Triage

In digital forensic incident response (DFIR), triaging refers to the process of swiftly gathering data about a system to determine whether or not it's relevant to a forensic investigation. Although many people associate triage with just file collection, in Velociraptor, there's actually no distinction between file collection and other non-volatile artifact collections. Triaging is just the act of capturing machine state or any other volatile data. This includes information on running processes, active network connections, etc.

## Collecting files

For the purpose of recording machine states at a particular moment in time, it's critical to effectively and swiftly gather and store evidence. One of the most commonly used Velociraptor artifacts for doing so is **Windows.KapeFiles.Targets**, which is based on the open-source tool [KapeFiles](https://github.com/EricZimmerman/KapeFiles). The Velociraptor KapeFiles artifact can gather information on a large number of files in a relatively short amount of time. It collects data on files based on the file targets listed, but won't perform any analysis on them.

To set up and configure a collection, you must first select a machine from the list of hosts in Velociraptor. Once you've selected a host, the **Collection** button will become available.

![[Pasted image 20250815093603.png]]

Next, click on the **Plus** icon to open the **New Collection** wizard. From here, you can search for the **Windows.KapeFiles.Targets** artifact:

![[Pasted image 20250815093615.png]]

Once selected, head to the **Configure Parameters** tab and click on the **Wrench** icon to see what sort of files can be collected. KapeFiles is extremely powerful because it has a fine-grained list of files that can be collected by default. Such collections include information on:

- Antivirus logs
- Registry hives
- MFT records
- Discord information
- Browser cache
- Event logs
- Microsoft Office cache
- And much, much more!

To conduct a collection, make sure the **check box** is ticked next to the list of files that need to be reviewed as part of the investigation requirements. For the purpose of this demonstration, select the **_BasicCollection** option:

![[Pasted image 20250815093626.png]]

The next step is to specify the resources available for the collection. The KapeFiles artifact can recover a vast amount of file data from the endpoints, but it may take a while to complete depending on how much information needs to be captured. The resource control of the collection must consequently be updated to accommodate this:

![[Pasted image 20250815093636.png]]

Once the correct amount of resources has been assigned (for this lab, these can be left as default), you can launch the collection. Keep an eye on the **State** variable within the **Artifact Collection** tab.

![[Pasted image 20250815093649.png]]
Once the state variable returns **FINISHED**, the collection has been completed.

### Results

To view the results of the collection, navigate to the **Results** tab. From here, you can see all of the files (that are stored on the system at the time the collection was conducted) that match the file format criteria assigned within the collection parameters.

![[Pasted image 20250815093701.png]]

