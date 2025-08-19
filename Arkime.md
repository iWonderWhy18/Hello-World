
[Arkime Demo - Help](https://demo.arkime.com/help?date=-1&exp=asn.dst#sessions)


1. Find all sessions originating from the 192.168.1.0/24 subnet accessing external web servers on port 80.
ip.src == 192.168.1.0/24 && port.dst == 80
5361 Entries

2. Which country does the IP address that accessed any `.ru` domain belong to?
dns.host == *.ru
2

country.dst == ru
208

3. How many TLS version 1 sessions are there in total?
tls.version == TLSv1

4. Which university’s network does the IP address 192.168.1.10 communicate with most frequently? Use the SPI graph on the destination ASN to find out.
AS22877 University of Maryland University College

5. Find FTP sessions initiated by hosts within the 192.168.0.0/8 subnet. There are only two such sessions. For each, identify the destination IP address and the total number of packets transferred.
ip.src == 192.168.0.0/8 && protocols == ftp
Dst IP / Country 
98.114.205.102 US = Packets - 26
147.234.1.253 IL = Packets - 46

6. Find HTTP POST requests that resulted in a 500 Internal Server Error. How many such sessions are there?
http.method == POST && http.statuscode == 500 
7509 entries

7. [Omitted]
8. Find TLS sessions where the JA3 fingerprint matches a known malware fingerprint. How many such sessions are there?
9. Using the Connections view, how many connection groups are there for connections originating from IP addresses located in the United Kingdom (GB)?
10. Find HTTP POST sessions with uploaded data larger than 1 MB. How many such sessions exist?
11. Find TLS sessions that used self-signed certificates (where the certificate issuer and subject are the same). How many such sessions exist?
12. Identify SSH connections using non-standard ports (ports other than 22). How many such sessions are there?
13. Within the internal subnet 192.168.0.0/16, which are the top 3 IP addresses by total number of DNS queries made? How many queries did each make?
14. Which versions of curl appear in the HTTP User-Agent strings in the traffic? List all unique versions found.
15. Among HTTP requests containing the query parameter id, what is the most common URI path accessed?
16. [Omitted]
17. Apart from Basic, what is the only other value seen for http.authtype in HTTP sessions? Identify the value.
18. How many DNS update sessions (opcode UPDATE) are present in the traffic? Additionally, provide a brief explanation (a 'word picture') of what the DNS UPDATE opcode means and when it is used.
19. How many HTTP GET sessions have a response body identified as application/json?
20. Find all FTP sessions where the username used for login is anonymous. How many such sessions exist?
21. [Omitted]
22. Identify the three most common TLS cipher suites observed in the traffic. For each, provide an assessment of its security (e.g., strong, weak, deprecated).
23. Identify which mobile phone manufacturers appear in the HTTP User-Agent strings. List all unique manufacturers found.
24. Find the session where an HTTP GET request returned JSON data with a status code of 302. Provide the details of this session.