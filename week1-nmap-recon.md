# Week 1 — Nmap Reconnaissance

## Target
Metasploitable2 (VMware)

## Date
[today's date]

## Tool
Nmap 7.98 on Kali Linux

## Summary
- Total open ports: 22
- OS detected: Linux 2.6.9 - 2.6.33
- Risk breakdown: 6 Critical · 9 High · 5 Medium · 2 Low

---

## Open Ports — Risk Rated

| Port | Service | Version | Risk |
|------|---------|---------|------|
| 21 | FTP | vsftpd 2.3.4 | CRITICAL |
| 23 | Telnet | Linux telnetd | CRITICAL |
| 512 | rexecd | netkit-rsh | CRITICAL |
| 513 | rlogind | OpenBSD rlogind | CRITICAL |
| 1524 | bindshell | Metasploitable root shell | CRITICAL |
| 6667 | IRC | UnrealIRCd | CRITICAL |
| 22 | SSH | OpenSSH 4.7p1 | HIGH |
| 25 | SMTP | Postfix smtpd | HIGH |
| 80 | HTTP | Apache 2.2.8 | HIGH |
| 139 | NetBIOS | Samba 3.X-4.X | HIGH |
| 445 | NetBIOS | Samba 3.X-4.X | HIGH |
| 2121 | FTP | ProFTPD 1.3.1 | HIGH |
| 3306 | MySQL | 5.0.51a | HIGH |
| 5432 | PostgreSQL | 8.3.0 | HIGH |
| 5900 | VNC | protocol 3.3 | HIGH |
| 8180 | HTTP | Apache Tomcat 1.1 | HIGH |
| 53 | DNS | ISC BIND 9.4.2 | MEDIUM |
| 111 | rpcbind | RPC #100000 | MEDIUM |
| 2049 | NFS | RPC #100003 | MEDIUM |
| 1099 | Java RMI | grmiregistry | MEDIUM |
| 6000 | X11 | access denied | MEDIUM |
| 8009 | AJP | Apache Jserv 1.3 | LOW |

---

## Key Findings

1. **vsftpd 2.3.4** — CVE-2011-2523 backdoor confirmed
2. **Port 1524** — Pre-installed root shell (bindshell) — verified via netcat, whoami returned root
3. **UnrealIRCd** — CVE-2010-2075 backdoor present
4. **Telnet on port 23** — Credentials transmitted in plain text
5. **Legacy services open** — rexecd (512), rlogind (513) with no encryption
6. **Two databases exposed publicly** — MySQL 3306, PostgreSQL 5432
7. **22 open ports** — Extremely poor security hygiene

---

## Next Steps

- Exploit vsftpd 2.3.4 backdoor using Metasploit (Week 2)
- Exploit UnrealIRCd backdoor using Metasploit (Week 2)
- Capture Telnet credentials using Wireshark (Day 4)
- Test MySQL with default blank root password (Week 2)
- Attack Apache web application via Burp Suite (Week 3)
- Run Nmap --script vuln scan for CVE confirmation (Day 3)
