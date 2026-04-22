# 🔐 Network Enumeration & Vulnerability Assessment using Nmap
## Target: Metasploitable 2 (Vulnerable Lab Machine)

---

## 📌 Introduction

Network enumeration is a critical phase in penetration testing used to identify open ports, running services, and potential vulnerabilities within a target system.

In this lab, Nmap (Network Mapper) was used to perform structured scanning and service enumeration on Metasploitable 2, an intentionally vulnerable machine, within a controlled environment.

---

## 🎯 Objectives

- Perform network scanning using Nmap
- Identify open ports and running services
- Detect service versions
- Use Nmap Scripting Engine (NSE) for enumeration
- Identify misconfigurations and security risks

---

## 🧪 Lab Environment

- Attacker Machine: Kali Linux (VMware)
- Target Machine: Metasploitable 2 (VMware)
  
<img width="797" height="385" alt="metasploitable2_ip" src="https://github.com/user-attachments/assets/cc5470dc-70d1-428a-88e6-1d6e8c59a662" />

- Network Type: Host-only / NAT (Isolated Lab)
- Tool Used: Nmap

---

## 🛠️ Methodology

The assessment was performed in structured steps:

1. Initial service and port scanning  
2. Targeted enumeration using NSE scripts  
3. Analysis of discovered services and vulnerabilities  

---

## 🔍 Scanning & Enumeration

### Basic Service Scan

Command: nmap -sC -sV <target-ip>

# Screenshot Nmap Main Scan

<img width="1550" height="766" alt="sc_sv_command" src="https://github.com/user-attachments/assets/560929da-2e94-4a19-84b4-b28c52b513d5" />

<img width="1317" height="775" alt="sc_sv3" src="https://github.com/user-attachments/assets/fac0a614-9d41-4f4b-8676-c0e9513c890b" />

<img width="1662" height="776" alt="sc_sv2" src="https://github.com/user-attachments/assets/195ed2e3-b81f-41a3-9105-01542ecd865a" />


Purpose:
- Detect open ports
- Identify running services
- Retrieve service versions

Findings:
- Multiple open ports identified:
  - 21/tcp (FTP)
  - 22/tcp (SSH)
  - 23/tcp (Telnet)
  - 25/tcp (SMTP)
  - 80/tcp (HTTP)

Analysis:
The presence of multiple exposed services increases the attack surface. Several services appear outdated and may contain known vulnerabilities.

---

### FTP Enumeration

Command: nmap -p21 --script ftp-anon <target-ip>

Purpose:
- Check if anonymous FTP login is allowed

Finding:
- Anonymous FTP login enabled

Security Impact:
- Allows unauthorized access without credentials
- Indicates improper access control configuration
- May expose sensitive files

---

<img width="966" height="655" alt="ftp_ _http_enum" src="https://github.com/user-attachments/assets/cadb42da-df8c-4f5f-bbad-eadedc414c3e" />


### HTTP Enumeration

Command: nmap -p80 --script http-enum <target-ip>


Purpose:
- Discover directories and web resources

Finding:
- Multiple accessible endpoints identified

Se
curity Impact:
- Hidden or exposed directories can provide entry points for attacks
- May reveal sensitive application structure

---

### HTTP Header Analysis

Command: nmap -p80 --script http-headers <target-ip>

<img width="823" height="396" alt="http_header" src="https://github.com/user-attachments/assets/e5ab6872-e4cb-4ce3-9845-36e40ea86c62" />


Purpose:
- Retrieve HTTP response headers

Finding:
- Server information disclosure observed

Security Impact:
- Exposes underlying technologies
- Can assist attackers in targeting known vulnerabilities

---

## ⚠️ Identified Security Issues

- Anonymous FTP access enabled (High Risk)
- Multiple open ports increasing attack surface (Medium Risk)
- Outdated services potentially vulnerable (High Risk)
- Information disclosure via HTTP headers (Medium Risk)

---

## 🧠 Key Learnings

- Enumeration is the foundation of penetration testing
- Misconfigurations are often easier to exploit than complex vulnerabilities
- Nmap’s scripting engine provides powerful automation capabilities
- Structured analysis is more important than running multiple commands

---



## ⚠️ Disclaimer

This lab was conducted in a controlled environment using intentionally vulnerable systems. No unauthorized systems were targeted.

---

## 🚀 Future Work

- Exploitation of identified vulnerabilities
- Integration with SIEM tools for monitoring
- Automation of scanning and reporting
