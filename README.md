# Task-1-Basic-Network-Scanning-with-Nmap-OIBSIP
Nmap Scan Report – 10.181.99.206

Scan Date: 03 December 2025
Scanner: Nmap 7.98
Scan Type: -sS -sV -p- -A -v (Full TCP SYN scan, service/version detection, OS detection, script scan)
Target: 10.181.99.206
Host Status: Up (0.00065s latency)
Operating System: Linux Kernel 2.6.9 – 2.6.33
MAC Address: Oracle VirtualBox virtual NIC (08:00:27:B9:CE:18)

1. Executive Summary

The target system (10.181.99.206) exposes 30 open TCP services, many of which are outdated and known to contain critical vulnerabilities, including:

Anonymous FTP access (vsftpd 2.3.4) — known backdoor exploit.

Open Telnet (unencrypted remote login).

Samba 3.0.20 — vulnerable to RCE (e.g., CVE-2007-2447).

Multiple databases exposed (MySQL, PostgreSQL).

Default Tomcat, Apache, UnrealIRCd versions with known exploits.

Open VNC (no encryption).

Metasploitable bindshell on port 1524.

The system appears to be intentionally insecure, similar to a Metasploitable2 environment.

Risk level: Critical

2. Open Ports & Service Summary
High-Risk Services
Port	Service	Version	Notes
21/tcp	FTP	vsftpd 2.3.4	Anonymous login enabled; version has known backdoor vulnerability.
22/tcp	SSH	OpenSSH 4.7p1	Outdated; may contain privilege escalation issues.
23/tcp	Telnet	Linux telnetd	Unencrypted login; severe security risk.
25/tcp	SMTP	Postfix smtpd	VRFY enabled; potential for user enumeration.
139/445	SMB	Samba 3.0.20	Vulnerable to RCE (e.g., "username map script" exploit).
1524	Bindshell	Metasploitable Root Shell	Direct root shell access.
Web & Application Services
Port	Service	Version	Notes
80/tcp	HTTP	Apache/2.2.8	Outdated Apache; default Metasploitable page.
8180/tcp	HTTP	Apache Tomcat 5.5	Unpatched, default configuration weaknesses likely.
8009/tcp	AJP13	Apache JServ Protocol	Version known to be abused in "Ghostcat" type vulnerabilities.
Database Services
Port	Service	Version	Notes
3306/tcp	MySQL	5.0.51a	Very outdated, vulnerable to multiple exploits.
5432/tcp	PostgreSQL	8.3.x	End-of-life version.
RMI / RPC / Others
Port	Service	Version	Notes
1099	Java RMI	GNU Classpath	Often insecure by default; RCE possible.
2049	NFS	2–4	May allow unauthenticated file access.
3632	distccd	v1	Known for remote code execution vulnerabilities.
5900	VNC	VNC 3.3	No encryption; brute-forceable.
6667 / 6697	IRC	UnrealIRCd 3.2.8.1	Known backdoor vulnerability (CVE-2010-2075).
Various High Ports	RPC services	mountd, status, nlockmgr	Exposed RPC services that can leak info or allow access to NFS shares.
3. OS & Host Information

Device Type: General-purpose Linux host

OS Guess: Linux Kernel 2.6.9 – 2.6.33

NetBIOS Name: METASPLOITABLE

Workgroup: WORKGROUP

Domain: localdomain

Time Skew: +1 second from scanner

This confirms the system strongly resembles a Metasploitable2 training VM.

4. Vulnerability Analysis (Summary)
Critical Vulnerabilities Identified

vsftpd 2.3.4 Backdoor (port 21)

Samba 3.0.20 RCE (port 445)

Telnet (port 23) — Cleartext credential exposure

Unauthenticated MySQL access possible depending on config

distccd RCE (port 3632)

UnrealIRCd Backdoor (port 6667/6697)

NFS exports may allow remote file access

VNC without encryption (port 5900)

Metasploitable default bindshell (port 1524)

Outdated Apache, Tomcat, PostgreSQL with known CVEs

Risk Exposure: System is fully compromise-ready.

5. Recommendations
Immediate Actions

Remove or isolate the host from any production network.

Disable high-risk services immediately: Telnet, FTP, SMB, distccd, RMI, IRC, bindshell.

Restrict access via a firewall to required ports only (SSH/HTTPS).

Hardening Recommendations

Upgrade or replace outdated software (Apache, Samba, PostgreSQL, MySQL, Tomcat, SSH).

Disable anonymous FTP login.

Use SSH instead of Telnet.

Disable RPC/NFS services unless required.

Implement strong authentication and encryption for VNC.

Regularly apply OS and service patches.

Network Security Enhancements

Deploy IDS/IPS monitoring.

Enforce network segmentation.

Implement centralized logging and auditing.

6. Conclusion

The scan reveals that host 10.181.99.206 is running an extremely vulnerable software stack, typical of a penetration-testing training environment. Almost every open service is outdated and potentially exploitable.

The system must be considered highly compromised or compromise-ready and should not be used in any production environment.
