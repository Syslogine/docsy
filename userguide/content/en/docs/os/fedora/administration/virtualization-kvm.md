---
title: "Virtualization with KVM"
description: "Virtualization is a technology that allows you to create and run virtual machines (VMs) on a single physical host system. Kernel-based Virtual Machine (KVM) is a full virtualization solution for Linux that enables you to run multiple operating systems simultaneously on a single hardware platform. In this tutorial, we'll explore how to set up and use KVM on Fedora Linux for virtualization purposes."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction to KVM

KVM is a kernel module that provides hardware-assisted virtualization support on x86 hardware with virtualization extensions (Intel VT or AMD-V). It transforms the Linux kernel into a hypervisor, allowing it to run multiple virtual machines securely and efficiently.

KVM has several advantages over other virtualization solutions:

- **Performance**: KVM provides near-native performance for virtual machines due to hardware-assisted virtualization.
- **Open-source**: KVM is an open-source solution and part of the Linux kernel, making it free and accessible.
- **Integration**: KVM is tightly integrated with the Linux kernel, allowing for easy management and monitoring of virtual machines.
- **Security**: KVM leverages the Linux kernel's built-in security features, providing a secure and isolated environment for virtual machines.

## Installing KVM on Fedora Linux

Before you can use KVM on Fedora Linux, you need to ensure that your system meets the necessary hardware and software requirements.

### Hardware Requirements

- A CPU that supports hardware virtualization (Intel VT or AMD-V)
- Sufficient RAM and storage space for the host system and virtual machines

To check if your CPU supports hardware virtualization, run the following command:

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
```

If the output is greater than 0, your CPU supports hardware virtualization.

### Software Requirements

KVM is included in the Fedora Linux distribution by default, but you need to install a few additional packages:

1. Open a terminal and update the package lists:

   ```bash
   sudo dnf update
   ```

2. Install the required packages:

   ```bash
   sudo dnf install @virtualization
   ```

   This command installs the KVM hypervisor, QEMU emulator, and other necessary components.

3. Verify the installation by checking the KVM module status:

   ```bash
   lsmod | grep kvm
   ```

   You should see output similar to the following, indicating that the KVM module is loaded:

   ```
   kvm_intel             286720  0
   kvm                   690176  1 kvm_intel
   ```

Congratulations! You have successfully installed KVM on your Fedora Linux system.

## Creating a Virtual Machine

Now that you have KVM installed, you can create and manage virtual machines. There are several ways to create and manage VMs with KVM, including command-line tools like `virt-manager` and `virsh`, as well as graphical tools like the GNOME Boxes application.

In this section, we'll focus on using the `virt-manager` graphical tool, as it provides a user-friendly interface for managing virtual machines.

1. Install the `virt-manager` package:

   ```bash
   sudo dnf install virt-manager
   ```

2. Launch the `virt-manager` application from the application menu or by running the following command:

   ```bash
   virt-manager
   ```

3. In the `virt-manager` window, click on the "Create a new virtual machine" button.

4. Follow the wizard to configure your virtual machine:

   - Choose the installation source (ISO image, CDROM, or network install)
   - Set the RAM and CPU allocation for the virtual machine
   - Configure storage for the virtual machine (disk size and location)
   - Customize additional options like network configuration and video settings

5. Once you've completed the wizard, click the "Finish" button to create the virtual machine.

6. The virtual machine will start, and you can proceed with installing the guest operating system as you would on a physical machine.

During the installation process, you may be prompted to install additional drivers or software for better integration between the host and guest operating systems.

## Managing Virtual Machines

After creating your virtual machines, you can manage them using the `virt-manager` application or the command-line `virsh` tool.

### Using virt-manager

The `virt-manager` graphical tool provides a user-friendly interface for managing virtual machines. Here are some common tasks you can perform with `virt-manager`:

- Start, pause, and stop virtual machines
- View performance metrics like CPU, memory, and disk usage
- Take snapshots of virtual machines for backup or rollback purposes
- Attach additional storage devices or network interfaces
- Configure virtual machine settings like CPU, memory, and device allocation

### Using virsh

The `virsh` command-line tool provides a more powerful and scriptable way to manage virtual machines. Here are some common `virsh` commands:

- `virsh list` - List all virtual machines and their states
- `virsh start <vm-name>` - Start a virtual machine
- `virsh shutdown <vm-name>` - Gracefully shut down a virtual machine
- `virsh destroy <vm-name>` - Forcefully stop a virtual machine
- `virsh undefine <vm-name>` - Remove a virtual machine definition from KVM
- `virsh edit <vm-name>` - Edit the XML configuration of a virtual machine

You can find more `virsh` commands and their usage by running `virsh help` or referring to the `virsh` manual pages.

## Advanced KVM Configuration

While the default KVM configuration works well for most use cases, you may need to customize certain settings for advanced scenarios or specific workloads.

### CPU and Memory Allocation

KVM allows you to allocate specific CPU and memory resources to virtual machines. You can configure these settings during virtual machine creation or modify them later using `virt-manager` or the `virsh` tool.

To modify CPU and memory allocation using `virsh`, run the following commands:

```bash
# Change CPU allocation
virsh setvcpus <vm-name> <number-of-cpus>

# Change memory allocation
virsh setmaxmem <vm-name> <memory-size>
```

Replace `<vm-name>` with the name of your virtual machine, `<number-of-cpus>` with the desired number of CPUs, and `<memory-size>` with the desired memory size (e.g., 4096M for 4 GB).

### Storage Configuration

KVM supports various storage options, including file-based disk images, physical storage devices (LUNs), and networked storage (iSCSI, NFS). You can configure storage during virtual machine creation or add/remove storage devices later using `virt-manager` or `virsh`.

To add a new disk to a virtual machine using `virsh`, run the following command:

```bash
virsh attach-disk <vm-name> <source-path> <target-device> --persistent
```

Replace `<vm-name>` with the name of your virtual machine, `<source-path>` with the path to the disk image or device, and `<target-device>` with the target device name (e.g., vda, vdb).

### Network Configuration

KVM supports various network configurations, including bridged networking, NAT (Network Address Translation), and virtual networks. You can configure network settings during virtual machine creation or modify them later using `virt-manager` or `virsh`.

To create a new virtual network using `virsh`, run the following command:

```bash
virsh net-define <network-xml-file>
```

Replace `<network-xml-file>` with the path to an XML file defining your network configuration.

### Snapshots and Live Migration

KVM supports taking snapshots of virtual machines, which can be useful for backup or rollback purposes. You can create and manage snapshots using `virt-manager` or the `virsh` tool.

To create a snapshot of a virtual machine using `virsh`, run the following command:

```bash
virsh snapshot-create-as <vm-name> <snapshot-name> <description>
```

Replace `<vm-name>` with the name of your virtual machine, `<snapshot-name>` with a name for the snapshot,