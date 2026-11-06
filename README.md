# Cybersecurity Learning Log

A portfolio of hands-on cybersecurity exercises and technical investigation notes by Sanket Shetty.

This repository documents the investigation process: scope, environment, commands and filters visible in retained evidence, observations, analysis, defensive relevance, and limitations. It is intended to demonstrate developing practical skills in network traffic analysis and security investigation—not professional SOC employment or production incident handling.

## Investigations

| Investigation | Focus | Tools | Retained evidence | Report |
|---|---|---|---:|---|
| HTTP Traffic Investigation | Cleartext HTTP request and form-data visibility | Wireshark, Kali Linux, Windows 11 VM, Python HTTP server | 1 screenshot; original PCAP not retained | [Open report](01-http-traffic-investigation/README.md) · [View evidence](01-http-traffic-investigation/evidence/) |
| TCP SYN Scan Analysis | Nmap SYN scan behaviour and filtered port results | Nmap 7.98, Wireshark, Kali Linux, Windows 11 VM, VMware | 2 screenshots; original PCAP/PCAPNG not retained | [Open report](02-tcp-syn-scan-analysis/README.md) · [View evidence](02-tcp-syn-scan-analysis/evidence/) |
| ARP Cache Poisoning Investigation | Gateway IP-to-MAC mapping changes and related ARP/ICMP traffic | Wireshark, Windows ARP cache, Kali Linux, VMware | 5 screenshots; original PCAP/PCAPNG not retained | [Open report](03-arp-spoofing-detection/README.md) · [View evidence](03-arp-spoofing-detection/evidence/) |

## Evidence and interpretation standard

- Screenshots are retained as visual evidence; they are not substitutes for original PCAP/PCAPNG files.
- The original packet captures were not retained for these exercises. Complete packet sequences, packet numbers, timestamps, and unshown protocol details therefore cannot be independently re-examined.
- Each report separates details visible in screenshots from context reported by the author and from technical interpretation.
- A finding is not stronger than its evidence. For example, a filtered Nmap result does not identify the specific filtering control, and a changed ARP mapping alone does not prove a complete, bidirectional MITM session.
- Dummy HTTP form values in the retained screenshot were confirmed by the author as synthetic lab credentials. Never reuse real credentials in demonstrations or publish screenshots containing secrets.
- Exact commands, filters, addresses, and values are included only where visible in retained evidence or confirmed by the author.

## Safe and responsible lab use

- Perform scanning and attack simulations only on systems and networks you own or are explicitly authorised to test.
- Keep lab exercises isolated from production and third-party networks.
- Review screenshots and captures for credentials, tokens, personal information, hostnames, and unrelated network details before publishing.
- Do not redistribute third-party PCAPs or datasets unless their licence permits it.

## Author

**Sanket Shetty** — BSc Information Technology student building practical skills in defensive security and SOC operations.

- GitHub: https://github.com/shettysanket06
- LinkedIn: https://www.linkedin.com/in/sanket-shetty-467008329
