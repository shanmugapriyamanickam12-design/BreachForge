# **DNS Activity Investigation**

## PART 1 — DNS LOG UNDERSTANDING 

**1. List the unique source IP addresses found in the logs.**

       1. 192.168.1.25 
       2. 192.168.1.30
       3. 192.168.1.40
       4. 192.168.1.45
       5. 192.168.1.50
       6. 192.168.1.55
       7. 192.168.1.60
       8. 192.168.1.70
       9. 192.168.1.80
       10. 192.168.1.90
       11. 192.168.1.100
       12. 192.168.1.110
       13. 192.168.1.120
       14. 192.168.1.130
       15. 192.168.1.140
       16. 192.168.1.150
       17. 192.168.1.160
       18. 192.168.1.35
       
**2. Identify all unique domains queried.**

          1. www.example.com
        2.update.example-software.test
        3. mail.example.org
        4. cdn.example.net
        5. cloud-sync.example
        6. portal.internal.example
        7. printer-office.example
        8. typo-example-site.test
        9. api.business-app.example
        10. tracking-service.example
        11. very-long-random-looking-subdomain-8f3k2x7m9q.data-service.example
        12. software-update.example
        13. login-verification.example
        14. unknown-service.example
        15. new-service-not-seen-before.example
        16. backup-cloud.example
        17. cloud-storage.example
        18. telemetry.example
        
**3. List the DNS record types found.**

        1. A
        2. AAAA
        3.MX
        4.CNAME

**4. Identify the different response statuses.**

        NOERROR, NXDOMAIN, and SERVFAIL

**5. Which systems made the highest number of DNS requests?**

      WS 13 -5

**6. Identify successful DNS queries.**

      

**7. Identify failed DNS queries.**

     1. typo-example-site.test
     2. unknown-service.example
     
**8. Which domains resolved to an IP address?**

      www.example.com, update.example-software.test, cdn.example.net, cloud-sync.example, portal.internal.example, printer-office.example,
      api.business-app.example, tracking-service.example, very-long-random-looking-subdomain-8f3k2x7m9q.data-service.example, software-update.example, 
      login-verification.example, new-service-not-seen-before.example, cloud-storage.example, and telemetry.example

## PART 2 — REPEATED ACTIVITY ANALYSIS.

**1. Identify a system repeatedly querying the same domain.**

     cloud-sync.example - WS-05
     tracking-service.example - WS-10
     software-update.example - WS-12
     login-verification.example - WS-13
     telemetry.example - WS-18

**2. Identify any domain queried several times within a short period.**

      login-verification.example - WS-13

**3. Identify any repeated failed DNS requests.**

      typo-example-site.test - WS-08
      unknown-service.example - WS-14

**4. Does repeated activity automatically mean malicious behavior?Explain your answer.**

      No.  can be completely normal because applications, browsers, updates, and services may request information repeatedly.

**5. Which repeated pattern appears normal based on the available context?**

      cloud-sync.example - WS-05

**6. Which repeated pattern requires additional investigation?**

      WS-11 repeatedly querying the very-long-random-looking-subdomain-8f3k2x7m9q.data-service.example every 20 seconds is the pattern I would investigate first.


## PART 3 — TRICKY SCENARIOS 

### SCENARIO 1 — REPEATED UNKNOWN DOMAIN 

A workstation repeatedly queries an unfamiliar domain at regular intervals.

**• Which system is involved?**

    WS-11 - 192.168.1.90
    
**• Which domain is queried?**

     very-long-random-looking-subdomain-8f3k2x7m9q.data-service.example
     
**• What pattern do you observe?**

     The domain was queried 3 times at 20-second intervals.

**• Can you confirm that the domain is malicious?**

    No. The available log alone does not confirm malicious activity.

**• What additional information would you investigate?**

    I would check,

    1. the DNS requests
    2. DNS query history
    3. endpoint activity
    4. whether the domain is associated with a legitimate application


### SCENARIO 2 — FAILED DNS REQUESTS

A system repeatedly receives failed responses while querying a domain.

**• Which system is involved?**

    WS-08 - 192.168.1.60
    
**• Which domain was requested?**

    typo-example-site.test

**• What response status appears?**

    NXDOMAIN

**• Give two possible non-malicious reasons for this activity.**

    1. The user may have typed the domain incorrectly.
    2. The domain may simply not exist.

**• When could repeated failures become more interesting to investigate?**

    If the failures continue frequently or involve many random-looking/unusual domains, it could indicate automated or suspicious DNS activity.


### SCENARIO 3 — LONG DOMAIN NAME 

A workstation queries a long and unusual-looking domain name.

**• Which system made the request?**

    WS-11 - 192.168.1.90
    
**• Why might the domain attract attention?**

     It is unusually long and contains a random-looking string, which can sometimes be associated with automated or DNS-tunneling activity.

