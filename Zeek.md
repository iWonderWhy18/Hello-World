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
