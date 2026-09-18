CVE PoCs 🔐

A collection of proof-of-concept implementations for CVE research, vulnerability analysis, and Linux security experimentation.

This repository contains C-based PoCs developed to study selected vulnerabilities affecting Linux subsystems and to explore their underlying mechanisms.

Depending on the vulnerability, the implementations range from controlled user-space simulations to experiments interacting with real Linux interfaces and subsystems.

«Note: A PoC in this repository is not necessarily a complete or reliable exploit. Some implementations reproduce vulnerable logic in a controlled environment rather than triggering the vulnerability directly in the Linux kernel.»

---

🎯 Purpose

The main objectives of this repository are to:

- Study the technical mechanisms behind Linux vulnerabilities
- Reproduce vulnerable conditions in controlled environments
- Analyze memory-safety and boundary-checking issues
- Explore kernel subsystem behavior
- Investigate security implications of containerized environments
- Develop experimental PoCs for vulnerability research
- Document observations and limitations during security experiments

---

🔬 Areas of Research

The PoCs cover several categories of Linux security issues, including:

Memory Safety

- Use-after-free scenarios
- Out-of-bounds access
- Buffer overflows
- Memory lifetime and object reuse

Integer & Boundary Handling

- Integer wraparound
- Allocation-size mismatches
- Insufficient bounds checking
- Invalid length calculations

Concurrency & State Management

- Race-condition scenarios
- Reference and usage counter handling
- Transaction rollback behavior
- Object lifecycle management

Linux Subsystems

The repository includes experiments involving components such as:

- "io_uring"
- RxRPC
- Netfilter / nftables
- AMDGPU / debugfs
- ALSA
- HID / BPF
- RAID5
- Netlink

---

📂 Repository Structure

CVE_Pocs/
│
├── 2023/
│   └── ...
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

---

🧪 Selected PoC Examples

io_uring

One PoC models a fixed-buffer registration scenario involving page calculation and access beyond the intended buffer boundaries.

The implementation uses a controlled user-space model to track:

- Pages associated with a registered buffer
- Pages outside the expected buffer range
- Out-of-bounds accesses
- Detected corruption events

Approach: user-space simulation.

---

RxRPC / XDR

Another PoC models an integer wraparound during the calculation of aligned lengths.

The experiment examines how an incorrect size calculation can result in:

Large requested size
        ↓
32-bit wraparound
        ↓
Incorrect allocation size
        ↓
Out-of-bounds write

Approach: controlled user-space simulation.

---

AMDGPU

A PoC models insufficient size validation during a GPR wave buffer operation.

It compares the requested size with the simulated buffer capacity and records potential out-of-bounds writes.

Approach: user-space simulation.

---

Netfilter / nftables

A PoC models an object-lifecycle scenario involving nftables chains, catchall elements, transaction aborts, and a resulting use-after-free condition.

The simulation tracks:

- Object usage counters
- Transaction rollback
- Chain deletion
- Access to previously released memory
- Potential object reuse

Approach: user-space simulation.

---

ALSA / Scarlett2

A PoC interacts with the ALSA control interface and prepares control data intended to exercise a vulnerable driver path.

It demonstrates a different research approach from the purely simulated PoCs by interacting with an actual Linux subsystem through the ALSA API.

Approach: Linux subsystem interaction.

---

HID / BPF

A PoC models a situation where a BPF-related return value exceeds the size of a destination buffer.

The experiment tracks:

- Returned length
- Buffer capacity
- Out-of-bounds writes
- Corruption indicators

Approach: user-space simulation.

---

🛠️ Technologies

Languages

- C
- Bash / shell scripting for experimentation

Operating System & Kernel

- Linux
- Linux kernel interfaces
- Kernel subsystems
- Debugging and system observation tools

Security

- CVE analysis
- Vulnerability research
- Memory-safety analysis
- Boundary-condition testing
- Kernel security
- Container security

Systems & Interfaces

- io_uring
- Netlink
- Netfilter / nftables
- ALSA
- BPF
- debugfs

---

🔍 Research Workflow

The PoCs are developed as part of a broader vulnerability-analysis workflow:

CVE identification
       ↓
Technical analysis
       ↓
Vulnerable mechanism identification
       ↓
PoC development
       ↓
Controlled experimentation
       ↓
Behavior / anomaly observation
       ↓
Results and limitations

The goal is not simply to execute an exploit, but to understand why a vulnerability occurs, under which conditions it can be observed, and what security boundary may be involved.

---

🐳 Container Security Context

Several experiments are designed with containerized environments in mind.

Where relevant, the PoCs can detect common container environments and record whether an experiment is running inside or outside a container.

This supports research into questions such as:

- How Linux kernel vulnerabilities behave from a container
- Which kernel interfaces are accessible from containers
- How container isolation affects vulnerability exposure
- Whether a kernel vulnerability can cross a container boundary
- Which security mechanisms limit or prevent exploitation

These observations are experimental and should not be interpreted as proof of container escape or host compromise unless independently demonstrated.

---

⚠️ Limitations

These PoCs have different levels of fidelity.

Some implementations:

- Simulate vulnerable kernel logic in user space
- Use simplified representations of kernel structures
- Reproduce vulnerability conditions rather than the complete kernel execution path
- Interact with real Linux interfaces without necessarily demonstrating successful exploitation

Therefore:

«Detection of a simulated corruption or vulnerable condition does not by itself demonstrate successful kernel exploitation, privilege escalation, or container escape.»

Results should be interpreted together with the corresponding CVE description, affected kernel versions, source-code analysis, and experimental environment.

---

🔐 Responsible Use

These PoCs are intended for:

- Security research
- Vulnerability analysis
- Academic experimentation
- Defensive testing
- Isolated laboratory environments

Only run experiments against systems you own or have explicit authorization to test.

For kernel-level experimentation, use isolated test environments such as virtual machines or dedicated research systems whenever possible.

---

📚 References

For each vulnerability, consult the corresponding authoritative CVE record, vendor advisory, Linux kernel documentation, and upstream security discussions where available.

The CVE identifiers are used to connect each PoC with the vulnerability being investigated.

---

👤 Author

Lumière Minka

Software Engineer interested in:

"Cybersecurity" · "Linux Systems" · "Container Security" · "Cloud Computing" · "Vulnerability Research"

This repository is part of my broader exploration of Linux security, container isolation, and cloud/serverless security.
