# Comprehensive Project Requirements

To successfully engineer, build, and deploy this custom hybrid Linux distribution, the following prerequisites, resources, and requirements must be fulfilled.

## 1. Hardware Requirements

### Build Environment (The Host Machine)
*   **CPU**: Multi-core processor (8+ cores recommended) to handle heavy kernel compilation (`make -j$(nproc)`) and SquashFS compression.
*   **RAM**: Minimum 16 GB (32 GB preferred) to cache packages and speed up RAM-disk based compilation phases.
*   **Storage**: At least 100 GB of fast NVMe/SSD free space for storing the Debian repository cache, extracted kernel sources, and intermediate ISO build artifacts.
*   **Network**: High-speed, stable internet connection for downloading thousands of packages, kernel sources, and Bedrock strata.

### Deployment Environment (The Master Node / Laptop)
*   **CPU**: Modern x86_64 architecture with support for Hardware P-States (Intel Core 6th Gen+ or AMD Zen+ architecture).
*   **Network Interface**: Gigabit Ethernet (or reliable Wi-Fi 6) capable of sustaining high-throughput LAN traffic without hardware bottlenecking.

### Deployment Environment (Worker Nodes)
*   **Hardware**: Arbitrary x86_64 devices (older desktops/laptops).
*   **Boot Media**: USB flash drives (8GB+) for booting the "Worker Node Mode" live ISO.
*   **Network**: Wired LAN connection (preferred) to the central router/switch for reliable HTCondor ClassAd broadcasting and file transfer.

## 2. Software & Tooling Requirements

### Host Operating System
*   A stable Linux host environment (preferably Debian 12 "Bookworm" or Ubuntu LTS) to ensure absolute compatibility with the build tools.

### Required Build Packages
*   `live-build` and `debootstrap`: For programmatic ISO generation and rootfs bootstrapping.
*   `build-essential`, `fakeroot`, `libncurses-dev`, `bc`, `bison`, `flex`, `libelf-dev`, `libssl-dev`: For custom kernel configuration and compilation.
*   `squashfs-tools`, `xorriso`, `grub-pc-bin`, `grub-efi-amd64-bin`: For final ISO compression and hybrid bootloader generation.

### Target Distribution Components
*   **Kernel Source**: Linux Kernel Source Tree (post-5.12 to support `CONFIG_PREEMPT_DYNAMIC`).
*   **Integration Middleware**: Bedrock Linux installation script (`bedrock-linux-install.sh`).
*   **Cluster Middleware**: HTCondor Debian packages and configuration templates.
*   **Thermal Daemons**: `thermald` and associated ACPI/RAPL utilities.

## 3. Knowledge & Engineering Prerequisites

*   **Debian Live-Build Ecosystem**: Deep understanding of the `config/` directory structure, `.chroot` package lists, and executable hooks.
*   **Kernel Configuration**: Familiarity with `make menuconfig`, understanding of Linux scheduling (preemption models), network stack tuning (Ring buffers, XDP), and hardware-level power management.
*   **Advanced Package Management**: Knowledge of DEB822 repository formats, GPG key isolation, and APT pinning (as a fallback or complement to Bedrock Linux).
*   **Distributed Systems**: Understanding of HTCondor's ClassAd matchmaking system, daemons (`schedd`, `collector`, `negotiator`, `startd`), and network topography.
*   **Security & Compliance**: Knowledge of kernel lockdown parameters, principle of least privilege, and SBOM generation tools (like Syft or Trivy utilizing the CycloneDX standard).

## 4. Network and Infrastructure Requirements
*   **Local Area Network (LAN)**: A router or switch capable of handling high localized traffic.
*   **DHCP/DNS**: A properly configured local network providing consistent IP addresses to the worker nodes so they can reliably locate the master laptop's `condor_collector` daemon.

## 5. Development Workflow Requirements
*   **Version Control**: A Git repository to strictly maintain the `live-build` configuration files, kernel config (`.config`), and custom hook scripts.
*   **Iterative Testing**: A hypervisor (e.g., QEMU/KVM, VirtualBox) for rapidly testing the generated ISOs in a virtualized environment before flashing to physical hardware.
