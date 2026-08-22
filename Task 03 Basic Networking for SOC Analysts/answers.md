# **Basic Networking for SOC Analyst**

## **SCENARIO 1 :**

Source IP: 192.168.1.15

Destination IP: 192.168.1.10

Destination Port: 22

Protocol: TCP


### Answer:

Source IP: 192.168.1.15

Destination IP: 192.168.1.10

Port: 22

Common Service: SSH

Protocol: TCP


## SCENARIO 2:##

Source IP: 192.168.1.25

Destination IP: 93.184.216.34

Destination Port: 443

Protocol: TCP

### Answer:

Source IP: 192.168.1.25

Destination IP: 93.184.216.34

Port: 443

Common Service: HTTPS

Protocol: TCP


## **SCENARIO 3:**

Source IP: 192.168.1.30

Destination IP: 8.8.8.8

Destination Port: 53

Protocol: UDP


### Answer:

Source IP: 192.168.1.30

Destination IP: 8.8.8.8

Port: 53

Common Service: DNS

Protocol: UDP


## SHORT SCENARIO

A SOC Analyst sees the following network activity:

Source IP: 192.168.1.50

Destination IP: 8.8.8.8

Destination Port: 53

Protocol: UDP


### Answer:

1. What service is commonly associated with port 53?
 
       DNS

3. Is this information alone enough to say that the activity is
   malicious?
   
       No.This information alone isn't enough to say that the activity is malicious.

5. Why or why not?
   
       No, because the port DNS is a server that translates the domain name into an ip address.
   
