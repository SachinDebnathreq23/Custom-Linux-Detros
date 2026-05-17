# 🐧 HybridOS: Pentesting & Distributed Compute Cluster

![Current Phase](https://img.shields.io/badge/Current_Phase-Sector_1:_Bootstrapping-orange)
![Architecture](https://img.shields.io/badge/Architecture-x86__64-blue)
![Base](https://img.shields.io/badge/Base-Debian_12_Stable-red)

## 📖 Project Overview

This repository contains the blueprints, build scripts, and configurations for a highly specialized, custom Linux distribution. The objective of this project is to solve a complex architectural challenge: engineering an operating system that seamlessly bridges the divide between a **stable server environment**, a **specialized penetration testing workstation**, and a **decentralized compute cluster orchestrator**.

Historically, attempting to merge stable environments (like Debian) with rolling-release security distros (like Kali Linux or Parrot OS) results in catastrophic dependency collapse (the "FrankenDebian" dilemma). Furthermore, running heavy cluster workloads on consumer laptop hardware leads to severe thermal throttling.

This OS solves these issues through advanced kernel topologies, meta-distribution integration, and High-Throughput Computing (HTC) middleware.

---

## 🏗️ Core Architecture

1. **The Base OS**: Built programmatically using Debian `live-build`. Relies on Debian Stable for an unbreakable foundation.
2. **Cross-Ecosystem Integration**: Utilizes **Bedrock Linux** to create isolated "strata." This allows the native execution of bleeding-edge Kali Linux and Parrot OS security tools directly alongside Debian server utilities without dependency conflicts.
3. **Hybrid Laptop-Server Kernel**: Features a custom-compiled Linux kernel with `CONFIG_PREEMPT_DYNAMIC`, allowing boot-time switching between raw server throughput (`preempt=none`) and low-latency desktop responsiveness (`preempt=full`). Utilizes hardware P-states and `thermald` for proactive thermal governance.
4. **Decentralized CPU Pooling**: Integrates **HTCondor** directly into the OS fabric. Secondary computers on the LAN can boot from an amnesic USB "Worker Node Mode" to transparently donate their idle CPU cycles to the master laptop, creating a massive, decentralized resource pool.

---

## 🚀 Project Roadmap & Status

We are currently actively developing this project. Below is the phased execution plan:

- [x] **Phase 0: Architectural Research & Planning**
- [ ] 🚧 **Phase 1: Bootstrapping the Base System (CURRENTLY WORKING ON)**
  - Setting up the Oracle VirtualBox build environment.
  - Initializing the `live-build` configuration tree.
  - Generating the first functional Debian base ISO.
- [ ] **Phase 2: Custom Kernel Compilation**
  - Configuring `make menuconfig` for dynamic preemption and XDP support.
  - Compiling kernel `.deb` packages and injecting them into the build pipeline.
- [ ] **Phase 3: Bedrock Linux Integration (Security Strata)**
  - Implementing build hooks to hijack the Debian base with Bedrock Linux.
  - Automating the retrieval of Kali and Parrot OS toolchains.
- [ ] **Phase 4: HTCondor Cluster Orchestration**
  - Configuring the master Central Manager.
  - Developing the amnesic (tmpfs) "Worker Node Mode" for secondary LAN devices.
- [ ] **Phase 5: Security Hardening & ISO Synthesis**
  - Kernel lockdown, Software Bill of Materials (SBOM) generation, and final ISO compression.

---

## 🛠️ Development Environment

*   **Host OS**: Windows 10
*   **Build Hypervisor**: Oracle VirtualBox (Debian 12 Build VM)
*   **Build Toolchain**: `live-build`, `debootstrap`

---

*Note: This repository is currently in the foundational bootstrapping phase. Build scripts and configuration files will be pushed to this repository as they are developed.*
