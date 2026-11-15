<div align="center">

# Network Traffic Analysis & Investigation Using Wireshark

**Cyber Security Assignment 02 · Mars Tech Campus**

![Wireshark](https://img.shields.io/badge/Wireshark-4.6.9-1679A7?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Windows%2011-0078D4?style=flat-square)
![Category](https://img.shields.io/badge/Category-Network%20Traffic%20Analysis-243E63?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-2E8B57?style=flat-square)

**Prepared by:** AS. Mohammed Sasni  
**Submission date:** 15 November 2026

*A practical, evidence-based investigation of TCP, DNS, HTTP, ICMP, and an optional DNS-port anomaly using recorded Wireshark packet captures.*

</div>

---

## Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Tools and Environment](#tools-and-environment)
- [Assignment Tasks](#assignment-tasks)
- [Capture Files](#capture-files)
- [Getting Started](#getting-started)
- [Wireshark Display Filters](#wireshark-display-filters)
- [Key Findings](#key-findings)
- [Evidence and Report](#evidence-and-report)
- [Investigation Scope and Limitations](#investigation-scope-and-limitations)
- [Safety and Responsible Use](#safety-and-responsible-use)
- [References](#references)
- [Acknowledgement](#acknowledgement)

## Project Overview

This repository contains the completed **Network Traffic Analysis & Investigation Using Wireshark** practical assignment for **Mars Tech Campus**. The project uses previously recorded packet capture files to examine network protocols, communication endpoints, TCP connection establishment, DNS name resolution, HTTP request–response exchanges, and an optional anomaly involving traffic on DNS-associated port 53.

The repository is intended as an **educational investigation and reporting project**, not a network attack tool. Findings are supported by packet numbers, observed protocol fields, timestamp information, screenshots, and evidence tables. Unusual behaviour is described separately from confirmed malicious activity.

## Objectives

- Explore Wireshark's **Packet List**, **Packet Details**, and **Packet Bytes** panes.
- Identify protocols, IP addresses, packet lengths, and communication direction.
- Investigate **TCP flags**, port numbers, and the three-way handshake.
- Examine **DNS queries and responses**, including reverse DNS (PTR) lookups.
- Analyse **HTTP requests and responses** and inspect an HTTP stream.
- Prepare an investigation summary based on verifiable packet evidence.
- Optionally assess unusual TCP communication involving **port 53**, while documenting uncertainty and limitations.

## Tools and Environment

| Component | Details |
|---|---|
| Network analyser | [Wireshark](https://www.wireshark.org/) |
| Version used | 4.6.9 |
| Operating system used | Windows 11 |
| Data sources | Official Wireshark sample captures |
| File formats | `.pcap`, `.pcapng`, and compressed `.pcapng.gz` |
| Analysis approach | Offline inspection of existing packet captures |
| Submission material | Written report, packet captures, observation tables, and screenshots |

> **No programming environment or live packet capture is required** to review these samples. Wireshark is the only essential tool for the practical analysis.

## Assignment Tasks

| Section | Activity | Main focus |
|---|---|---|
| Task 01 | Install and Explore Wireshark | Interface, packet panes, and capture navigation |
| Task 02 | Identify Network Protocols and Addresses | Source/destination addresses, protocols, frame lengths |
| Task 03 | Investigate TCP Communication | Ports, control flags, TCP three-way handshake |
| Task 04 | Analyse DNS Traffic | Queries, response records, PTR lookup |
| Task 05 | Examine Basic HTTP Traffic | GET request, `200 OK`, Follow HTTP Stream |
| Task 06 | Prepare a Network Investigation Summary | Evidence assessment, confidence, limitations |
| Optional challenge | Investigate a DNS Anomaly | Unusual TCP traffic on port 53; packet timestamps and context |

The optional challenge is included for additional practical learning and is separate from the compulsory activities.

## Capture Files

The captures used in the assignment are available through the [official Wireshark Sample Captures collection](https://wiki.wireshark.org/SampleCaptures).

| Capture file | Used for | What to examine |
|---|---|---|
| `tcp-ecn-sample.pcap` | Tasks 01–03 | TCP packets, addresses, flags, handshake, ECN-related fields |
| `dns+icmp.pcapng` | Task 04 | DNS and ICMP traffic, matching queries and responses |
| `http.cap` | Task 05 | HTTP GET requests, server responses, HTTP stream |
| `dns-remoteshell.pcap` | Optional challenge | DNS-filtered packets and unusual TCP traffic involving port 53 |

**Note:** The DNS/ICMP file is distributed as `dns+icmp.pcapng.gz` in the sample collection; the assignment uses the extracted file `dns+icmp.pcapng`.

The exact locations of uploaded files may differ depending on the repository layout. Locate the corresponding filenames in the repository's file list, or retrieve the original samples from the official collection.

## Getting Started

### 1. Install Wireshark

Download Wireshark from the [official website](https://www.wireshark.org/download.html) and install it for your operating system. The assignment was completed using **Wireshark 4.6.9 on Windows 11**; another compatible release may display some interface elements differently.

### 2. Download or open a capture

1. Download the repository files using **Code → Download ZIP** on GitHub, or clone the repository using Git.
2. Extract the downloaded ZIP if necessary.
3. Launch **Wireshark**.
4. Choose **File → Open** (`Ctrl + O`).
5. Select one of the supplied `.pcap` or `.pcapng` files.
6. Use the packet list to choose an individual packet and expand its protocol fields in the details pane.

> Only open the sample files in Wireshark for analysis. The optional challenge does not require connecting to any endpoint or running any payload.

### 3. Inspect the packets

- **Packet List:** Locate the packet number, time, source, destination, protocol, length, and summary.
- **Packet Details:** Expand TCP, DNS, HTTP, and IP fields to verify the technical observations.
- **Packet Bytes:** Inspect the bytes already recorded in the capture, where relevant.
- **Display Filter:** Enter a filter and press **Enter**; a display filter hides non-matching packets without altering the capture.

### 4. Reproduce the key observations

| Capture | Suggested starting point | Observation |
|---|---|---|
| `tcp-ecn-sample.pcap` | Packets 1–3 | SYN → SYN-ACK → ACK connection establishment |
| `dns+icmp.pcapng` | Packets 2–3 | PTR query and matching DNS response |
| `http.cap` | Packets 4 and 38 | `GET /download.html` and `HTTP/1.1 200 OK` |
| `dns-remoteshell.pcap` | Packets 14, 17, 18, 21, 22 and 25 | TCP connection and subsequent data exchange involving port 53 |

Packet numbers are **local to each capture file**, not global identifiers across all files.

## Wireshark Display Filters

Type one of these expressions into Wireshark's **Display Filter** bar and press **Enter**:

| Filter | Purpose |
|---|---|
| `tcp` | Show traffic Wireshark identifies as TCP |
| `dns` | Show traffic Wireshark decodes as DNS |
| `http` | Show traffic Wireshark decodes as HTTP |
| `tcp.port == 53` | Show TCP traffic with source or destination port 53 |

`dns` is a **protocol filter**, whereas `tcp.port == 53` is a **port filter**. They can return different packets because a port number does not guarantee that the payload follows that protocol.

For details, see the [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html_chunked/) and [Display Filter Reference](https://www.wireshark.org/docs/dfref/).

## Key Findings

### TCP — connection establishment

In `tcp-ecn-sample.pcap`, Packets **1–3** show a three-way handshake between **1.1.23.3** and **1.1.12.1**. Packet 1 uses source port **46557** and destination port **80**, with **SYN, ECE, and CWR** flags. The observed sequence supports TCP connection establishment and illustrates ECN capability negotiation.

### DNS — reverse name resolution

In `dns+icmp.pcapng`, Packet **2** contains a PTR lookup for `8.8.8.8.in-addr.arpa`; Packet **3** contains the corresponding DNS response with hostname `google-public-dns-a.google.com` and a **No error** status. The response links to the matching query in frame 2.

### HTTP — request and response

In `http.cap`, Packet **4** contains `GET /download.html HTTP/1.1`; Packet **38** contains `HTTP/1.1 200 OK`, including HTML content. The Follow HTTP Stream feature reveals the recorded request and response. The sample illustrates the visibility of unencrypted HTTP content to an observer with access to the capture.

### Optional challenge — unusual DNS-port traffic

In `dns-remoteshell.pcap`, Wireshark displays **six decoded DNS packets** out of **131 total packets**, while additional TCP communication involving port **53** is present outside the `dns`-filtered results.

Packets **14, 17, and 18** show TCP connection establishment. Packet **21** contains an **88-byte TCP payload**, and Packet **22** (time **25.556102 seconds**) is identified as a **retransmission** of that segment, sent from **192.168.1.2:53** to **192.168.1.3:1396**. Its recorded bytes include readable text associated with a Windows command environment. Packet **25** contains a **four-byte TCP payload** in the opposite direction.

**Interpretation:** The unusual port/payload combination warrants investigation. The examined packets alone **do not prove** malicious intent, unauthorized access, successful remote-shell operation, or complete system compromise.

## Evidence and Report

The full assignment report documents:

- **Objectives and practical procedures** for each task.
- **Question-and-answer explanations** aligned with the assignment brief.
- **Packet observation tables** identifying packet numbers, addresses, protocols, flags, timestamps, and HTTP/DNS details.
- **Wireshark screenshots** supporting the stated findings.
- **Investigation summary, conclusion, and references**.

The submitted report is available among the repository files in Word and/or PDF form, depending on what was uploaded. Screenshot evidence may also be embedded directly in the report rather than stored as separate images.

For the optional challenge, the report includes a table of TCP packets with relative timestamps and an analysis of the differences between decoded DNS traffic and TCP traffic associated with port 53.

## Investigation Scope and Limitations

- The project analyses **previously recorded sample captures**, not traffic collected from a production network.
- The capture files represent **separate traffic samples** and should not be treated as one continuous incident.
- A completed TCP handshake confirms connection establishment in the observed sequence, not the success of every later application operation.
- DNS responses and HTTP status codes should be interpreted according to what the packets actually show.
- Unusual port usage, retransmission, and readable payload data are **investigative observations**, not automatic proof of an attack.
- Stronger security conclusions would require **longer captures, endpoint and application logs, DNS records, firewall/security alerts, and network context**.

## Safety and Responsible Use

This repository is for **authorized education and offline traffic analysis only**.

- Use the provided captures only as recorded evidence.
- **Do not connect** to IP addresses or domains found in the samples.
- **Do not execute** extracted or downloaded payloads.
- **Do not attempt to reproduce** the remote-shell activity suggested by the optional sample.
- Respect privacy, institutional requirements, and applicable rules when sharing packet captures or screenshots.
- Before making a repository public, review the report and attachments for personal details such as student identification numbers.

## References

1. [Wireshark — Official Website](https://www.wireshark.org/)
2. [Wireshark — Sample Captures](https://wiki.wireshark.org/SampleCaptures)
3. [Wireshark — Official Documentation](https://www.wireshark.org/docs/)
4. [Wireshark — User's Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
5. [Wireshark — Display Filter Reference](https://www.wireshark.org/docs/dfref/)
6. **Mars Tech Campus** — *Cyber Security Assignment 02: Network Traffic Analysis & Investigation Using Wireshark* (course assignment brief, 2026).

## Acknowledgement

Thanks to **Mr. MIM. Ramzeen** for his guidance and practical instruction, and to **Mars Tech Campus** for the learning opportunity and resources used in completing this assignment.

---

<div align="center">

**Mars Tech Campus · Cyber Security Assignment 02 · 15 November 2026**

*Evidence first. Interpret cautiously. Document clearly.*

</div>
