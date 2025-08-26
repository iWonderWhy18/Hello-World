![[Corelight-Zeek-Cheatsheet-8.0.pdf]]


What is Zeek


Why we use it


Log outputs


Exploring Zeek Logs



Cat dhcp.log | zeek-cut host_name client_addr | sort | uniq



```python
cat dns.json | jq '.'
```

```python
cat http.json| jq 'select(.["id.resp_h"] = "10.0.0.100")'
```

```python
cat http.json| jq 'select(.method = "GET")'  
```

```python
cat http.json| jq '. | {uri, query}'    
```

```python
cat dns.json| jq 'select(.["id.resp_h"] == "10.0.0.100")' | jq '.["id.resp_h"]'
```

```python
cat dns.json| jq 'select((.["qtype_name"] = "AAAA") and (.["proto"] = "udp"))'
```

How many times certain ip addresses have gone to github.com

```python
cat dns.json | jq -r 'select(.query == "github.com" and .qtype_name == "A" and .proto == "udp") | .id.orig_h' | sort | uniq -c
```


To see how many times each domain was queried with an `A` record:
```python
cat dns.json | jq -r 'select(.qtype_name == "A") | .query' | sort | uniq -c | sort -nr
```



http log

show all GET methods that are not using default/traditional port numbers



how many times each unique `arg` value appears, here's a clean and powerful way to do it using `jq`.
```python
cat ftp.json | jq -r 'select(.arg != null) | .arg' | sort | uniq -c | sort -nr
```

