# Network Activity and Connection Analysis

## PART 1 — CONNECTION ANALYSIS 

**1. List the unique source IP addresses found in the logs.**

     1. 192.168.1.25
     2. 192.168.1.30
     3. 10.0.0.20
     4. 10.0.0.35
     5. 192.168.1.45
     6. 192.168.1.60
     7. 203.0.113.88
     8. 192.168.1.70
     9. 192.168.1.80
     10. 192.0.2.55
     11. 192.168.1.90
     12. 10.0.0.25
     13. 192.168.1.110
     14. 198.51.100.250 
     15. 192.168.1.120
     
**2. Identify the internal source IP addresses.**

     1. 192.168.1.25
     2. 192.168.1.30
     3. 10.0.0.20
     4. 10.0.0.35
     5. 192.168.1.45
     6. 192.168.1.60
     7. 192.168.1.120
     8. 192.168.1.70
     9. 192.168.1.80
     10. 192.0.2.55
     11. 192.168.1.90
     12. 10.0.0.25
     13. 192.168.1.110
     14. 192.168.1.120

**3. Identify the external source IP addresses involved in inbound activity.**

      1. 203.0.113.88
      2. 198.51.100.250
 

**4. List the different destination ports found.**

     1. 53
     2. 5432
     3. 443
     4. 25
     5. 8080
     6. 3389
     7. 22
     8. 4444
     9. 445

**5. Identify the protocols used.**

     1. UDP
     2. TCP

**6. Identify two examples of internal communication.**

     1. device=APP-SRV-01 - src_ip=10.0.0.20 - dst_ip=10.0.0.50 
     2. device=WS-02 - src_ip=192.168.1.30 - dst_ip=10.0.0.20

**7. Identify two examples of outbound communication.**

     1. device=WS-01 - src_ip=192.168.1.25 - dst_ip=8.8.8.8 
     2. device=WS-02 - src_ip=192.168.1.30 - dst_ip=93.184.216.34

**8. Identify two examples of inbound communication.**

      1. device=FW-01 - src_ip=203.0.113.88 - dst_ip=192.168.1.100
      2. device=WEB-SRV-01 - src_ip=192.0.2.55 - dst_ip=10.0.0.10

**9. Identify which connections were allowed and which were blocked.**

       **BLOCKED**

            1. device=WS-05 src_ip=192.168.1.70 - dst_ip=203.0.113.99
            
            2. device=FW-01 src_ip=198.51.100.250 - dst_ip=192.168.1.100
            
            3. device=FW-01 src_ip=192.168.1.110 - dst_ip=192.168.1.100
            
            4. device=FW-01 src_ip=203.0.113.88 - dst_ip=192.168.1.100


      **ALLOWED**

            1. device=WS-01 src_ip=192.168.1.25 - dst_ip=8.8.8.8
            
            2. device=WS-02 src_ip=192.168.1.30 - dst_ip=93.184.216.34
            
            3. device=APP-SRV-01 src_ip=10.0.0.20 - dst_ip=10.0.0.50

            4. device=MAIL-01 src_ip=10.0.0.35 - dst_ip=198.51.100.25

            5. device=WS-03 src_ip=192.168.1.45 - dst_ip=203.0.113.50

            6. device=WS-04 src_ip=192.168.1.60 - dst_ip=198.51.100.77

            7. device=WS-01 src_ip=192.168.1.25 - dst_ip=8.8.8.8

            8. device=WS-06 src_ip=192.168.1.80 - dst_ip=198.51.100.200

            9. device=WEB-SRV-01 src_ip=192.0.2.55 - dst_ip=10.0.0.10

            10. device=WS-02 src_ip=192.168.1.30 - dst_ip=10.0.0.20

            11. device=WS-07 src_ip=192.168.1.90 - dst_ip=198.51.100.150

            12. device=APP-SRV-02 src_ip=10.0.0.25 - dst_ip=10.0.0.50

            13. device=WS-08 src_ip=192.168.1.110 - dst_ip=203.0.113.120

            14. device=WS-09 src_ip=192.168.1.120 - dst_ip=203.0.113.200 


## PART 2 — PATTERN ANALYSIS 

**1. Identify a source system that repeatedly communicates with the same external destination.**

     1. device=WS-03
     
     2. device=WS-06

     3. device=WS-07

     4. device=WS-08

     5. device=WS-09

