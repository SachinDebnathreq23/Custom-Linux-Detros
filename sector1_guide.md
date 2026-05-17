# Sector 1: Bootstrapping the Base System

Welcome to Sector 1! Our goal here is to establish the isolated build environment and create the foundation of your custom Linux distribution. Because you are on Windows 10, we will perform all Linux operations inside an Oracle VirtualBox Virtual Machine.

Follow these steps carefully. 

---

## Step 1: Set Up the Debian 12 Build VM

If you haven't already created a Debian Virtual Machine, you need to set one up in VirtualBox. This acts as our secure "factory" for building the custom ISO.

1.  **Download Debian 12**: 
    *   Go to the official Debian website and download the **Debian 12 (Bookworm) Netinst ISO**.
2.  **Create the VM in VirtualBox**:
    *   **OS Type**: Linux / Debian (64-bit)
    *   **RAM**: Allocate at least **4096 MB** (4GB), ideally 8GB if your laptop can spare it.
    *   **CPU**: Allocate at least **2 to 4 processors**.
    *   **Hard Disk**: Create a dynamically allocated Virtual Hard Disk of at least **50 GB**.
3.  **Install Debian**:
    *   Boot the VM using the downloaded Debian ISO.
    *   Run through the graphical installer. When prompted for software selection, you only need the **"SSH server"** and **"standard system utilities"**. You do not need a desktop environment (like GNOME) for the build machine, as a terminal is faster and lighter, but you can install one if you prefer.
4.  **Boot into the VM**.

---

## Step 2: Install the Build Dependencies

Once your Debian 12 VM is up and running, open the terminal inside the VM and run the following commands to update the system and install the required ISO generation tools.

```bash
# Log in as root or use sudo
sudo apt update && sudo apt upgrade -y

# Install the core build tools
sudo apt install -y live-build debootstrap build-essential git curl
```

---

## Step 3: Initialize the Build Directory

We are going to create a dedicated folder for your project and initialize the `live-build` skeleton. Run these commands in the VM's terminal:

```bash
# Create a directory for the project
mkdir -p ~/custom-distro
cd ~/custom-distro

# Initialize the live-build configuration tree
lb config
```
This command creates two important directories: `auto/` and `config/`. This is where the entire DNA of your custom OS will live.

---

## Step 4: Define the Base Packages

Now we need to tell `live-build` what software to include in the base operating system. We want a lightweight, stable foundation. We will use `XFCE` as a fast, reliable desktop environment for the master node.

Create a file named `base.list.chroot` inside the package lists directory:

```bash
# Use nano to create the package list
nano config/package-lists/base.list.chroot
```

Paste the following list of packages into the file:

```text
# Base System and Desktop
xorg
xfce4
xfce4-goodies
lightdm

# Core Utilities
sudo
curl
wget
git
htop
net-tools
dnsutils
iputils-ping

# Networking and SSH
network-manager
network-manager-gnome
openssh-server
```

Save and exit (Press `CTRL+O`, `Enter`, then `CTRL+X`).

---

## Step 5: Test the Build (The First Compilation!)

Now it's time to test the pipeline and build your very first, basic custom ISO! This ISO won't have the pentesting tools or the cluster software yet—this is just to ensure the foundation works.

Run the build command (Note: This requires root privileges):

```bash
sudo lb build
```

> [!WARNING]
> **This process will take a while.** The system is actively downloading a fresh Linux filesystem from the internet, packing it, and compressing it. Depending on your internet speed and VM resources, this can take anywhere from 10 to 45 minutes.

### The Output
When the process finishes, you will see a file named something like `live-image-amd64.hybrid.iso` inside your `~/custom-distro` directory. 

Congratulations! That is your custom bootable operating system. You can create a *new* VirtualBox VM and use that ISO file as the boot disk to test it out.

---

### Ready for Sector 2?
Once you have successfully built and tested this foundational ISO, let me know. We will then move on to **Sector 2**, where we will download the Linux Kernel source code and compile your custom `CONFIG_PREEMPT_DYNAMIC` kernel tailored for the Hybrid Laptop-Server architecture!
