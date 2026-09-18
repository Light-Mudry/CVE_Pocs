CVE PoCs 🔬

A collection of proof-of-concept implementations developed for CVE research, vulnerability analysis, and security experimentation.

The repository primarily contains C-based PoCs exploring vulnerable behaviors in Linux and related system components.

Overview

This repository contains experimental implementations corresponding to selected CVEs investigated during vulnerability research and security analysis.

The PoCs are intended to help study:

- Vulnerability mechanisms
- Kernel and system-level behavior
- Memory-safety issues
- Race conditions and integer overflows
- Network subsystem interactions
- Security boundaries and isolation
- Reproduction and observation of vulnerable behavior

Depending on the CVE, a PoC may either reproduce the relevant behavior through a user-space simulation or interact with actual Linux interfaces and subsystems.

«Important: The presence of a CVE in this repository does not necessarily mean that the corresponding PoC provides a complete or reliable exploitation path. Some implementations are experimental simulations designed to study the underlying vulnerability mechanism.»

---

Repository Structure

CVE_Pocs/
│
├── 2023/
│
├── CVE-2023-0461.c
├── CVE-2023-1281.c
├── CVE-2023-2598.c
├── CVE-2023-3090.c
├── CVE-2023-3106.c
├── CVE-2023-3609.c
│
├── CVE-2024-23307.c
├── CVE-2024-49969.c
├── CVE-2024-50282.c
├── CVE-2024-53142.c
│
├── CVE-2026-23078.c
├── CVE-2026-23111.c
├── CVE-2026-23172.c
├── CVE-2026-23178.c
├── CVE-2026-23351.c
├── CVE-2026-23390.c
├── CVE-2026-31401.c
└── CVE-2026-31641.c

Each PoC is named according to the corresponding CVE identifier.

---

CVE Coverage

CVE| Year| Implementation| Main Area
CVE-2023-0461| 2023| C PoC| System security
CVE-2023-1281| 2023| C PoC| System security
CVE-2023-2598| 2023| C PoC| System security
CVE-2023-3090| 2023| C PoC| System security
CVE-2023-3106| 2023| C PoC| System security
CVE-2023-3609| 2023| C PoC| System security
CVE-2024-23307| 2024| C PoC| Linux / system security
CVE-2024-49969| 2024| C PoC| Linux / system security
CVE-2024-50282| 2024| C PoC| Linux / system security
CVE-2024-53142| 2024| C PoC| Linux / system security
CVE-2026-23078| 2026| C PoC| System / device interaction
CVE-2026-23111| 2026| C PoC| Linux networking
CVE-2026-23172| 2026| C PoC| Linux kernel
CVE-2026-23178| 2026| C PoC| Linux kernel
CVE-2026-23351| 2026| C PoC| Netfilter / nftables
CVE-2026-23390| 2026| C PoC| DMA / kernel subsystem
CVE-2026-31401| 2026| C PoC| Linux kernel
CVE-2026-31641| 2026| C PoC| Linux kernel

The exact behavior, affected component, prerequisites, and reproduction status are documented or can be documented individually for each PoC.

---

Example Research Areas

Memory-Safety Vulnerabilities

Some PoCs explore memory-management and lifetime-related vulnerability mechanisms.

For example, the repository includes an experimental TCP ULP/TLS use-after-free simulation illustrating a sequence involving:

TCP socket
    ↓
TLS ULP context
    ↓
Context release
    ↓
Dangling pointer
    ↓
Socket transition
    ↓
Child socket inheritance
    ↓
Potential use-after-free

The implementation models the vulnerability mechanism in user space rather than directly reproducing kernel memory corruption.

Concurrency and Integer-Handling Issues

Other PoCs explore concurrency-related behavior and integer calculations through controlled user-space simulations.

A RAID5-related example models interactions involving:

- Concurrent accesses
- Cache-size updates
- Integer calculations
- State inconsistencies
- Potential corruption conditions

These simulations are useful for studying the underlying logic without requiring direct manipulation of kernel memory.

Linux Networking and Netfilter

Some of the newer PoCs interact with Linux networking interfaces.

For example, one implementation uses:

- Linux user/network namespaces
- Netlink
- "nf_tables"
- "libmnl"
- "libnftnl"

to prepare and submit structures associated with nftables/Pipapo experimentation.

This category of PoC is closer to interaction with the actual Linux subsystem rather than a purely user-space simulation.

---

Research Workflow

The PoCs are developed as part of an experimental vulnerability-analysis workflow:

CVE
 │
 ▼
Vulnerability analysis
 │
 ▼
Affected component / subsystem
 │
 ▼
PoC implementation
 │
 ▼
Controlled execution
 │
 ▼
Behavior observation
 │
 ▼
Security impact analysis

The objective is to understand and characterize vulnerable behavior rather than simply provide an exploitation tool.

---

Technologies

- C
- Linux
- Linux kernel interfaces
- POSIX APIs
- pthreads
- Network namespaces
- User namespaces
- Netlink
- Netfilter / nftables
- libmnl
- libnftnl
- GCC
- Git

---

Experimental Environment

PoCs should be evaluated in isolated and controlled environments.

Depending on the vulnerability, experiments may require:

- A specific Linux kernel version
- Specific kernel configuration options
- Required system libraries
- Appropriate privileges or capabilities
- Dedicated test environments

Individual PoCs may therefore behave differently depending on the kernel, configuration, architecture, available libraries, and execution environment.

---

Safety and Responsible Use

These PoCs are provided for:

- Educational purposes
- Security research
- Vulnerability analysis
- Defensive security testing
- Controlled laboratory experimentation

Run PoCs only on systems you own or are explicitly authorized to test.

Do not execute experimental kernel or vulnerability code on production systems.

A PoC may trigger crashes, unexpected system behavior, resource exhaustion, or other undesirable effects depending on the vulnerability and environment.

---

Limitations

A proof of concept is not necessarily a complete exploit.

Some implementations in this repository:

- Simulate vulnerable kernel behavior in user space
- Reproduce only part of the vulnerability mechanism
- Require specific kernel versions or configurations
- Demonstrate a vulnerable condition without achieving code execution
- Serve primarily as experimental research artifacts

The implementation status should therefore be evaluated individually for each CVE.

---

References

For each CVE, consult the corresponding authoritative vulnerability advisory and vendor/kernel documentation to verify:

- Affected versions
- Fixed versions
- Vulnerability description
- Severity
- Required conditions
- Security impact

---

Author

Lumière Minka

Software Engineer interested in:

- Cybersecurity
- Linux systems
- Container security
- Cloud computing
- Vulnerability research
- Secure software engineering
- Systems research
