# **Introduction to Security Logs**

## SCENARIO 1

Time:09:10:15

User: Priya 

Source IP: 192.168.1.45 

Action: Login 

Status: Successful 

## Answer: 

Time:09:10:15

User: Priya

Source IP:  192.168.1.45 

Action: Login

Status: Successful

## SCENARIO 2 

Time: 10:07:13 

User: Priya 

Source IP: 192.168.1.45

Action: Login 

Status: Failed 

### Answer: 

Time: 10:07:13

User: Priya

Source IP: 192.168.1.45

Action: Login

Status: Failed


## SCENARIO 3 

Time: 10:08:02 

User: Priya 

Source IP: 10.10.10.25

Action: Login

Status: Failed 

### Answer:

Time:  10:08:02

User: Priya

Source IP: 10.10.10.25

Action: Login

Status: Failed

## SHORT SCENARIO 

A SOC Analyst sees the following activity:

09:15:22 — Rahul — Login — Failed 

09:15:40 — Rahul — Login — Failed 

09:16:03 — Rahul — Login — Successful 

### Answer the following: 

**1. What looks unusual about this activity?**

     After two failed login attempts, Rahul successfully logged in.

**2. What information would you want to check?**

     I would check whether it is a genuine user mistake(forgot password) and check whether any malicious activities happened after the login.

**3. Does this information alone prove that the account was compromised? Why or why not?**

     No. It maybe a user mistake (forgot password). To prove that the account was compromised we need more additional information.
     