**• Does its unusual appearance prove malicious activity?**

      No. An unusual-looking domain does not by itself prove malicious activity.
      
**• What evidence would you check before making a decision?**

      Check the responsible process, DNS query history, endpoint activity, domain reputation, and network connections to the resolved IP.


### SCENARIO 4 — NORMAL ACTIVITY THAT LOOKS UNUSUAL 

Identify one activity that initially looks unusual but may have a legitimate explanation based on the available information. Explain your reasoning.

     **Activity:** WS-05 repeatedly queries cloud-sync.example every 30 seconds.
     **Reasoning:** It may look unusual because of the repeated requests, but the domain name suggests a cloud-sync service, so the activity could be normal application behavior

### PART 4 — DOMAIN INVESTIGATION PRIORITY

1. Priority 1 — very-long-random-looking-subdomain-8f3k2x7m9q.data-service.example

  **• Which system queried it?**

     WS-11 - 192.168.1.90

  **• What pattern did you observe?**

       Queried 3 times every 20 seconds.
       
  **• Why did you assign that priority?**

      The domain is very long and random-looking, which can be suspicious.
      
  **• What would you investigate next?**

       Check the process making the requests and review WS-11 network activity.
       
2. login-verification.example


  **• Which system queried it?**

       WS-13 - 192.168.1.110

  **• What pattern did you observe?**

       Queried 5 times every 10 seconds.

  **• Why did you assign that priority?**

       It was queried very frequently in a short period.
       
  **• What would you investigate next?**

       Check which application generated the requests and what the domain is used for.
       
3. Priority 3 — unknown-service.example

   **• Which system queried it?**

      WS-14 - 192.168.1.120

  **• What pattern did you observe?**

      Queried 3 times and received SERVFAIL

  **• Why did you assign that priority?**

      The unknown domain repeatedly failed to resolve.

  **• What would you investigate next?**

       Check the application responsible and investigate why the DNS requests are failing.


## PART 5 — NORMAL VS REQUIRES INVESTIGATION

### **NORMAL OR EXPECTED ACTIVITY**

    1. WS-01 → www.example.com — Normal web DNS lookup; it successfully resolved with NOERROR.
    
    2. WS-03 → mail.example.org — Normal mail-related DNS lookup using an MX record.
    
    3.WS-05 → cloud-sync.example — Repeated queries every 30 seconds may be normal for a cloud-sync application.
    
### **REQUIRES FURTHER INVESTIGATION**

    1. WS-11 → long random-looking domain — The unusual domain name and repeated queries every 20 seconds could indicate automated activity.
    
    2. WS-13 → login-verification.example — Five queries within 40 seconds is unusually frequent and should be checked.
    
    3. WS-14 → unknown-service.example — The unknown domain repeatedly returned SERVFAIL, so the reason for the repeated requests should be investigated.

## PART 6 — CONNECT THE EVIDENCE

A SOC analyst often compares multiple sources of information. For each scenario below, explain what additional log source could help. 

**1. A suspicious domain resolves to an external IP address.**

      Check firewall/proxy logs to see what connection was made to that IP.
      
**2. A system repeatedly queries an unknown domain.**

     Check endpoint/EDR logs to identify which application or process is making the requests.

**3. DNS requests suddenly increase from one workstation.**

     Check DNS server logs and endpoint logs to understand what is causing the increase.

**4. A DNS query is followed by an unusual outbound network connection.**

     Check firewall and EDR logs to connect the DNS request with the process and network connection.


## PART 7 — SHORT ANSWERS

**1. What does DNS stand for?**

      Domain Name System
      
**2. What is the purpose of DNS?**

       To convert the human readable domain names into IP addresses.
       
**3. What is a DNS query?**

       A request asking for information about a domain.
       
**4. What is a DNS response?**

        The answer returned by the DNS server.
       
**5. What does an A record provide?**

       Provides an IPv4 address for a domain.

**6. What does an MX record relate to?**

      Identifies the mail server responsible for a domain.

**7. What does NOERROR generally indicate?**

       Generally means the DNS query was successful.

**8. Does a failed DNS request automatically indicate an attack?**

       No. It does not automatically indicate an attack.

**9. Why are repeated DNS patterns important?**

     They can reveal normal automated activity or suspicious behavior.

**10. Why should analysts investigate context before reaching a conclusion?**

     Analysts need context to distinguish legitimate activity from potentially malicious activity.


## PART 8 — SOC INVESTIGATION SUMMARY

The main activity I noticed was WS-11 (192.168.1.90) repeatedly querying the long, random-looking domain very-long-random-looking-subdomain-8f3k2x7m9q.data-service.example every 20 seconds. This needs further checking because the domain looks unusual. 
I would check the process making the requests and the system’s network activity. Based on the log alone, I cannot confirm that it is malicious.






  
