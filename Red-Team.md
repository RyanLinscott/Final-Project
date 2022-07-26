# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

![nmap_OS_GitHub](https://user-images.githubusercontent.com/96896057/180900970-cde5b2a9-797e-4be8-8f8b-8d4144ed46a1.png)

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

![nmap_GitHub](https://user-images.githubusercontent.com/96896057/180901150-349de607-5be8-4917-bdaa-220ea62f1844.jpg)

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`{b9bbcb33e11b80be759c4e844862482d}
    ![flag1_GitHub](https://user-images.githubusercontent.com/96896057/180901342-66075ffa-1e88-42cf-9166-1c5b888109db.png)
    - **Exploit Used**
      - ssh to users host after exploting vulnerable worpress server
        ![ssh_michael_GitHub](https://user-images.githubusercontent.com/96896057/180901239-6bba5f41-7242-413c-a7d7-3c352ac368be.jpg)

  - `flag2.txt`{fcfd58dcdad9ab23faca6e9a36e581c}
TODO:
    - **Exploit Used**
      - vulnerable Worpress server
    ![Flag2_GitHub](https://user-images.githubusercontent.com/96896057/180901445-deee105a-67b8-460b-b804-2bdd32d45b44.jpg)
    `flag3.txt`{afc01ab56b5091e7dccf93122770cd2}
    - **Exploit Used**
      - using the files discovered infiltrate the MySQL server
TODO:![MySQL info](./jpgs/Screenshot%202022-07-23%20131649.jpg)
TODO:![MySQL command](./jpgs/Screenshot%202022-07-23%20131558.jpg)
TODO:![flag3](./jpgs/Screenshot%202022-07-23%20134422.jpg)
TODO:![hash values](./jpgs/Screenshot%202022-07-23%20134525.jpg)
    `flag4.txt`{715ea6c055b9fe3337544932f291ce}
    - **Exploit Used**
      - Once we have the hash values we crack them using John the Ripper
TODO:![john](./jpgs/Screen%20Shot%202022-07-23%20at%202.05.56%20PM.jpg)
      - After John is finished we can log onto steven's account, he was not included in the sudoers group, but simply by guessing we were able to find the root login password as:
      - Username: root
      - Password: toor
TODO:![Got Root](./jpgs/FinalFlagRaven.jpg)
