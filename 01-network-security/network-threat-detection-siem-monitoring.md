# Network Threat Detection and SIEM Monitoring

**Project type:** Practical cybersecurity laboratory  
**Reported lab period:** 27 July – 3 August 2026  
**Environment:** Kali Linux, Ubuntu, VMware virtual machines, and Wazuh  
**Status:** Practical work reported; supporting screenshots and selected figures still require review

## 1. Objective

To practise basic network discovery, service identification, traffic observation, authentication-event investigation, and centralized security-event monitoring.

## 2. Scope and lab environment

The work was carried out in a controlled virtual lab using Kali Linux as the testing system and Ubuntu as the monitored system. Wazuh was used to review security events generated in the lab.

Host addresses and network identifiers are intentionally omitted from this public report.

## 3. Activities performed

### 3.1 Network discovery

A host-discovery scan was run against the lab network:

```bash
sudo nmap -sn <LAB_SUBNET>
```

The report recorded five discovered hosts. This was a discovery exercise; it did not establish that every discovered host was vulnerable.

### 3.2 Service identification

A service/version scan was run against the Ubuntu lab host:

```bash
sudo nmap -sV <UBUNTU_LAB_HOST> -Pn
```

The recorded scan identified SSH (22), HTTP (80), and HTTPS (443) as open on the target at the time of testing. These results describe the lab host during that scan and should not be treated as a statement about its current state.

### 3.3 Local service review

The Ubuntu host's listening services were reviewed with:

```bash
ss -tulnp
```

The report noted local-only database and service listeners, including MongoDB, PostgreSQL, and CUPS bound to the loopback interface. A loopback-bound service is not directly exposed to other network hosts through that listener.

### 3.4 Network traffic observation

ICMP traffic was observed with tcpdump. The exercise included observing echo requests and replies.

The TCP connection process was also examined, including the three-way handshake used to establish a TCP connection. HTTP and HTTPS traffic were compared to understand the difference between plaintext application data and encrypted transport sessions.

### 3.5 Scan and authentication-event investigation

The lab included observation of TCP SYN scan activity and review of failed SSH authentication attempts on Ubuntu. Authentication logs were examined in:

```bash
/var/log/auth.log
```

The report recorded repeated failed authentication attempts originating from the Kali lab system. An exact attempt count is omitted from this public version because the supplied report drafts contain different totals that have not yet been reconciled.

### 3.6 Wazuh event review

Wazuh was used to review security events associated with the lab activity. The supplied report recorded events under several rule IDs, including:

- **5710** and **5760** — SSH authentication-related events in the reported investigation.
- **5502, 5501, 5402, 19011, 533, and 502** — additional events recorded in the Wazuh report.

The event counts and complete alert context should be checked against original dashboard or log evidence before being published as definitive statistics.

## 4. Key learning outcomes

- Network discovery and service/version scans provide different kinds of information.
- Listening interfaces matter: a service bound only to loopback is not equivalent to one listening on a network interface.
- Packet capture helps explain ICMP exchanges and TCP connection establishment.
- Repeated authentication failures can be investigated through operating-system logs.
- SIEM rules help organize and identify events, but an alert should be interpreted in context rather than treated as proof of a successful attack.

## 5. Limitations and evidence status

- The original reports contain inconsistent failed-login totals; no exact total is claimed here.
- Sanitized screenshots and complete command outputs have not yet been attached to this portfolio entry.
- Wazuh rule IDs are included as reported, but their exact event meanings and counts should be confirmed against the original alert details.
- The exercise was performed in a controlled learning environment. It does not claim exploitation of the target or compromise of a real system.

## 6. Responsible-use statement

All scanning and authentication-testing activities described in this report were intended for the user's isolated, authorized virtual laboratory. Similar techniques should only be used on systems for which explicit permission has been granted.

## 7. Evidence to add

When available, add sanitized evidence for:

1. Nmap host-discovery and service-scan output.
2. The Ubuntu listening-service review.
3. A representative tcpdump capture.
4. Relevant failed-authentication log entries with host identifiers removed.
5. Wazuh alert details showing the relevant rule IDs and event context.

Do not publish passwords, tokens, personal information, public IP addresses, or identifying network details.
