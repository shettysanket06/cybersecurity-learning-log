# HTTP Traffic Investigation & Credential Visibility Analysis

**Activity type:** Home SOC lab / network traffic analysis  
**Author:** Sanket Shetty  
**Original LinkedIn post:** https://www.linkedin.com/posts/sanket-shetty-467008329_cybersecurity-socanalyst-wireshark-share-7462391397011345408-pdP5/

## 1. Objective

Examine how HTTP communication appears at packet level and understand what information may be exposed when a client submits data over unencrypted HTTP.

## 2. Lab environment

The original activity described the following setup:

- **Client:** Kali Linux
- **Server:** Windows 11 virtual machine
- **HTTP server:** Python's built-in HTTP server
- **Traffic analysis:** Wireshark

The exercise used a simple HTTP login page hosted on the Windows VM. GET and POST requests were sent from Kali Linux and captured for analysis.

## 3. Methodology

The activity followed this general workflow:

1. Host a simple test HTTP login page on the Windows 11 VM using Python's built-in HTTP server.
2. Send HTTP GET and POST requests from the Kali Linux client.
3. Capture the client-server traffic in Wireshark.
4. Inspect the HTTP conversation, request headers, response codes, and transmitted form data.
5. Use Wireshark's **Follow HTTP Stream** feature to reconstruct the conversation between the client and server.

> Add the exact commands, test values, capture interface, filter expressions, and screenshots from your original lab before treating this as a fully reproducible lab guide. They were not included in the accessible LinkedIn post text.

## 4. Observations reported in the original activity

- HTTP POST requests exposed submitted test credentials in plaintext within the captured traffic.
- HTTP headers including `User-Agent`, `Host`, `Content-Type`, and `Referer` were visible in the packet stream.
- HTTP response codes and server information could be identified during analysis.
- **Follow HTTP Stream** made it possible to reconstruct the client-server conversation.

## 5. Defensive interpretation

The exercise demonstrates that HTTP does not encrypt application-layer content. Anyone able to capture the traffic on the relevant network path may be able to inspect submitted form data and metadata. This creates a risk of credential disclosure and interception.

For production systems, authentication pages and sensitive application traffic should be protected using HTTPS/TLS with correctly configured certificates. Network defenders can also investigate unexpected cleartext HTTP use, especially where authentication or other sensitive data is involved.

## 6. Limitations and evidence needed

This write-up is based on the text of the original LinkedIn post. The following supporting artifacts have not yet been added:

- Original Wireshark screenshots showing the HTTP requests and Follow HTTP Stream output.
- The relevant PCAP, if it can be safely shared and contains no real credentials or private data.
- Exact commands used to start the server and send requests.
- Exact Wireshark display filters and the packet numbers used as evidence.

Do not add real credentials. Use synthetic test credentials only. If sharing a PCAP, inspect and sanitize it first.

## 7. Key learning

Packet analysis can reveal information that may not be obvious from the browser interface. Understanding HTTP methods, headers, response codes, and stream reconstruction helps a SOC analyst explain why unencrypted protocols create exposure and what evidence supports that assessment.

## 8. Original post

See the [LinkedIn activity](https://www.linkedin.com/posts/sanket-shetty-467008329_cybersecurity-socanalyst-wireshark-share-7462391397011345408-pdP5/).

## 9. Suggested interview discussion

Be prepared to explain:

1. What is the difference between an HTTP GET and POST request?
2. Why can the request body and headers be read in a plaintext HTTP capture?
3. What does Wireshark's Follow HTTP Stream feature show?
4. What changes when the same application is accessed over HTTPS?
5. What evidence in the capture demonstrates that the test data was transmitted without encryption?
