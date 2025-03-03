# Analyzing DNS Log Files Using Splunk SIEM
<p align="center">
<img src="https://i.imgur.com/uer6djf.png" height="80%" width="80%" alt="Splunk SIEM Lab"/> 
</p>


## Introduction
DNS (Domain Name System) logs are crucial for understanding network activity and identifying potential security threats. In this project, we use **Splunk SIEM (Security Information and Event Management)** to analyze DNS logs, aiming to detect anomalies or malicious activities within network traffic.

## Prerequisites
Before you begin, ensure you have:

1. A **Splunk instance** installed and configured.
2. Sample DNS log data to upload and analyze in Splunk.

## Project Steps

### Part 1: Uploading Sample DNS Log Files to Splunk SIEM

1. **Prepare Sample DNS Log Files**
   - Obtain a sample DNS log file in a supported format (e.g., text or CSV).
   - Ensure the log file includes relevant fields, such as:
     - Source IP
     - Destination IP
     - Domain name
     - Query type
     - Response code
   - Save this file in a location accessible by the Splunk instance.

2. **Upload Log Files to Splunk**
   - Log in to the Splunk web interface.
   - Go to **Settings > Add Data**.
   - Choose **Upload** as the data input method.
   -![Screenshot 2024-11-03 211127](https://github.com/user-attachments/assets/33720665-95ce-46a9-88e3-a01e38888838)

   -![Screenshot 2024-11-03 211315](https://github.com/user-attachments/assets/38e04d61-c086-4b8f-8a40-c150f5d04227)
   
   -![Screenshot 2024-11-03 211340](https://github.com/user-attachments/assets/8c05ee91-a22b-435f-b49d-5ced4f211e5b)
   
   -![Screenshot 2024-11-03 211407](https://github.com/user-attachments/assets/630de7dc-889d-49b1-8d68-30f13815ed94)





### Part 2: Analyzing DNS Log Files in Splunk SIEM

1. **Search for DNS Events and apply special filter such as "src_ip", "dest_ip, "record_type","FQDN" **
   -![Screenshot 2024-11-03 211730](https://github.com/user-attachments/assets/093c0572-1f82-495e-bff5-d9dba4aa6048)

   -![Screenshot 2024-11-03 212049](https://github.com/user-attachments/assets/3ee6c039-a146-4607-a82a-3b5ced104593)
   
   -![Screenshot 2024-11-03 212446](https://github.com/user-attachments/assets/f82c3f27-17a5-4303-8f2c-749c87ab0836)
   
   -![Screenshot 2024-11-03 211944](https://github.com/user-attachments/assets/f2216f58-7520-488a-a4f2-48b0942bb3ec)
   
   -![Screenshot 2024-11-03 214235](https://github.com/user-attachments/assets/9ae91f03-ed1c-40a6-b9ec-afa2f951bf68)




   

     ```

3. **Extract Relevant Fields**
   - Use regular expressions or field extractions to identify fields like source IP, destination IP, domain name, query type, and response code.
   - Example regex-based field extraction:
     ```spl
     index=dns_logs sourcetype=dns_sample | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
     
    -![Screenshot 2024-11-03 213439](https://github.com/user-attachments/assets/88a209e3-143b-473b-8562-ea859abf2f7d)


4. **Identify Anomalies in DNS Activity**
   - To detect unusual patterns, such as spikes or anomalies, run the following query:
     ```spl
     index=dns_logs sourcetype=dns_sample | stats count by fqdn
    -![Screenshot 2024-11-03 213630](https://github.com/user-attachments/assets/2f598155-7e08-4d53-bf77-63ad9194b266)

    -![Screenshot 2024-11-03 213904](https://github.com/user-attachments/assets/6fb3359a-f252-4ec8-96f7-b44dc3addb8f)

    -![Screenshot 2024-11-03 214333](https://github.com/user-attachments/assets/9fc2c033-aa6b-494d-9fd2-1190ebe91e21)

     ```

5. **Identify Top DNS Sources**
   - Use the `top` command to list the most common Fully Qualified Domain Names (FQDNs) and source IPs:
     ```spl
     index=dns_logs sourcetype=dns_sample | top fqdn, src_ip

    -![Screenshot 2024-11-03 214429](https://github.com/user-attachments/assets/d8c21f3b-880d-4341-be96-705a68ee3bfe)
     
    -![Screenshot 2024-11-03 215453](https://github.com/user-attachments/assets/6e482d6c-c371-4fa3-a64a-3bfecba8383e)


     ```

 Conclusion-
This Splunk project demonstrates how to upload and analyze DNS log files, focusing on identifying anomalies and top sources in network activity. DNS log analysis is an essential part of monitoring network security and detecting potential threats.
