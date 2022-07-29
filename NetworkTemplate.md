# Network Forensic Analysis Report


## Time Thieves 
You must inspect your traffic capture to answer the following questions:

1. What is the domain name of the users' custom site? 
    ```
    frank-n-ted.com
    ```

2. What is the IP address of the Domain Controller (DC) of the AD network? 
    ```
    10.6.12.12
    ```

3. What is the name of the malware downloaded to the 10.6.12.203 machine? 
    ```
    june11.dll
    ```
![mal_GitHub](https://user-images.githubusercontent.com/96896057/181854985-38360dbe-1a93-4aac-a873-30139f31dc9f.png)

4. Upload the file to [VirusTotal.com](https://www.virustotal.com/gui/). 
5. What kind of malware is this classified as? 
    ```
    Trojan
    ```
![Network_Troj_GitHub](https://user-images.githubusercontent.com/96896057/181854940-2a9c15d5-13e4-4a17-925b-3167e496fe79.png)
---

## Vulnerable Windows Machine

1. Find the following information about the infected Windows machine:
    
    ````
    Host name: ROTERDAM-PC$
    IP address:172.16.4.205
    MAC address: 00:59:07:b0:63:a4

2. What is the username of the Windows user whose computer is infected?
    ```
    matthijs.devries
    ```
![user_Windows_GitHub](https://user-images.githubusercontent.com/96896057/181855091-bab98803-16ce-4f27-8fee-78759d1abd3d.png)

3. What are the IP addresses used in the actual infection traffic?

    ```
    172.12.4.205
    185.243.115.84
    166.62.11.64
    ```

![WireShark_Convo_GitHub](https://user-images.githubusercontent.com/96896057/181855132-6c4fa8fd-04a2-493d-ab99-51fe10c5616f.png)

4. As a bonus, retrieve the desktop background of the Windows host.

![desktop_GitHub](https://user-images.githubusercontent.com/96896057/181399648-f2e4a800-ab65-4ed3-a710-f8122a148893.png)

