Network Traffic Analysis: DNS Incident Report
1. Project Overview
This project demonstrates the analysis of a cybersecurity incident involving network connectivity issues. Using tcpdump, network traffic was captured to diagnose why users were unable to access the domain www.yummyrecipesforme.com. The investigation focused on the interaction between UDP, DNS, and ICMP protocols at the internet and transport layers.

2. The Scenario
Multiple users reported a "destination port unreachable" error after waiting for the client page to load. As a cybersecurity analyst, I utilized protocol analysis to determine if the issue was related to the application, transport, or internet layer of the TCP/IP model.

3. Technical Evidence (tcpdump log)
The following log capture represents the repeated attempts by the client machine (192.51.100.15) to query the DNS server (203.0.113.2).


13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 150

4. Root Cause Analysis
A. Protocol Investigation
DNS via UDP: The logs show the browser initiating a DNS request via the UDP protocol on Port 53.

The Goal: The browser was requesting an A record to map the domain name to an IP address.

B. Error Identification
ICMP Response: The response udp port 53 unreachable confirms that the server at 203.0.113.2 is online but is actively rejecting traffic to the DNS service.

Port 53 Analysis: Since Port 53 is dedicated to DNS, the "unreachable" status indicates that no service was listening on that port to receive the query.

C. Final Conclusion
The failure is likely due to the DNS service (daemon) being down on the server or a firewall rule blocking incoming UDP traffic on Port 53. Without successful DNS resolution, the browser cannot find the destination IP to send an HTTPS request, resulting in the timeout error for users.