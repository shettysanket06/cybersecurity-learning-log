# From Normal ARP to MITM: Detecting ARP Spoofing with Wireshark

**Activity type:** Controlled home SOC lab / network traffic investigation  
**Author:** Sanket Shetty  
**Lab environment:** Isolated VMware environment  
**Original activity:** LinkedIn post shared by the author at https://lnkd.in/p/dn8J2eMF

> This write-up is based on the activity description supplied by the author. Add original screenshots or packet-capture evidence before treating it as a fully reproducible lab report. The exercise was described as taking place in an isolated, controlled VMware environment.

## 1. Objective

Establish a baseline for normal ARP behaviour, simulate ARP spoofing in an isolated lab, and use Wireshark and the Windows ARP cache to identify evidence of a possible Man-in-the-Middle (MITM) position.

The defensive focus is to understand how an unexpected change in an IP-to-MAC mapping can redirect Layer-2 traffic and how a network analyst can investigate that change.

## 2. Lab environment and tools

The original activity described the following setup:

- **Windows 11 VM:** endpoint used to observe ARP-cache changes and ICMP traffic.
- **Kali Linux VM:** controlled test system used to simulate ARP spoofing.
- **VMware NAT gateway:** gateway whose IP-to-MAC mapping was observed.
- **Wireshark:** packet capture and analysis on Windows and Kali.
- **arpspoof:** utility used for the controlled ARP-spoofing simulation.
- **Virtualisation:** VMware, with the exercise isolated from production networks.

The activity description identified the gateway IP as `192.168.198.2`. This is a private lab address and should be interpreted only in the context of the described VMware environment.

## 3. Methodology described

The exercise was performed in the following stages:

1. Establish a normal ARP baseline between the Windows 11 VM, Kali Linux VM and VMware NAT gateway.
2. Capture and record the legitimate IP-to-MAC mapping observed for the gateway.
3. In the isolated lab, simulate ARP spoofing from Kali Linux by sending forged ARP replies to the Windows VM and the gateway.
4. Inspect the Windows ARP cache and observe whether the gateway IP becomes associated with the Kali VM's MAC address.
5. Capture Windows network traffic in Wireshark and inspect the Ethernet destination MAC address for the test ICMP traffic.
6. Capture the corresponding traffic on Kali and check whether the same ICMP traffic is observed there before it is forwarded toward the gateway.
7. Review ARP packets for repeated replies, unexpected mapping changes and duplicate-IP indications.

> The exact commands, interface names, packet numbers, capture filters, VM configuration and screenshots were not included in the supplied activity description. Add those details from the original lab notes if available. Do not reconstruct or guess them.

## 4. Observations reported

The author reported the following gateway mapping before and after the simulation:

| State | Gateway IP | MAC address associated with the gateway IP |
|---|---|---|
| Normal baseline | `192.168.198.2` | `00:50:56:ED:2D:9E` |
| After spoofing | `192.168.198.2` | `00:0C:29:B1:3B:4F` (reported as the Kali VM's MAC) |

Additional observations reported in the activity:

- The Windows ARP cache changed so that the gateway IP was associated with the Kali VM's MAC address.
- Windows ICMP traffic was observed with the Kali VM's MAC address as the Ethernet destination.
- The same ICMP traffic was observed in Kali's Wireshark capture before being forwarded toward the gateway.
- Repeated ARP replies and duplicate-IP indications were observed during the simulation.

These values and observations are reproduced from the author's description. Packet-level screenshots or the original PCAP should be added to independently demonstrate each observation.

## 5. Technical interpretation

ARP is used on a local network to resolve an IPv4 address to a Layer-2 MAC address. Traditional ARP does not authenticate replies, so a host may update its ARP cache based on a forged or otherwise unexpected ARP reply.

In the described lab, the gateway's IP address remained the same while the MAC address associated with it changed to the Kali VM's MAC address. This is the key Layer-2 detail: the destination IP of the test traffic does not need to change for its next-hop Ethernet destination to be redirected.

If the attacker system is also forwarding traffic, packets can pass through that system on their way to the actual gateway. This creates a potential MITM position in the controlled scenario.

## 6. Defender's perspective

A SOC or network analyst investigating possible ARP spoofing can look for:

- Unexpected changes to the MAC address associated with a trusted IP, especially the default gateway.
- Unsolicited or unusually frequent ARP replies.
- One MAC address claiming multiple IP addresses in a way that is inconsistent with the network baseline.
- Duplicate-IP or conflicting ARP indications.
- Endpoint traffic whose Ethernet destination unexpectedly points to an unfamiliar host.
- Corroborating switch, endpoint, DHCP, network-access-control or network-monitoring logs, where available.

An individual ARP reply or a changed mapping is not, by itself, conclusive proof of malicious activity. Analysts should compare it with the known network topology, authorised changes and other evidence.

## 7. Limitations and evidence to add

This write-up is based on the author's LinkedIn activity text. To make it a stronger, independently reviewable technical report, add the following original artefacts if available:

- Screenshot of the normal ARP cache and gateway mapping.
- Screenshot showing the changed ARP cache entry after the simulation.
- Wireshark capture showing the relevant ARP replies and mapping change.
- Windows-side packet evidence showing the Ethernet destination MAC.
- Kali-side packet evidence showing the forwarded ICMP traffic.
- Relevant capture filters and packet numbers.
- A short lab topology diagram showing the Windows VM, Kali VM and VMware NAT gateway.

Before publishing screenshots or PCAP files, review them for personal information, hostnames, tokens and unrelated network details. The MAC addresses above were included in the original activity description; consider whether you want to retain or redact them in a public repository. Never include credentials or traffic from networks you do not own or have permission to inspect.

## 8. Key learning

This exercise connected ARP theory with packet-level behaviour. The important defensive lesson is that a MITM condition may be indicated by unexpected changes in normal network relationships—not merely by an obviously malicious command. Comparing an established IP-to-MAC baseline with current ARP observations can help identify suspicious redirection, while packet captures can provide evidence of where traffic is being sent.

## 9. Original activity

The activity description was supplied by the author and was originally shared on LinkedIn: https://lnkd.in/p/dn8J2eMF

## 10. Suggested interview discussion

Be prepared to explain:

1. What problem does ARP solve on an IPv4 local network?
2. Why can forged ARP replies change a host's ARP cache?
3. During this exercise, why did the gateway IP remain the same while the Ethernet destination MAC changed?
4. What packet-level evidence supports the conclusion that traffic was being sent through the Kali VM?
5. What is the difference between ARP spoofing and IP spoofing?
6. Which network controls or monitoring signals can help detect or reduce ARP spoofing?
7. Why should an analyst compare observations against a known network baseline before classifying an event as malicious?
