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

      affected accounts: employee01, employee02, employee03, hr01, admin, finance01

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


## PART 4 — INCIDENT INVESTIGATION CHALLENGE 

A source IP attempts access to multiple accounts, and one account later successfully logs in from the same source. 

**1. Which source IP is involved?**

     198.51.100.45

**2. Which accounts were targeted?**

     employee01, employee02, employee03, finance01, hr01, and admin.

**3. Which account later logged in successfully?**

      finance01

**4. Why is this sequence important?**

      This looks suspicious because the same IP tried logging into several different accounts and later successfully logged into one of them. This could indicate a password-spraying or credential attack.

**5. What would you investigate immediately?**

      Investigate the finance01 login, verify whether the source IP is authorized, and review what activity occurred during/after the successful session.
      
**6. Can you confirm account compromise based only on this log? Explain.**

        No. The log shows suspicious behavior and a successful login, but it does not prove that the attacker obtained or used stolen credentials. Additional evidence such as VPN/session logs, MFA records, endpoint activity, and account-owner confirmation would be needed


## PART 5 — PRIORITIZATION 

**Priority 1 — Multiple failed logins followed by a successful login**

1. The IP address 198.51.100.45 tried to log into several different accounts and failed each time. Later, it successfully logged into finance01.

3. finance01 — Source IP 198.51.100.45.
   
5. This is the most suspicious activity because the same IP tried multiple accounts and eventually got into one of them. It could be a password-spraying attack.
   
7. I would check VPN logs, MFA records, the user's login history, and what activity happened after the successful login.
   
**Priority 2 — Repeated failed attempts against the admin account**

1. The admin account had six failed login attempts from 203.0.113.88 within a short period. Later, there were two more failed attempts from the same IP.
   
2. admin — Source IP 203.0.113.88.
   
3. Repeated attempts against an administrator account could indicate a brute-force attack. If the attacker had succeeded, the impact could be serious.
   
4. I would check authentication logs, VPN logs, whether the IP is known or trusted, and whether there were any successful logins from the same source.

**Priority 3 — Failed logins followed by a successful login for Alice**

1. alice had three failed login attempts on WS-03 and then successfully logged in shortly afterward.

2. Account and source: alice — Source IP 192.168.1.30.

3. It could simply be Alice entering the wrong password a few times, but the quick success afterward makes it worth checking.

4. I would check Alice's normal login activity, endpoint logs from WS-03, MFA records, and confirm whether Alice was actually using the computer at that time.


## PART 6 — NORMAL VS REQUIRES INVESTIGATION

### Activities That May Be Normal

**1. John’s successful login**

 John logged in successfully from 192.168.1.25.
This looks normal because it was an internal login and there were no unusual login attempts around it.

**2. Developer01 logging in and out**

developer01 logged in successfully and logged out shortly afterward.
This could just be a normal work session, so there is nothing obviously suspicious about it.

**3. Contractor01’s VPN login**

contractor01 successfully logged into the VPN from 203.0.113.150.
This may be normal if the contractor was expected to work remotely at that time. I would only check further if the login was unexpected.

### Activities That Require Further Investigation

**1. Finance01’s successful login**

The IP 198.51.100.45 tried several different accounts and later successfully logged into finance01.
This stands out because it could be a password-spraying attempt. I would check the VPN logs, MFA records, and what finance01 did after logging in.

**2. Repeated attempts against the admin account**

The IP 203.0.113.88 tried to log into admin several times and failed.
The number of attempts in a short period makes this look like possible brute-force activity. I would check if there were any successful logins from this IP and whether it is a known or trusted source.

**3.Alice’s failed attempts followed by a successful login**

Alice had three failed login attempts and then successfully logged in shortly afterward.
This could simply mean she entered the wrong password a few times, so it is not automatically malicious. However, I would check the login and endpoint records to make sure the successful login was really Alice.

## PART 7 — SHORT ANSWERS 

**1. What is authentication?**

     Authentication is the process of verifying the identity of user before allowing access.
     
**2. What does a failed login mean?**

      A failed login refers that someone tried to login to the account and got denied

**3. What does a successful login mean?**

      It means the the authentication was accepted.

**4. What information can a source IP provide?**

      It provides information such as where the login/event is originated.

**5. What is a possible brute-force pattern?**

     A possible brute-force pattern may involve many attempts against one account. 
     
**6. What is a possible password spraying pattern?**

     A possible password spraying pattern may involve a small number of attempts against many accounts from the same source.
     
**7. Why can a successful login after failures be important?**

     A successful login after several failures may be legitimate or may require investigation. We need additional context to confirm whether ot was an attack or not.
     
**8. Does an unfamiliar source IP automatically mean an attack?**

      No. It may need investigation but it does not automatically mean that it was an attack. There maybe an legitimate reason.
      
**9. Why are privileged account events important?**

      Accounts with greater permissions deserve additional attention because unauthorized access could have a larger impact.

**10. Why is context important during authentication investigations?**

      Context is important because it helps us understand whether a login is normal or suspicious by looking at the user, IP, time, and surrounding activity.


## PART 8 - FINAL INVESTIGATION SUMMARY

The main activity that needs attention came from 198.51.100.45. This IP tried to log into several accounts, including employee01, employee02, employee03, finance01, hr01, and admin. Most attempts failed, but later the same IP successfully logged into finance01. This pattern looks suspicious and could be a password-spraying attack, so it should be investigated further. I would check VPN logs, MFA records, login history, and what activity happened after the successful login. However, based only on this log, we cannot confirm that the finance01 account was compromised.
