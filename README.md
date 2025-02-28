# FUTURE_CS_03

## Incident Response Report: ARP Poisoning Attack

### 🔍 **Overview**
This project focuses on **analyzing and responding to an ARP poisoning attack** as part of a **simulated cybersecurity incident response exercise**. The goal was to **understand how ARP spoofing works, analyze its impact, and implement security measures to prevent such attacks**.

As an **ethical hacking and blue team exercise**, I **simulated an attack using Ettercap and Wireshark**, then **acted as an incident responder** to detect and mitigate the attack.

---

## 1. Root Cause Analysis
The attack occurred due to the vulnerability of the Address Resolution Protocol (ARP), which lacks authentication. This allowed an attacker to:

- Use Ettercap to scan the network and identify hosts.
- Perform ARP poisoning, tricking devices into associating the attacker's MAC address with a legitimate IP address (e.g., `192.168.100.1`).
- Capture sensitive data, such as login credentials, using Wireshark.

---

## 2. Steps to Mitigate the Incident
To stop an ongoing ARP poisoning attack:

1. **Identify the malicious MAC address:**  
   - Use `arp -a` (Windows) or `arp -n` (Linux) to check the ARP table for anomalies.  
   - Compare against known device MAC addresses.

2. **Clear the poisoned ARP cache:**  
   - Windows:  
     ```sh
     netsh interface ip delete arpcache
     ```
   - Linux/macOS:  
     ```sh
     sudo ip -s -s neigh flush all
     ```

3. **Restart affected devices** to refresh the ARP cache.  

4. **Enable static ARP entries** for critical devices (e.g., gateways, DNS servers).  

5. **Use packet filtering and intrusion detection:**  
   - Deploy ARP monitoring tools such as Arpwatch or XArp.  
   - Configure firewalls to block suspicious ARP requests.  

---

### 3. Lessons Learnt

## Network Security Enhancements
- Implement Dynamic ARP Inspection (DAI) on managed switches.  
- Enable port security to restrict allowed MAC addresses.  
- Use encrypted communication protocols (HTTPS, SSH, VPN) to mitigate data interception risks.  

## Monitoring and Response
- Deploy intrusion detection systems (IDS) to monitor ARP spoofing activities.  
- Conduct periodic network traffic analysis with Wireshark or similar tools.  

## User Awareness
- Educate employees on ARP spoofing risks and safe network practices.  
- Encourage the use of secure authentication methods, such as multi-factor authentication (MFA).  
 

---

###  **Note:**  
📌 This was a **controlled, ethical cybersecurity exercise** conducted for learning purposes. The **goal was to simulate an attack, analyze it, and implement defensive measures as an incident responder**.

---
