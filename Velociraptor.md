
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



