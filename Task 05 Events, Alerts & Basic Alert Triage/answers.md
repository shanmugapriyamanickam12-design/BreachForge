# **Task 05-Events, Alerts & Basic Alert Triage**

## Scenario 1 :

A user successfully logs in to their company account during normal working hours.

**1. Is this an event, alert, or incident?**

   It is an Event.
   
**2. Why?**

   Logging into their company account as an employee during the working hours is completely normal.

 ## Scenario 2 :

 A security system detects 15 failed login attempts for the same user account within two minutes.
 
**1. Is this an event, alert, or incident?**

   This maybe an incident.
   
**2. What information should an L1 analyst check?**

   An L1 Analyst should check further information such as;
   
     1. Account they are logging into
     2. Whether it was success or not after the 15 failed attempts
     3. From where they are trying to login.
     4. Source and destination IP addresses
   

   
**3. Would you immediately call this a confirmed attack? Why?**

  No. I would not call this as a confirmed attack. Because the user may forgot his password (a genuine user mistake).

  ## Scenario 3 :

  An analyst investigates suspicious login activity and confirms that an unauthorized person accessed the employee's
account.

**1. Is this an event, alert, or incident?**

    It is an incident.
    
**2. Why?**

   In this scenario , it was confirmed that an unauthorized person accessed the employee's account.

## SHORT SCENARIO — BASIC ALERT TRIAGE

Alert:

User: Rahul

Source IP: 203.0.113.50

Failed Login Attempts: 15

Time: 2 minutes

### Answer the following:

**1. What happened?**

   An alert was generated because a user tried to login to the account multiple times(15) within a short period of time.
   
**2. What information would you check first?**

    I will check with the user whether he was the one who is logging into, location of the source IP address and the status of the login attempt (whether it was successful or not after the attempts.

**3. Is there enough information to confirm an incident?**

  No. It was an alert, we need further information to confirm that it was an incident.


 
