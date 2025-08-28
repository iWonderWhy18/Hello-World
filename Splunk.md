
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

