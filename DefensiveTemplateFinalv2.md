# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Windows Host
  - **Operating System**: Windows XP
  - **Purpose**: Client
  - **IP Address**: 192.168.1.1
- Capstone
  - **Operating System**: Linux 2.6.X
  - **Purpose**: Server
  - **IP Address**: 192.168.1.90
- ELK
  - **Operating System**: Linux 2.6.X
  - **Purpose**: Server
  - **IP Address**: 192.168.1.100
- Kali
  - **Operating System**: Linux 2.6.X
  - **Purpose**: Server
  - **IP Address**: 192.168.1.105
- Target1
  - **Operating System**: Linux 3.X
  - **Purpose**: Server
  - **IP Address**: 192.168.1.110
- Target2
  - **Operating System**: Linux 3.X
  - **Purpose**: Server
  - **IP Address**: 192.168.1.115
### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:
- Excessive HTTP Errors
- HTTP Request Size Monitor
- CPU Usage Monitor

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors

Alert 1 is implemented as follows:
  - **Metric**: HTTP Response Codes
  - **Threshold**: Over 400 for the last 5 minutes
  - **Vulnerability Mitigated**: Brute force logins of accounts.
  - **Reliability**: Medium Reliability

#### HTTP Request Size Monitor
Alert 2 is implemented as follows:
  - **Metric**: HTTP Request Bytes
  - **Threshold**: Is above 3500 for the last 1 minute.
  - **Vulnerability Mitigated**: HTTP Request Smuggling
  - **Reliability**: High Reliability

#### CPU Usage Monitor
Alert 3 is implemented as follows:
  - **Metric**: CPU Usage
  - **Threshold**: Percentage of CPU usuage over all documents exceeds 0.5 for the last 5 minutes.
  - **Vulnerability Mitigated**: Denial of Service/Information Extraction
  - **Reliability**: Low Reliability


### Suggestions for Going Further (Optional)
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: Limit HTTP Response Code Errors Count based on IP and send to a DMZ, IP Addresses associated with high volume of requests.
  - **Why It Works**: Allows for further investigation in a "safe" area of the network that blocks potential threats from gaining more ground wihtin network.
- Vulnerability 2
  - **Patch**: Deploy a Web Application Firewall
  - **Why It Works**: A Web Application Firewall can be used to sanitize HTTP traffic and detect abnormal requests
- Vulnerability 3
  - **Patch**: Limit excessive CPU Utilization based on work time.
  - **Why It Works**: When a process/child item is utilizing too much CPU processing power for a prolonged amount of time, the process is terminated and memory dump created which can then be analyzed for further tuning.
