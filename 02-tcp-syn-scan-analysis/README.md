# Reconnaissance Detection & TCP SYN Scan Analysis

**Activity type:** Controlled home SOC lab / network reconnaissance analysis  
**Author:** Sanket Shetty  
**Original LinkedIn post:** https://www.linkedin.com/posts/sanket-shetty-467008329_cybersecurity-socanalyst-wireshark-ugcPost-7459652166018838528-Bdax/

## 1. Objective

Run a TCP SYN scan in an isolated lab and examine how reconnaissance traffic appears in a packet capture. The investigation focuses on SYN probes, incomplete TCP conversations, and how filtered ports appear to a scanner.

## 2. Lab environment

The supplied screenshots show:

- **Scanning system:** Kali Linux
- **Target system:** Windows 11 VM
- **Scanning tool:** Nmap 7.98
- **Traffic analysis:** Wireshark
- **Virtualisation:** VMware Workstation

The visible addresses are scanner `192.168.56.10` and target `192.168.56.11`. Only systems owned by the student or explicitly authorised for testing should be scanned.

## 3. Methodology

The Nmap terminal screenshot shows this exact command:

```bash
nmap -sS 192.168.56.11
```

The Wireshark screenshot shows the display filter:

```
tcp.flags.syn==1
```

The visible packet list contains TCP SYN probes from `192.168.56.10` to `192.168.56.11`, including destination ports 111, 22, 8080, 443, 1025, 80, and 445. The selected packet is a SYN to destination port 443, and its TCP details show the SYN flag set and an incomplete conversation.

## 4. Observations

The Nmap output directly shows:

- Target: `192.168.56.11`
- Host reported as up, with approximately `0.0011s` latency.
- Nmap version: `7.98`.
- 1,000 TCP ports scanned.
- All 1,000 scanned ports reported as `filtered`, with no response.

The Wireshark screenshots show multiple outgoing SYN packets from `192.168.56.10` to `192.168.56.11` on different destination ports. The selected packet has the SYN flag set. Wireshark labels the selected conversation as incomplete.

## 5. Defensive interpretation

A sequence of connection attempts from one source to multiple destination ports can indicate network reconnaissance. In a SOC, analysts should identify the source and target, establish whether the activity was authorised, correlate packet observations with endpoint and firewall logs, and assess whether additional suspicious behaviour followed.

Nmap's `filtered` state and the absence of a response in the displayed evidence are consistent with silent filtering or another condition that prevented a response. The screenshots do **not** identify which firewall, network control, or failure caused the lack of response. Do not attribute the result specifically to Windows Defender Firewall without corroborating configuration or logs.

## 6. Evidence and limitations

| Evidence item | Status |
|---|---|
| Nmap terminal screenshot | Supplied and reviewed |
| Wireshark SYN-filter screenshot | Supplied and reviewed |
| Original PCAP/PCAPNG | Not retained |
| Full packet sequence | Cannot be independently re-examined |
| Exact packet numbers and complete response behaviour | Not established from the screenshots |
| Firewall configuration/logs | Not supplied |

The screenshots support the displayed Nmap result and selected SYN traffic. They do not provide a complete packet capture, so packet numbers and unshown response behaviour are not asserted.

## 7. Key learning

A TCP SYN scan sends connection-initiation probes without completing a normal TCP connection. Packet analysis can reveal repeated probes across destination ports, while scanner output summarises how the target's ports responded—or failed to respond. Analysts should distinguish a filtered result from proof of a specific firewall action.

## 8. Original post

See the [LinkedIn activity](https://www.linkedin.com/posts/sanket-shetty-467008329_cybersecurity-socanalyst-wireshark-ugcPost-7459652166018838528-Bdax/).

## 9. Suggested interview discussion

Be prepared to explain:

1. What is a TCP SYN scan and how does it differ from a full TCP connect scan?
2. What packet sequence would you expect when a port is open, closed, or filtered?
3. What does Nmap's `filtered` state mean?
4. Why might a Wireshark conversation be marked incomplete?
5. What additional logs or evidence would help confirm which control prevented a response?
