# Cybersecurity Learning Log

A collection of practical cybersecurity exercises and learning notes documented by Sanket Shetty.

The purpose of this repository is to preserve the methodology, tools, observations, limitations, and lessons from hands-on learning activities. Each write-up distinguishes the author's reported observations from interpretations and points that still need supporting evidence.

## Activities

| Activity | Focus | Tools | Status |
|---|---|---|---|
| [HTTP Traffic Investigation & Credential Visibility Analysis](01-http-traffic-investigation/README.md) | Inspecting HTTP requests, headers, form data, and plaintext exposure in a controlled lab | Wireshark, Kali Linux, Windows 11 VM, Python HTTP server | Write-up drafted from the author's LinkedIn activity; add original screenshots/PCAP if available |
| [Reconnaissance Detection & TCP SYN Scan Analysis](02-tcp-syn-scan-analysis/README.md) | Understanding TCP SYN scan traffic and firewall filtering | Nmap, Wireshark, Kali Linux, Windows 11 VM, VMware Workstation | Write-up drafted from the author's LinkedIn activity; add original screenshots/PCAP if available |
| [From Normal ARP to MITM: Detecting ARP Spoofing with Wireshark](03-arp-spoofing-detection/README.md) | Comparing normal and spoofed ARP mappings and analysing redirected traffic in an isolated lab | Wireshark, Kali Linux, Windows 11 VM, VMware, arpspoof | Write-up drafted from the activity description supplied by the author; add original screenshots/PCAP if available |

## Documentation standards

- Only describe actions that were actually performed.
- Distinguish packet/log observations from interpretations.
- Add original screenshots, packet numbers, filters and commands when available; do not invent missing evidence.
- Do not include credentials, tokens, personal information or unrelated sensitive network details.
- Do not upload third-party PCAPs or datasets unless their licence permits redistribution; link to the source when appropriate.
- Keep attack simulations limited to systems and networks owned by you or explicitly authorised for testing.
- These are controlled learning exercises, not evidence of professional SOC employment or production incident handling.

## Author

**Sanket Shetty** — BSc Information Technology student, developing practical skills in defensive security and SOC operations.

- GitHub: https://github.com/shettysanket06
- LinkedIn: https://www.linkedin.com/in/sanket-shetty-467008329
