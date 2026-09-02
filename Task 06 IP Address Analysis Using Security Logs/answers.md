# **Task 06 - IP ADDRESS ANALYSIS USING SECURITY LOGS**

## PART 1 — IP ADDRESS ANALYSIS

### Review the complete log file and answer the following questions: 

**1. List all unique source IP addresses found in the log.**

     1. 192.168.1.25
     2. 192.168.1.30
     3. 10.0.0.15
     4. 198.51.100.24
     5. 203.0.113.50
     6. 192.168.1.42
     7. 10.0.0.32
     8. 198.51.100.77
     9. 10.0.0.12
     10. 10.0.0.30


**2. Identify which source IP addresses belong to private IP ranges.**

     1. 192.168.1.25
     2. 192.168.1.30
     3. 10.0.0.15
     4. 192.168.1.42
     5. 10.0.0.32
     6. 10.0.0.12
     7. 10.0.032

     
**3. Identify which source IP addresses are external/public based on the log data.**

     1. 198.51.100.24
     2. 203.0.113.53
     3. 198.51.100.77

**4. List all destination IP addresses that belong to private IP ranges.**

     1. 10.0.0.10
     2. 10.0.0.25
     3. 10.0.0.20
     4. 10.0.0.05
     5. 10.0.0.40
     6. 192.0.2.44

**5. Identify two examples of communication between internal systems.**

     1. source ip=192.168.1.25 destination ip=10.0.0.10 activity happened=login.
     2. source ip=10.0.0.15 destination ip=10.0.0.25 activity happened=login.

**6. Identify two examples where an internal system communicates with an external address.**

     1. source ip=192.168.1.30 destination ip=8.8.8.8 activity happened=dns query
     2. source ip=192.168.1.42 destination ip=93.184.216.34 activity happened=https request

     
## PART 2 — PATTERN IDENTIFICATION

**1. Which source IP address appears repeatedly during failed login attempts against the database server?**

     1. 203.0.113.50
 
 
**2. How many failed login attempts are shown for that activity?**

     1. 203.0.113.50  - 5 
     
**3. Which username is being targeted during those attempts?**

     1. 203.0.113.50 - admin
     
**4. Identify another source IP associated with repeated failed login attempts.**

    1. 198.51.100.77

**5. Which destination systems are involved in the repeated failed login activity?**

    1. 10.0.0.20 

**6. Do repeated failed logins automatically prove that an account was compromised? Explain briefly.**

    No. Repeated failed logins doesn't prove that an account was compromised, It maybe a genuine user mistake.

## PART 3 — TRICKY INVESTIGATION SCENARIOS

