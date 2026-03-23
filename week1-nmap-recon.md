# Week 1 - Nmap Reconnaissance 
## Target - Metasploiable2 
## Date: 23-03-2026

## Open Ports Found 
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  tcpwrapped
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 00:0C:29:96:08:6E (VMware)
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel


## Key Findings 
* 20+ ports are open, precisely 22 ports are open
*  Ports 21, 6667, and 1524 are the critical ports and can be easily vulnerable.
*  Port 23 is open, i.e., telnet, which gives password in plain text format.
*  Ports 139/445 (Samba 3.X): Highly vulnerable to CVE-2007-2447 (Username Map Script). 
Attackers can execute arbitrary shell commands by providing a specially crafted username during the login process.
*  Port 2049 (NFS): On Metasploitable 2, the NFS exports are usually misconfigured to allow "root squash" or wide-open access, meaning you can mount the entire / (root) filesystem remotely.
*  Database Vulnerabilities
Port  Service         Primary Vulnerability                       CVE 
3306   MySQL 5.0.51a   Remote Authentication Bypass               CVE-2012-2122
5432   PostgreSQL 8.3  Multiple Buffer Overflows / SQL Injection  CVE-2012-0868
*  Port 25 (SMTP): Postfix is generally secure, but it can be used for User Enumeration (VRFY command) to find valid system accounts.
*  Port 53 (BIND 9.4.2): Vulnerable to CVE-2008-0122, which can lead to a Denial of Service or potential cache poisoning.
*  Port 1099 (Java RMI): Often allows for RMI registry exploitation, leading to Remote Code Execution (RCE) via deserialization.
*  Port 5900 (VNC): Frequently uses the "VNC Null Authentication" flaw or weak passwords like password.

## Next Step 
* Exploiting the vulnerabilities that have critical risk factors, and high-risk factors like port 21 
