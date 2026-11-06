# Cybersecurity Learning Log

A collection of practical cybersecurity exercises and learning notes documented by Sanket Shetty.

The purpose of this repository is to preserve the methodology, tools, observations, limitations, and lessons from hands-on learning activities. Each write-up distinguishes directly visible evidence from reported activity and technical interpretation.

## Activities

| Activity | Focus | Evidence reviewed | Evidence status |
|---|---|---:|---|
| [HTTP Traffic Investigation & Credential Visibility Analysis](01-http-traffic-investigation/README.md) | Inspecting HTTP requests, headers, form data, and plaintext exposure in a controlled lab | 1 screenshot | Screenshot reviewed; original PCAP not retained |
| [Reconnaissance Detection & TCP SYN Scan Analysis](02-tcp-syn-scan-analysis/README.md) | Understanding TCP SYN scan traffic and filtered port responses | 2 screenshots | Screenshots reviewed; original PCAP/PCAPNG not retained |
| [ARP Cache Poisoning Investigation](03-arp-spoofing-detection/README.md) | Comparing ARP mappings and examining related ARP/ICMP traffic in an isolated lab | 5 screenshots | Screenshots reviewed; original PCAP/PCAPNG not retained |

> **Evidence note:** The screenshots supplied for these exercises have been reviewed and their visible details are documented in the reports. The original packet-capture files were not retained. Do not treat screenshots as a substitute for a complete PCAP/PCAPNG or infer packet details that are not visible. The screenshots still need to be added to the repository's evidence folders before the repository can claim that the image files are publicly available here.

## Documentation standards

- Only describe actions that were actually performed.
- Separate direct observations, author-reported context, and technical interpretation.
- Record exact commands, filters, addresses, and values only when they are visible in retained evidence or confirmed lab notes.
- Do not invent packet numbers, timestamps, responses, commands, or missing capture details.
- Do not publish real credentials, tokens, personal information, or unrelated sensitive network details. Redact screenshots before committing them if they expose anything sensitive.
- Do not upload third-party PCAPs or datasets unless their licence permits redistribution; link to the source when appropriate.
- Keep attack simulations limited to systems and networks owned by you or explicitly authorised for testing.
- These are controlled learning exercises, not evidence of professional SOC employment or production incident handling.

## Author

**Sanket Shetty** — BSc Information Technology student, developing practical skills in defensive security and SOC operations.

- GitHub: https://github.com/shettysanket06
- LinkedIn: https://www.linkedin.com/in/sanket-shetty-467008329
