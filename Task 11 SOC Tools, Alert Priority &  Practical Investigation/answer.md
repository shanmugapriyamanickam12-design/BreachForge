# **SOC Tools, Alert Priority & Practical Triage**

## Task 1 — 

Identify the Security Tool For each source below, write what type of security tool it represents and what an SOC analyst can learn from it. 

**A. A platform collecting Windows, firewall, DNS and authentication logs in one searchable interface.**

       	SIEM 

**B. An endpoint security platform showing a suspicious process and its network connection.**

       	EDR

**C. A network security device showing an external connection blocked by a rule.**

        Firewall / Network Security Device

**D. A network detection system generating an alert for suspicious traffic.**

        	NIDS/NDR

## Task 2 — Assign Alert Priority

   A - P1
   
   B - P3
   
   C - P1
   
   D - P4
   
   E - P4
   
## Task 3 — Tricky Alert Investigation

**Scenario:** A SIEM generates a high-priority authentication alert. The logs show 12 failed login attempts against the admin account
from 203.0.113.50 within 5 minutes. Two minutes later, the same account successfully logs in from the same IP.
An EDR alert then shows a new PowerShell process on the server. 

**Answer the following:**

**1. What makes this activity suspicious?**

     12 failed admin logins followed by a successful login from the same external IP is suspicious.
     The new PowerShell process on the server makes it even more concerning.

**2. Which evidence should you check next?**

     1. Login/authentication logs
     
     2. PowerShell command and process details
     
     3. EDR activity
     
     4. Network/firewall connections
     
     5. Any other activity from the admin account
     
**3. Would you keep, increase, or decrease the alert priority? Explain.**

     I would increase to critical P1. The successful admin login plus PowerShell activity could mean the account or server has been compromised.

**4. Should this be escalated? Why?**

     Yes. It involves an admin account, a server, and possible unauthorized activity, so it needs immediate investigation.

**5. List at least three pieces of evidence you would record.**

      1. Source IP: 203.0.113.50
      
      2. Failed and successful login times
      
      3. Admin account involved

## Task 4 — Correlate the Evidence

Connect the following events into one timeline and explain whether they could be related:

09:10 — Firewall: outbound connection from SERVER-02 to an unfamiliar external IP. 

09:12 — SIEM: privileged account login to SERVER-02. 

09:14 — EDR: PowerShell process started on SERVER-02. 

09:15 — DNS: SERVER-02 resolves a newly observed domain.

09:18 — Firewall: second outbound connection to the same external IP.


    Yes. The events happen within minutes on the same server. The privileged login, PowerShell activity, and repeated external connection could indicate possible compromise or malware activity.
    Further investigation is needed to confirm.


## Task 5 — True Positive or False Positive? 

**1. IDS detects scanning traffic from an authorized vulnerability scanner used by the security team.**

    False Positive.
    
**2. EDR detects an unknown executable launched by a user, followed by an external connection.**

    True Positive

**3. SIEM detects one failed login from a user's normal workstation followed by a successful login.**

    False Positive

## Task 6 — Short SOC Questions 

**1. What is the purpose of a SIEM?**

       Collects and centralizes security logs so analysts can search events, correlate activity, investigate alerts, and build timelines.

**2. What is the difference between IDS and IPS?**

   **IDS** - Only detects suspicious activity.

   **IPS** - Detects and also prevents suspicious activity.

**3. What is EDR used for?**

     It  monitors endpoints like computers and servers to detect, investigate, and respond to threats.

**4. What is the difference between severity and priority?**

   **Severity** - shows how serious the threat is

   **Priority** - shows how urgently it should be handled.

**5. Why is correlation important during an investigation?**

       Because it is Connecting related events from different source, which helps analysts understands what happened.

**6. When should an alert be escalated?**

     Escalate when there is strong evidence of a real threat, active compromise, high-impact system involvement, or urgent risk.
