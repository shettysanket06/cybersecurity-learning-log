# Reconnaissance Detection & TCP SYN Scan Analysis

**Activity type:** Controlled home SOC lab / network reconnaissance analysis  
**Author:** Sanket Shetty  
**Original LinkedIn post:** https://www.linkedin.com/posts/sanket-shetty-467008329_cybersecurity-socanalyst-wireshark-ugcPost-7459652166018838528-Bdax/

## 1. Objective

Simulate a TCP SYN scan in an isolated lab and examine how reconnaissance traffic appears in a packet capture. The aim was to understand scan behaviour, TCP handshake patterns, and how firewall filtering can affect the responses visible to an analyst.

## 2. Lab environment

The original activity described:

- **Scanning system:** Kali Linux
- **Target system:** Windows 11 VM
- **Scanning tool:** Nmap using `-sS` (TCP SYN scan)
- **Traffic analysis:** Wireshark
- **Virtualisation:** VMware Workstation

Only systems owned by the student or explicitly authorised for testing should be scanned.

## 3. Methodology

The activity followed this workflow:

1. Prepare the Kali Linux scanner and Windows 11 target VM in the home lab.
2. Capture the relevant network traffic in Wireshark.
3. Run a TCP SYN scan from Kali Linux against the Windows VM using Nmap's `-sS` scan option.
4. Inspect the resulting TCP packets, source and destination ports, and handshake behaviour.
5. Compare the packet-level evidence with Nmap's reported port states.

> Add the original command line, target address (sanitised if necessary), scan options, capture interface, Wireshark filters, and screenshots before treating this as a reproducible procedure. The accessible LinkedIn post did not provide all these details.

## 4. Observations reported in the original activity

- Repeated TCP SYN packets originated from the Kali Linux system.
- Destination ports changed during the scan.
- The capture showed incomplete TCP handshakes and no successful connection establishment for the reported probes.
- Wireshark displayed **Conversation completeness: Incomplete** for the relevant traffic.
- Nmap reported the scanned ports as `filtered`, with no visible SYN-ACK or RST response in the observed capture.
- The Windows system appeared to silently drop the packets, consistent with filtering by a host firewall.

## 5. Defensive interpretation

A sequence of connection attempts from one source to multiple destination ports can be a sign of network reconnaissance. In a SOC, analysts should correlate packet observations with endpoint and firewall logs, identify the source and target, establish whether the activity was authorised, and assess whether additional suspicious behaviour followed.

The absence of a SYN-ACK or RST in a capture is consistent with silent packet filtering, but the packet capture alone does not prove which control dropped the traffic. Firewall logs or additional host/network evidence would strengthen that conclusion.

## 6. Limitations and evidence needed

This write-up is based on the text of the original LinkedIn post. Add the following from the original lab if available:

- Sanitised screenshot of the Nmap output.
- Wireshark screenshot highlighting repeated SYN packets and relevant response behaviour.
- The exact Nmap command and scan scope.
- Relevant Wireshark filters and packet numbers.
- Firewall configuration or logs, if collected, to support the interpretation that the Windows firewall silently dropped the probes.

Do not scan public or third-party systems without explicit authorisation. Keep the lab isolated and document the authorised scope.

## 7. Key learning

The exercise helped demonstrate how TCP SYN scanning differs from a completed TCP connection, how incomplete handshakes may appear in packet captures, and why firewall filtering affects the evidence available to network defenders.

## 8. Original post

See the [LinkedIn activity](https://www.linkedin.com/posts/sanket-shetty-467008329_cybersecurity-socanalyst-wireshark-ugcPost-7459652166018838528-Bdax/).

## 9. Suggested interview discussion

Be prepared to explain:

1. What is a TCP SYN scan and how does it differ from a full TCP connect scan?
2. What packet sequence would you expect when a port is open, closed, or filtered?
3. What does Nmap's `filtered` state mean?
4. Why might a Wireshark conversation be marked incomplete?
5. What additional logs or evidence would help confirm that a host firewall dropped the probes?
