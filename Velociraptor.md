
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

