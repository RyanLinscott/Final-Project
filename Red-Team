# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

![nmap scan](./jpgs/Screenshot%202022-07-23%20111713.jpg)

This scan identifies the services below as potential points of entry:
- Target 1
  - ssh port 22
  - http port 80
  - rpcbind port 111
  - netbios-ssn port 139
  - microsoft-ds port 445


The following vulnerabilities were identified on each target:
- Target 1
  - ssh is open 
  - http is open
  - the http has a vulnerable Wordpress server

![nmap scan](./jpgs/Screenshot%202022-07-23%20111713.jpg)

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`{b9bbcb33e11b80be759c4e844862482d}
    - **Exploit Used**
      - ssh to users host after exploting vulnerable worpress server
![ssh](./jpgs/Screenshot%202022-07-23%20124427.jpg)
![ssh result](./jpgs/flag1v2.jpg)
  - `flag2.txt`{fcfd58dcdad9ab23faca6e9a36e581c}
    - **Exploit Used**
      - vulnerable Worpress server
![wpscan](./jpgs/Screenshot%202022-07-23%20123143.jpg)
    `flag3.txt`{afc01ab56b5091e7dccf93122770cd2}
    - **Exploit Used**
      - using the files discovered infiltrate the MySQL server
![MySQL info](./jpgs/Screenshot%202022-07-23%20131649.jpg)
![MySQL command](./jpgs/Screenshot%202022-07-23%20131558.jpg)
![flag3](./jpgs/Screenshot%202022-07-23%20134422.jpg)
![hash values](./jpgs/Screenshot%202022-07-23%20134525.jpg)
    `flag4.txt`{715ea6c055b9fe3337544932f291ce}
    - **Exploit Used**
      - Once we have the hash values we crack them using John the Ripper
![john](./jpgs/Screen%20Shot%202022-07-23%20at%202.05.56%20PM.jpg)
      - After John is finished we can log onto steven's account, he was not included in the sudoers group, but simply by guessing we were able to find the root login password as:
      - Username: root
      - Password: toor
![Got Root](./jpgs/FinalFlagRaven.jpg)
