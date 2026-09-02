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

**1. A VPN login for the user amit is successful, followed later by one failed login and then another successful login from the same source IP. Does this automatically indicate an attack? Explain your reasoning.**

     No. It won't automatically indicate an attack. The user may mistyped the password or mistakenly typed any other password. It maybe a genuine user mistake.

**2. The user admin has multiple failed login attempts from an external source IP. Later, the admin account successfully logs in from a different private IP address. Can you conclude that the external source successfully accessed the account? Why or why not?**

     No. We cannot conclude that the external source successfully accessed the account since there is no records that says that the external IP login was a success. Later the account logs in from the internal IP only, it maybe the employee who owns the account. 

**3. A system makes DNS queries to public IP addresses. Does communication with a public IP address automatically make the activity suspicious? Explain.**

     No. DNS is a protocol which is used to convert a domain name into an IP address and also communicating with an public IP address doesn't mean it was an suspicious activity.

**4. One user successfully accesses a file server from a private IP address. What additional information would you need before deciding whether this activity is suspicious?**

    1. What is the source IP and Destination IP address?
    2. Which file was accessed?
    3. Which user is in control with the system associated with the destination Ip?
    4. From where the file was accessed(location)?
    5. Which information does the file contains?

**5. Which event in the log would you prioritize for further investigation first? Explain why.**

   1. source ip=203.0.113.50 destination ip=10.0.0.20

     This event has 5 continuous failed login attempts and no successful login afterwards.

## PART 4 — INVESTIGATION QUESTIONS

**1. Identify two activities that appear normal based on the available context.**

    1. src_ip=192.168.1.25 dst_ip=10.0.0.10 activity happened=login
    2. src_ip=10.0.0.15 dst_ip=10.0.0.25 activity happened=login

 **2. Identify two activities that require further investigation.**
 
       1. src_ip=203.0.113.50 dst_ip=10.0.0.20 action=login
       2. src_ip=198.51.100.77 dst_ip=10.0.0.10 action=login
 
 **3. For each activity requiring investigation, explain what makes it interesting or unusual.**
 
        1. src_ip=203.0.113.50 dst_ip=10.0.0.20 action=login
        2. src_ip=198.51.100.77 dst_ip=10.0.0.10 action=login

        These two activities have multiple failed login attempts.
 
**4. What additional information would you check before confirming malicious activity?**

      1. Source and Destination IP addresses
      2. User associated with that account
      3. Whether it was successful afterwards
      4. Location of source IP

**5. Why is context more important than looking at an IP address alone?**

      Context gives brief information about the event such as:

      • What activity occurred? 
      • Which user was involved? 
      • When did it happen? 
      • Which system was affected? 
      • Has similar activity occurred before?

      Because seeing the IP address alone doesn't confirm anything.

## PART 5 — SHORT ANSWERS 

**1. What does a source IP represent?**

     An address used to communicate and identify a device/system in a network.
    
**2. What does a destination IP represent?**

     It is the address where the communication ends.

**3. Is 192.168.1.25 a public or private IP address?**

      Private IP address.

**4. Is 10.0.0.15 a public or private IP address?**

      Private IP address.

**5. Which field in a log helps identify when an event occurred?**

     Action, Context helps identify when an event occurred.

**6. Which field identifies whether an authentication attempt succeeded or failed?**

    Action field

**7. Can an IP address alone confirm that an attack occurred?**

    No. An IP address alone can't confirm that an attack occured.

**8. What is one reason repeated failed logins may require investigation?**

    It maybe an possible attack or the user could forgot his password.


## PART 6 — INVESTIGATION SUMMARY

  The log contains many events that occurred in an organisation. These contains events such as login, logout, dns_query, vpn login. There are two suspicious activities which involves multiple failed login attempts. However we can't immediately say that was an security incident, we have investigate further about that cases (user=admin src_ip=203.0.113.50 dst_ip=10.0.0.20, user=root src_ip=198.51.100.77 dst_ip=10.0.0.10 ).
