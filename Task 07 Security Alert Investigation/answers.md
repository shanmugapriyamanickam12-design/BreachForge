# **Security Alert Investigation**

## PROBLEM 1 — ADMIN LOGIN ALERT

**1. Which user account triggered the alert?**

     Admin account

**2. Which source IP generated the failed attempts?**

     203.0.113.45

**3. How many failed login attempts occurred?**

     4

**4. Was there a successful login after the failures?**

      Yes, but not from from the same source IP.

**5. Was the successful login from the same IP address?** 

     No.
     
**6. Does the available evidence confirm that the external IP successfully accessed the admin account?**

    No. We need additional information.
    
**7. Would you consider this activity suspicious? Why?**

    This event is suspicious, because there were four failed login attempts followed by a successful login which is also from a different source IP.
    
**8. What would you investigate next?**

     I would investigate the person authorized with admin account, location of the source IP( the failed and successful).

## PROBLEM 2 — REPEATED LOGIN ALERT 

**1. How many failed login attempts occurred before the successful login?**

    3

**2. What source IP was involved?**

    192.168.1.50 

**3. Was the successful login from the same source IP?**

    Yes.

**4. What additional event appears after the successful login?**

     Password Reset

**5. Based on the available context, does this look more like suspicious activity or a possible normal user issue?**

     It looks like a possible user issue.

**6. Explain your reasoning in your own words.**

     The user(sarah) has three failed login attempts followed by a successful login with the same source IP address which is also a private IP address. After that the user has changed her password, it may indicate that the user may forgot their password. Hence it can be a genuine user mistake but we've also need to investigate additional information.
     
**7. What additional information could help confirm your conclusion?**

      I would investigate

        1. User (sarah)
        2. Location of the source IP
        3. Activities happened after password change


# PROBLEM 3 — HIGH PRIORITY 

**1. Which user account is involved?**

    Finance

**2. Which source IP generated the activity?**

     198.51.100.77

**3. How many failed login attempts occurred?**

      5

**4. Did a successful login occur from the same source IP?**

      Yes. After 5 failed attempts, the successful one was occurred from the same IP address.

**5. What file was downloaded after the successful login?**

     payroll_2026.xlsx

**6. Why should this activity receive further investigation?**

     Because based on only the failed login attempts, we can't decide whether it was an attack or not.

**7. What additional information would you check immediately?**

      I would check with the user, activity happened after the login, which location the source IP came from

**8. Can you confirm malicious activity based only on these logs? Explain why or why not.**

       Because based on only the failed login attempts and the file download we can't decide whether it was an attack or not. We need additional information to confirm this as a malicious activity

## FINAL ANALYSIS

**1. Which alert would you prioritize first as an L1 SOC Analyst?**

     I would prefer Problem 1 - ADMIN LOGIN ALERT

**2. Why would you prioritize it?**

     Because it involves an public IP address which tries to log into the Admin account  

**3. Which problem may represent a possible false positive or normal activity?** 

       Problem 2 — REPEATED LOGIN ALERT 

**4. Why is context important when investigating a security alert?**

        Based on the three incidents, they can be a genuine user mistake such as forgotten password, but it can also be a an unauthorized person who is trying to gain access, by investigating only we can confirm.
 

**5. Write a short conclusion for each of the three problems.**

    1.  PROBLEM 1 — ADMIN LOGIN ALERT

                  In this the admin account has 4 failed login attempts with a public IP address followed by a successful login attempt from a different private IP address. 

    2. PROBLEM 2 — REPEATED LOGIN ALERT 

                  In this the user account(sarah) has three failed login attempts followed by a successful attempt from the same private address. After that the user has changed the password. It maybe a genuine user issue as they can possibly forgot their password and changed their password.

    3. PROBLEM 3 — HIGH PRIORITY 

                  In this the finance account has 5 failed login attempts followed by a successful login attempt from the same IP address. After that they have downloaded a payroll file.

     Each of them can be a false positive or a possible security incident. We need addition context to confirm these events as false positives or incidents.

## SHORT QUESTIONS

**1. What is the difference between an event and an alert?**

    **Event :** It is an activity that happened inside the organisation
    **Alert :** It is possible incident that need to be investigated

**2. Does every alert mean an attack has happened?**

      No. Every alert doesn't mean an attack has happened.

**3. What is a true positive?**

      True positive means that the alert means that an attack had happened.

**4. What is a false positive?**

    False positive means that the alert was not an attack.

**5. Why should a SOC Analyst review related logs before making a conclusion?**  

     Because the alert can be a genuine user mistake or an attack, to confirm that we need to review the related logs, information.
