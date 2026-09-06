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
     15. 1192.168.1.110
     16. 192.168.1.120
     
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
      3. 

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
            
            3. device=FW-01 src_ip=1192.168.1.110 - dst_ip=192.168.1.100
            
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



            
