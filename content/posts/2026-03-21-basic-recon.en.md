---
title: "0x6. Basic Reconnaissance"
date: 2026-03-21T12:00:00+03:00
categories: [deep-dive, malware-analysis]
tags: [static-analysis, dynamic-analysis, tools, reconnaissance, network-analysis]
toc: true
draft: false
translationKey: "basic-recon"
---

Bismillah

Whenever we intend to analyze any file, we follow the steps below, irrespective of whether the objective is to determine whether the file is benign or contains malware, or even whether we intend to crack its protection:

## The 4 Stages of Analysis

1. **Basic Static Analysis:** This analysis does not require deep technical expertise, but relies entirely on tools that operate automatically (such as VirusTotal). It reveals indicators that show whether the file is a virus or not.
   > Rule: This analysis is performed without running the executable.

2. **Basic Dynamic Analysis:** Similar to the preceding stage, but the distinction is that here a virtualized environment is required.
   > Rule: This step requires running the executable in order to observe its mechanism and actual behavior.

3. **Advanced Static Analysis:** At this stage, one must possess sufficient expertise to work with disassemblers such as IDA Pro and Ghidra. We summarize this stage as the analysis of assembly code to understand its operation—that is, the structure the program follows.

4. **Advanced Dynamic Analysis:** This stage demands technical expertise, as one will work with a debugger. To contrast it with a disassembler: the difference is that a debugger permits the execution of code and stepping through it line by line in live memory, whereas a disassembler does not execute code (which is the basis of static analysis). Among the foremost debuggers is x64dbg.

---

## Basic Reconnaissance

In this article, we discuss the first two steps of the analysis process, known as basic reconnaissance: the rapid collection of preliminary information and indicators concerning the file prior to undertaking deeper analysis. As noted, this step does not require complex technical expertise; it consists of employing simple tools. We will enumerate each tool, its purpose, and an image of its interface.

### 1. Helpful Websites

- [VirusTotal](https://www.virustotal.com/): To verify the file's digital fingerprint (hashing) and determine whether antivirus vendors have classified it as malicious.
  
  ![Virustotal](/assets/img/posts/basic-recon/virustotal.png)
  _Figure (1): The VirusTotal website interface._

- [Hybrid-Analysis](https://www.hybrid-analysis.com/): A service providing automated execution of the file and producing a rapid report on its behavior (file, process, and network logs).
  
  ![hybrid analysis](/assets/img/posts/basic-recon/hybridanalysis.png)
  _Figure (2): The Hybrid-Analysis website interface._

- [CyberChef](https://gchq.github.io/CyberChef/): A tool for decoding and analyzing data (such as Base64, XOR).
  
  ![Cyber Chef](/assets/img/posts/basic-recon/cyberchef.png)
  _Figure (3): The CyberChef website interface._

---

### 2. Information Gathering: Static

- [Detect It Easy (DIE)](https://github.com/horsicq/Detect-It-Easy): To determine the file type and compiler type, and whether it is packed with a packer. Among the most important indicators in this program is the entropy.
  
  ![Detect It Easy](/assets/img/posts/basic-recon/die.png)
  _Figure (4): The DIE application interface._

- [FLOSS](https://github.com/mandiant/flare-floss): A tool capable of extracting strings that the programmer attempts to encrypt within the code (obfuscated strings).

  ![Floss](/assets/img/posts/basic-recon/floss.png)
  _Figure (5): The FLOSS program execution command._

- [PE-Bear](https://github.com/hasherezade/pe-bear): Used to analyze the file headers (PE Headers) and explore resources, and to identify the libraries (DLLs) and functions the program invokes, such as `CreateProcessA`.
  
  ![PE Bear](/assets/img/posts/basic-recon/pe-bear.png)
  _Figure (6): The PE-Bear application interface._

---

### 3. Information Gathering: Dynamic

- [Process Monitor (ProcMon)](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon): Monitors file activity, the system registry, and network traffic in real time.
  
  ![ProcMon](/assets/img/posts/basic-recon/procmon.png)
  _Figure (7): The ProcMon application interface._

- [Process Explorer (ProcExp)](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer): Used to monitor the processes currently active within the system and to detect any suspicious processes.
  
  ![ProcExp](/assets/img/posts/basic-recon/procexp.png)
  _Figure (8): The ProcExp application interface._

---

### 4. Network Monitoring

- [FakeNet-NG](https://github.com/mandiant/fakenet-ng): Used to simulate internet services locally, enabling the analyst to observe network requests (such as HTTP, GET) without requiring a genuine internet connection, thereby avoiding risk.
  
  ![FakeNet-NG](/assets/img/posts/basic-recon/fakenet.png)
  _Figure (9): Image of the file generated when the application is run, bearing the `.pcap` extension, which is opened in Wireshark._

- [Wireshark](https://www.wireshark.org/): A tool for capturing and analyzing network traffic (network sniffing) to determine whether the file is attempting to communicate with external command-and-control servers.
  
  ![WireShark](/assets/img/posts/basic-recon/wireshark.png)
  _Figure (10): The Wireshark application interface._
