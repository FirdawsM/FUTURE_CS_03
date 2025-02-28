# FUTURE_CS_03

## Incident Response Report: ARP Poisoning Attack

## 1. Root Cause Analysis
The attack occurred due to the vulnerability of the Address Resolution Protocol (ARP), which lacks authentication. This allowed an attacker to:

- Use Ettercap to scan the network and identify hosts.
- Perform ARP poisoning, tricking devices into associating the attacker's MAC address with a legitimate IP address (e.g., `192.168.100.1`).
- Capture sensitive data, such as login credentials, using Wireshark.

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


## 3. Supporting Evidence: `# FUTURE_CS_03`  

![alt text](image.png)
![alt text](image-1.png)
![alt text](image-2.png)
![alt text](image-3.png)

### Ensuring that Wireshark is running in the background 
![alt text](image-5.png)

### Opening Ettercap to simulate the attack then I went ahead an continued Scanning for hosts i got.Which are a total of 8 hosts.
![alt text](image-6.png)

### Setting `192.168.100.1` (`c8-84-cf-e9-7f-52`) as Target 1 
![alt text](image-7.png)

### Starting ARP poisoning
![alt text](image-8.png)

### The mac address is now changed from `c8-84-cf-e9-7f-52` to `08-00-27-38-c8-03`

![alt text](image-9.png)

### Capturing login details 
![alt text](image-10.png)

### Login credentials extracted  

![alt text](image-11.png)


### Ettercap analysis 

![alt text](image-12.png)

###  Wireshark capture  

![alt text](image-13.png)


## 4. Recommendations to Prevent Future Attacks
- Implement **Dynamic ARP Inspection (DAI)** on managed switches to verify ARP packets.  
- Use **static ARP entries** for essential systems to prevent ARP spoofing.  
- Enable **port security** on network switches to limit allowed MAC addresses.  
- Implement **network segmentation** to isolate critical systems.  
- Use **encrypted protocols** (HTTPS, SSH, VPN) to protect data from interception.  
- **Monitor network traffic** regularly using tools like Wireshark or IDS/IPS solutions.  