**2. Identify two different repeated connection patterns.**

      1. device=WS-04 src_ip=192.168.1.60 src_port=55210 dst_ip=198.51.100.77 dst_port=8080
      
      2. device=WS-06 src_ip=192.168.1.80 src_port=51000 dst_ip=198.51.100.200 dst_port=4444
  
**3. Which system communicates repeatedly with an external destination using port 4444?**

      1. device=WS-06

**4. Which repeated activity looks suspicious but cannot be confirmed as malicious based only on the log?**

      1. device=WS-06 src_ip=192.168.1.80 src_port=51000 dst_ip=198.51.100.200 dst_port=4444 protocol=TCP

**5. Identify one repeated activity that appears likely to be normal based on the application field.**

      1.device=WS-03 src_ip=192.168.1.45 src_port=54001 dst_ip=203.0.113.50 dst_port=443 protocol=TCP
      
**6. Does repeated communication automatically mean malicious activity? Explain briefly.**

      No. Repeated communication doesn't really mean malicious activity. One source IP communicates with an destination IP multiple times for different purposes, it maybe common.


## PART 3 — TRICKY INVESTIGATION SCENARIOS 

### SCENARIO 1:

A workstation repeatedly connects to the same external IP every 30 seconds using TCP port 4444. The application is marked UNKNOWN. 

**• Which workstation is involved?**

     device=WS-06

**• Which destination is involved?**

    dst_ip=198.51.100.200

**• What makes the pattern interesting?**

     The source IP is an private IP address and in each connection the application is marked UNKNOWN.

**• Can you confirm malicious activity?**

     No. By just seeing the log, we can't confirm malicious activity, we need additional context.

**• What additional evidence would you check?**

     i would check

     1. User / System associated with the Source and destination IP
     
     2. Location
     
     3. Time of the event
     
     4. Try to look into the unknown application


### SCENARIO 2: 

An external IP attempts connections to the same internal system on ports 22, 23, and 3389. All attempts are blocked. 

**• Which internal system is targeted?**

     device=FW-01
     
**• What pattern do you observe?**

     An external Ip tries to communicate with an internal IP via port 22, 23, 3389 after some failed attempts via 3389, after 30 minutes it tried via port 22, 23 but it also got blocked.

**• Were the connections successful?**

     No

**• Why could this still require investigation?**

     These blocked connections maybe an indicator of malicious activity, but they alone are not enough evidence to confirm a security attack


### SCENARIO 3:

A workstation repeatedly connects to an external destination on port 443. The application is SOFTWARE_UPDATE. 

**• Does repetition automatically make this suspicious?**

    No
    
**• What evidence suggests it may be expected activity?**

     This activity appears to be normal because the software update application is using HTTPS (port 443) to regularly check for updates from an external server.
     
**• What would you verify before closing the investigation?**

      I would confirm the server and application are legitimate and check for any unusual activity before closing the alert.


### SCENARIO 4: 

An internal system makes several DNS connections to the same external IP within a short period.

**• Identify the system and destination.**

      device=WS-07, 198.51.100.150

**• Why might this be normal?**

     This maybe normal because they are generated by a genuine application communicating with a trusted DNS server

**• What could make this pattern worth investigating further?**

       if the connections were too high, and more, targets unwanted domains and any unusual system activity happens.

## PART 4 — PRIORITIZATION 

1.

   **• What happened?**

      Four repeated inbound RDP connection attempts to TCP port 3389 were made and all were blocked by the firewall.
  
   **• Which systems or IPs are involved?**

        Source IP - 203.0.113.88
        Destination IP - 192.168.1.100

  **• Why would you prioritize it?**

        Repeated RDP attempts may indicate scanning or an attempted unauthorized remote-access attack, even though they were blocked.

  **• What additional information would you check first?**

     I would first check firewall and Windows/RDP logs for any successful connections or login attempts from the source IP.


2. 

   **• What happened?**

       WS-06 made five repeated outbound TCP connections to port 4444, and all were allowed by the firewall.

   **• Which systems or IPs are involved?**
   
         Source IP - 192.168.1.80
         Destination IP - 198.51.100.200 

   **• Why would you prioritize it?**

         Repeated outbound connections to an unknown application and unusual port 4444 could indicate suspicious or unauthorized communication.

   **• What additional information would you check first?**

         I would first identify the process/application on WS-06 responsible for the connections and check endpoint/security logs for related activity.

