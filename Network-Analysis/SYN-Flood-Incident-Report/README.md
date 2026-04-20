# Incident Report: TCP SYN Flood Analysis

## Project Overview
This project involves the identification, analysis, and mitigation of a network-layer attack directed at a travel agency's web server. As the security analyst, I investigated an automated alert regarding server unresponsiveness and used packet sniffing tools to diagnose a **TCP SYN Flood** attack.

## Incident Summary
* **Symptoms:** Users and employees received "connection timeout" error messages when attempting to access the company's sales webpage.
* **Detection:** Captured data packets revealed a massive volume of TCP SYN requests originating from an unfamiliar IP address.
* **Attack Type:** **TCP SYN Flood** (Denial of Service).
* **Root Cause:** An attacker exploited the TCP three-way handshake by sending continuous SYN packets without completing the connection, exhausting the server's ability to respond to legitimate traffic.

## Technical Analysis (Wireshark Evidence)
The investigation utilized network logs to differentiate between normal traffic and the attack pattern. Legitimate traffic follows a standard [SYN] -> [SYN, ACK] -> [ACK] sequence, while the attack traffic consisted of repeated [SYN] requests without the final acknowledgment.

### **Log Analysis Snippet**
The following data illustrates the transition from a successful HTTP GET request to the onset of the connection failure:

| No. | Time | Source | Destination | Protocol | Info |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 47 | 3.144 | 198.51.100.23 | 192.0.2.1 | TCP | 42584->443 [SYN] Seq=0 |
| 48 | 3.195 | 192.0.2.1 | 198.51.100.23 | TCP | 443->42584 [SYN, ACK] Seq=0 |
| 49 | 3.246 | 198.51.100.23 | 192.0.2.1 | TCP | 42584->443 [ACK] Seq=1 |
| 50 | 3.298 | 198.51.100.23 | 192.0.2.1 | HTTP | GET /sales.html HTTP/1.1 |
| 51 | 3.349 | 192.0.2.1 | 198.51.100.23 | HTTP | HTTP/1.1 200 OK |

*Note: Subsequent logs show a surge in [SYN] packets from unfamiliar IPs with no corresponding [ACK] from the source, leading to server timeout.*

## Impact on Organization
* **Service Interruption:** Critical sales pages were unavailable to customers, leading to potential loss of revenue.
* **Operational Downtime:** Internal employees could not search for vacation packages, disrupting the core business workflow.
* **System Integrity:** The web server was overwhelmed and required being taken offline to flush half-open connections and recover.

## Response & Remediation
1.  **Containment:** Temporarily took the server offline to clear the backlog of half-open TCP connections.
2.  **IP Blocking:** Configured the company's firewall to drop all traffic from the malicious source IP address identified in the logs.
3.  **Long-term Hardening:**
    * Proposed the implementation of **SYN Cookies** to manage connection state more efficiently.
    * Recommended configuring **Rate Limiting** on the firewall to prevent a single IP from overwhelming the Transport Layer (Layer 4).

## Files in this Repository
* `Incident_Report_SYN_Flood.pdf`: Full detailed report including response steps.
* `evidence/network_capture_log.csv`: Filtered Wireshark log showing the attack pattern.