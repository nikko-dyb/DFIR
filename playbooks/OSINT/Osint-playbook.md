# Classification: Public

# OSINT Playbook: Investigative Scenarios & Workflows

## 📌 Preface
This playbook provides a structured approach to **Open Source Intelligence (OSINT)** investigations across different scenarios, ensuring thorough data collection, analysis, and reporting. It is designed for cybersecurity professionals, threat hunters, digital investigators, and SOC teams to conduct **efficient, ethical, and legally compliant** OSINT investigations.

## 📖 Table of Contents
1. Overview
2. General OSINT Workflow
3. Scenario 1: Investigating a Phishing Website
4. Scenario 2: Tracking a Threat Actor
5. Scenario 3: Identifying a Suspicious IP Address
6. Scenario 4: Social Media Intelligence (SOCMINT)
7. Scenario 5: Dark Web Monitoring
8. Post-Investigation Actions
9. Appendix

---

## 🔍 1. Overview
Open Source Intelligence (OSINT) is the process of **collecting, analyzing, and interpreting publicly available data** to gain insights into cyber threats, criminal activities, or potential security risks.

### **Key Objectives:**
- Collect actionable intelligence from open sources.
- Verify and validate information for accuracy.
- Ensure investigations comply with **legal and ethical standards**.
- Document findings in a structured, reportable manner.

---

## 🔄 2. General OSINT Workflow
1. **Define Objectives** – Clearly outline investigation goals.
2. **Data Collection** – Gather relevant intelligence from open sources.
3. **Data Analysis** – Filter, correlate, and validate information.
4. **Reporting** – Document findings and provide actionable insights.
5. **Operational Security (OPSEC)** – Ensure anonymity where needed.

---

## 📌 3. Scenario 1: Investigating a Phishing Website

### **Objective:** Identify if a reported domain is being used for phishing.

### **Workflow:**
1. **Collect Domain Information**
   - Use WHOIS lookup:
     ```bash
     whois phishing-site.com
     ```
   - Check DNS records:
     ```bash
     nslookup phishing-site.com
     ```
2. **Analyze Website Content**
   - Capture website snapshot using **URLScan.io**
   - Inspect website for login forms, fake branding.
3. **Check Reputation Services**
   - [PhishTank](https://www.phishtank.com/)
   - [OpenPhish](https://www.openphish.com/)
   - [Google Safe Browsing](https://transparencyreport.google.com/safe-browsing/search)
4. **Monitor IP and Hosting Infrastructure**
   - Reverse IP lookup with **Shodan**:
     ```bash
     shodan host <IP Address>
     ```
5. **Report & Document Findings**
   - Summarize findings with screenshots, evidence, and risk level.

---

## 📌 4. Scenario 2: Tracking a Threat Actor

### **Objective:** Identify online footprints of a cybercriminal or hacking group.

### **Workflow:**
1. **Identify Known Aliases & Usernames**
   - Use [Sherlock](https://github.com/sherlock-project/sherlock):
     ```bash
     python sherlock.py username
     ```
2. **Analyze Social Media Activity**
   - Search Twitter, Telegram, and Discord for handles.
   - Use [Maltego](https://www.maltego.com/) for entity mapping.
3. **Check Data Breaches & Leaks**
   - Query **Have I Been Pwned** for compromised accounts.
   - Search paste sites (Pastebin, Ghostbin) for email dumps.
4. **Dark Web Monitoring**
   - Look for mentions in darknet forums using **OnionSearch**.
5. **Report & Document Findings**
   - Collect and archive OSINT findings for future reference.

---

## 📌 5. Scenario 3: Identifying a Suspicious IP Address

### **Objective:** Determine if an IP is linked to malicious activity.

### **Workflow:**
1. **Check Reputation Databases**
   - [AbuseIPDB](https://www.abuseipdb.com/):
     ```bash
     curl https://api.abuseipdb.com/api/v2/check?ipAddress=192.168.1.1
     ```
2. **Perform Reverse Lookup**
   - Identify associated domains:
     ```bash
     nslookup 192.168.1.1
     ```
3. **Check Open Ports & Services**
   - Scan using **Shodan**:
     ```bash
     shodan host 192.168.1.1
     ```
4. **Investigate Connection Logs**
   - Cross-reference IP with firewall logs or SIEM alerts.
5. **Report & Document Findings**
   - Provide an intelligence report with risk rating.

---

## 📌 6. Scenario 4: Social Media Intelligence (SOCMINT)

### **Objective:** Gather intelligence from social media platforms.

### **Workflow:**
1. **Identify Target Profiles**
   - Use **IntelTechniques** tools for profile discovery.
2. **Extract Metadata**
   - Download images and check EXIF data:
     ```bash
     exiftool image.jpg
     ```
3. **Analyze Engagement & Connections**
   - Check retweets, followers, and network relationships.
4. **Check Dark Web Mentions**
   - Scan deep web forums for target usernames.
5. **Report & Document Findings**
   - Create a SOCMINT profile with observed patterns.

---

## 📌 7. Scenario 5: Dark Web Monitoring

### **Objective:** Track illicit activities on Tor-based marketplaces and forums.

### **Workflow:**
1. **Access Onion Services Anonymously**
   - Use **Tails OS** for secure browsing.
2. **Search for Threat Actor Mentions**
   - Use [Ahmia](https://ahmia.fi/) for indexed searches.
3. **Monitor Marketplaces & Leaks**
   - Collect dark web chatter related to stolen credentials or exploits.
4. **Check Cryptocurrency Transactions**
   - Track suspicious BTC wallets using **CipherTrace**.
5. **Report & Document Findings**
   - Archive evidence with proper handling procedures.

---

## 🔄 8. Post-Investigation Actions
- **Validate collected intelligence before acting.**
- **Follow chain of custody guidelines for evidence handling.**
- **Collaborate with law enforcement where required.**
- **Store findings in a secure repository for future reference.**

---

## 📖 9. Appendix
### **OSINT Tool Reference**
| **Tool** | **Purpose** | **Link** |
|---------|------------|----------|
| Sherlock | Username investigation | [GitHub](https://github.com/sherlock-project/sherlock) |
| Shodan | IP and open port scanning | [Shodan.io](https://www.shodan.io/) |
| Maltego | Link analysis & intelligence | [Maltego](https://www.maltego.com/) |
| URLScan.io | Website investigation | [URLScan.io](https://urlscan.io/) |

---

### 📖 Additional Resources
- [OSINT Framework](https://osintframework.com/)
- [IntelTechniques OSINT Tools](https://inteltechniques.com/tools/)
- [MITRE ATT&CK Intelligence Gathering](https://attack.mitre.org/)

---

## ✅ Summary
This playbook provides a structured OSINT methodology tailored for different investigative scenarios. By leveraging **trusted tools and workflows**, investigators can uncover valuable intelligence while maintaining ethical and legal compliance.