3. 

    **• What happened?**

         WS-07 made five repeated outbound DNS queries over UDP port 53, and all were allowed
    
    **• Which systems or IPs are involved?**

        Source IP - 192.168.1.90
        Destination IP - 198.51.100.150
   
   **• Why would you prioritize it?**

         DNS traffic is normally legitimate, but the repeated queries every 10 seconds could be unusual and may warrant checking for automated or suspicious activity.

   **• What additional information would you check first?**
   
            I would first check the actual DNS query domains and identify which process on WS-07 generated the requests.


   **I would first check firewall and Windows/RDP logs for any successful connections or login attempts from the source IP.**

         Highest priority because the connection is outbound, allowed, and the application is unknown. Repeated connections every 30 seconds could indicate suspicious or unauthorized communication.


## PART 5 — NORMAL OR REQUIRES INVESTIGATION 

**1. Identify three activities that appear normal based on available context.**

      1. 2026-09-01 09:10:30 device=WS-01 src_ip=192.168.1.25 src_port=51601 dst_ip=8.8.8.8 dst_port=53 protocol=UDP direction=OUTBOUND action=ALLOWED application=DNS
      2. 2026-09-01 09:19:02 device=WEB-SRV-01 src_ip=192.0.2.55 src_port=50501 dst_ip=10.0.0.10 dst_port=443 protocol=TCP direction=INBOUND action=ALLOWED application=HTTPS
      3. 2026-09-01 09:25:30 device=APP-SRV-02 src_ip=10.0.0.25 src_port=49800 dst_ip=10.0.0.50 dst_port=5432 protocol=TCP direction=INTERNAL action=ALLOWED application=DATABASE

**2. Identify three activities that require further investigation.**

     1. 2026-09-01 09:09:01 device=FW-01 src_ip=203.0.113.88 src_port=45670 dst_ip=192.168.1.100 dst_port=3389 protocol=TCP direction=INBOUND action=BLOCKED application=RDP
     2. 2026-09-01 09:14:05 device=WS-06 src_ip=192.168.1.80 src_port=51000 dst_ip=198.51.100.200 dst_port=4444 protocol=TCP direction=OUTBOUND action=ALLOWED application=UNKNOWN
     3. 2026-09-01 09:22:50 device=WS-07 src_ip=192.168.1.90 src_port=62014 dst_ip=198.51.100.150 dst_port=53 protocol=UDP direction=OUTBOUND action=ALLOWED application=DNS

**3. For each activity, explain why.**

    1. Repeated RDP attempts may indicate scanning or an attempted unauthorized remote-access attack, even though they were blocked.

    2. Repeated outbound connections to an unknown application and unusual port 4444 could indicate suspicious or unauthorized communication.

    3. DNS traffic is normally legitimate, but the repeated queries every 10 seconds could be unusual and may warrant checking for automated or suspicious activity

**4. Can any single network log entry alone confirm an attack? Explain briefly.**

      No. A single log entry can not define an attack. It may indicate an activity, we need further details to confirm it as an activity


## PART 6 — SHORT ANSWERS

**1. What does a source IP identify?**

    It identifies from where the communication starts.

**2. What does a destination IP identify?**

    It identifies where the communication starts.

**3. What does a destination port help identify?**

     A port is a numbered communication endpoint on a computer that helps identify which service or application network traffic should go to

**4. What does a protocol describe?**

     Protocols are rules that allow systems to communicate.
     Examples : TCP, UDP, SMTP

**5. What is outbound traffic?**

        Outbound traffic leaves a system or network.
        
**6. What is inbound traffic?**

      Inbound traffic comes toward a system or network.


**7. Does an allowed connection automatically mean it is safe?**

     No

**8. Does a blocked connection automatically mean an attacker was successful?**

     No.

**9. Why are repeated connection patterns important?**

     Repeated connections matter because they may indicate automated or persistent communication, especially when the destination or application is unknown.

**10. Why is context important during network investigation?**

      Context is important because it helps determine whether an activity is **normal, suspicious, or malicious** by comparing it with the system, user, time, and expected behavior.

## PART 7

**Short Summary**


      The main suspicious activity was repeated outbound connections from WS-06 (192.168.1.80) to 198.51.100.200 on TCP port 4444. The connections were allowed and happened every 30 seconds, while the application was listed as unknown, so this activity should be investigated. I would first check which process on WS-06 made the connections, review the endpoint logs, and investigate the destination. Based on the available logs alone, we cannot confirm that the activity was malicious.
