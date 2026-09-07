# **Authentication and Account Activity Investigation**

## PART 1 — BASIC LOG ANALYSIS

**1. List the usernames found in the log.**

      1. John
      2. Alice
      3. Admin
      4. Employee01
      5. Employee02
      6. Employee03
      7. finance01
      8. hr01
      9. contractor01
      10. service_backup
      11. intern01
      12. developer01

**2. Identify successful login events.**

      1. hostname=WS-01 username=john source_ip=192.168.1.25
      2. hostname=WS-02 username=alice source_ip=192.168.1.30
      3. hostname=WS-03 username=alice source_ip=192.168.1.30 
      4. hostname=VPN-GW username=contractor01 source_ip=203.0.113.150
      5. hostname=WS-04 username=service_backup source_ip=10.0.0.25
      6. hostname=WS-05 username=john source_ip=192.168.1.25
      7. 2026-09-03 09:25:00 hostname=VPN-GW username=admin source_ip=192.168.1.200 
      8. hostname=VPN-GW username=finance01 source_ip=198.51.100.45
      9. hostname=WS-07 username=developer01 source_ip=192.168.1.75
      

**3. Identify failed login events.**

       1. hostname=VPN-GW username=admin source_ip=203.0.113.88
       2. hostname=VPN-GW username=employee01 source_ip=198.51.100.45
       3. hostname=VPN-GW username=employee02 source_ip=198.51.100.45
       4. hostname=VPN-GW username=employee03 source_ip=198.51.100.45
       5. hostname=VPN-GW username=finance01 source_ip=198.51.100.45
       6. hostname=VPN-GW username=hr01 source_ip=198.51.100.45
       7. hostname=VPN-GW username=admin source_ip=198.51.100.45
       8. hostname=WS-03 username=alice source_ip=192.168.1.30
       9. hostname=WS-05 username=john source_ip=192.168.1.25
       10. hostname=WS-06 username=intern01 source_ip=192.168.1.90

**4. List the unique source IP addresses.**

       1. 192.168.1.25 
       2. 192.168.1.30
       3. 203.0.113.88
       4. 198.51.100.45
       5. 203.0.113.150
       6. 10.0.0.25
       7. 192.168.1.200
       8. 192.168.1.90
       9. 192.168.1.75

**5. Which account has the highest number of failed attempts?**

       1. Admin
       
**6. Which source IP generated the highest number of failed attempts?**

         1. 203.0.113.88
         2. 198.51.100.45


## PART 2 — PATTERN DETECTION 

**1. Identify a possible brute-force pattern.**

       hostname=VPN-GW username=admin source_ip=203.0.113.88

       Tried to login 5 times and failed within a short period.

**2. Identify a possible password spraying pattern.**

        198.51.100.45

        Account Targeted : employee01, employee02, employee03, finance01, hr01, admin
      
**3. Identify a successful login after multiple failed attempts.**

        hostname=WS-03 username=alice source_ip=192.168.1.30

**4. Identify a successful login that follows a wider suspicious pattern.**

         hostname=VPN-GW username=finance01 source_ip=198.51.100.45

**5. Which accounts are affected by the same external source IP?**

        1. 203.0.113.88 - admin
        2. 198.51.100.45 - employee01, employee02, employee03, finance01, hr01, admin
        3. 203.0.113.150 - contractor01
        
**6. Explain why patterns are more useful than reviewing one event alone.**

       A single failed login can be normal, like entering the wrong password. But when we look at repeated attempts,
       the same IP, and multiple accounts, we can spot suspicious patterns like brute force or password spraying.
       Patterns help us understand the bigger picture instead of judging one event alone.


# PART 3 — TRICKY SCENARIOS 

## SCENARIO 1 — REPEATED FAILURES AGAINST ONE ACCOUNT 

**Identify the account and source IP.**

      203.0.113.88

**What pattern do you observe?**

      6 failed login attempts within about 1 minute, all targeting the same account.

**Can you confirm an attack?**

      No. It looks suspicious and could be brute force, but the log alone isn’t enough to confirm an attack.

**What would you check next?**

      Check whether the IP is known, review more login history, and look for any successful login after the failures.


## SCENARIO 2 — MANY ACCOUNTS, ONE SOURCE 

**Identify the source IP and affected accounts.**

      198.51.100.45

      *affected accounts:* employee01, employee02, employee03, hr01, admin, finance01

**Why is this pattern different from repeated attempts against one account?**

      One IP is trying many accounts, which looks more like password spraying than brute force against a single account.


## SCENARIO 3 — SUCCESS AFTER FAILURES 

**Identify the account.**

      Alice
      
**Give two possible explanations and describe what evidence you would check.**

       1. Alice entered the wrong password a few times, then entered the correct one.
       2. Someone may have been trying to guess her password and eventually succeeded.

       I would check the source IP, login location/device, previous login history, and whether there were other suspicious attempts around the same time.

## SCENARIO 4 — UNUSUAL BUT NOT CONFIRMED 

**Identify one login that looks unusual but cannot be confirmed as malicious using only the log.**

      hostname=VPN-GW username=admin source_ip=192.168.1.200

      It is an admin login from a different internal IP.
      It looks unusual, but the log alone cannot confirm it as malicious.


