# Lecture 02 – Virtualization

**Course:** T-401-ICYB – Introduction to Cyber Security  
**Lecture:** 02 – Virtualization  
**Date:** 24 November 2026  
**Lecturer:** Stephan Schiffel

---

## 1. What Is Virtualization?

Virtualization is a technology that allows physical computing resources to be divided into virtual resources.

Instead of using one physical computer for only one operating system or workload, virtualization allows multiple virtual machines or isolated environments to share the same physical hardware.

**Key idea:** Virtualization abstracts physical resources so they can be shared, managed and replicated through software.

### Example: Apartment Building

A physical server can be compared to a large apartment building:

- The building represents the physical server.
- Each apartment represents a virtual machine.
- Each apartment has its own space and resources.
- All apartments share the same underlying building.

### Why Use Virtualization?

| Benefit | Explanation |
|---|---|
| Isolation | Keeps crashes and some security problems contained within a VM. |
| Sandboxing | Allows unknown software or files to be tested in a controlled environment. |
| Multi-tenancy | Allows multiple users or organizations to share physical hardware while keeping workloads separated. |
| Resource utilization | Allows hardware resources to be used more efficiently. |
| Cost savings | Reduces the need for separate physical computers. |
| Flexibility | Makes it easier to create, copy, move and remove environments. |

**Cybersecurity connection:** Virtual machines can be used as isolated environments for safely investigating suspicious files or testing software.

---

## 2. Virtualization Terminology

### Host Machine / Host OS

The host is the physical computer that provides the hardware resources.

The host operating system is the operating system installed directly on the physical machine when using a hosted hypervisor.

### Guest Machine / Guest OS

A guest is a virtual computer running inside the host environment.

A virtual machine can have its own:
- Virtual CPU.
- Virtual RAM.
- Virtual disk.
- Virtual network interface.
- Operating system.

The guest behaves like a separate computer, even though it shares the physical hardware with other guests.

### Hypervisor (Virtual Machine Monitor)

A hypervisor is software that creates, runs and manages virtual machines.

It acts as an intermediary between virtual machines and physical hardware.

Examples:
- VMware ESXi.
- Microsoft Hyper-V.
- Oracle VirtualBox.
- VMware Workstation.
- KVM.

### Orchestrator

An orchestrator automates the deployment, scaling and networking of containers across systems.

**Example:** Kubernetes manages containerized applications across multiple machines.

---

## 3. Types of Hypervisors

There are two main types of hypervisors.

### Type 1 – Bare-Metal Hypervisor

A Type 1 hypervisor runs directly on physical hardware without requiring a conventional host operating system underneath it.

Examples:
- VMware ESXi.
- Microsoft Hyper-V.
- Citrix XenServer.
- KVM (commonly classified as Type 1).

**Advantages:**
- Designed for virtualization.
- Commonly used in servers and data centres.
- Does not depend on a conventional desktop host OS layer.

**Security consideration:** A vulnerability in the hypervisor can potentially affect multiple virtual machines running on the same host.

### Type 2 – Hosted Hypervisor

A Type 2 hypervisor runs as an application on top of a normal operating system.

Examples:
- Oracle VirtualBox.
- VMware Workstation.

**Advantages:**
- Easy to install on an ordinary computer.
- Useful for learning, testing and development.

**Security consideration:** The host operating system is part of the trusted computing environment. A compromise of the host can affect the virtual machines.

### Type 1 vs. Type 2

| Feature | Type 1 | Type 2 |
|---|---|---|
| Runs on | Physical hardware | Host operating system |
| Common use | Servers and data centres | Personal computers and testing |
| Examples | ESXi, Hyper-V, Xen | VirtualBox, VMware Workstation |
| Main security concern | Hypervisor vulnerabilities | Host OS and hypervisor vulnerabilities |

---

## 4. Virtualization Methods

### Full Virtualization

The hypervisor provides virtual hardware to the guest operating system.

The guest OS can run without being modified because it behaves as if it has access to normal hardware.

**Advantages:**
- Good compatibility.
- Guest operating systems usually do not need modification.

**Disadvantages:**
- Can introduce performance overhead.
- Uses additional CPU and RAM resources.

### Hardware-Assisted Virtualization

Modern CPUs include special virtualization features that help the hypervisor run virtual machines efficiently.

Examples:
- Intel VT-x.
- AMD-V.

These features allow the processor to handle certain virtualization operations more efficiently.

### Paravirtualization

In paravirtualization, the guest operating system is aware that it is running in a virtualized environment.

It communicates with the hypervisor using special calls called **hypercalls**.

**Key idea:** The guest OS and hypervisor cooperate to improve performance.

**Disadvantages:**
- May require a modified guest OS or special drivers.
- Can reduce compatibility.

### OS-Level Virtualization (Containers)

Containers isolate applications while sharing the host operating system's kernel.

Examples:
- Docker.
- Podman.
- LXC.
- Apple Container.

**Advantages:**
- Containers start quickly.
- They are lightweight compared with full virtual machines.
- Container images can be moved between compatible systems.

**Disadvantages:**
- Containers share the host kernel.
- A kernel vulnerability can affect multiple containers.
- Containers generally need a compatible host kernel.

### Emulation

Emulation simulates an entire hardware platform, potentially including a different CPU architecture.

This allows software designed for one type of hardware to run on another.

**Example:** Running software designed for an ARM system on an x86 computer through emulation.

**Disadvantage:** Emulation can be slower because instructions may need to be translated.

### Comparison of Virtualization Methods

| Method | Main idea | Main advantage | Main disadvantage |
|---|---|---|---|
| Full virtualization | Simulates hardware | Guest OS does not need modification | Performance overhead |
| Hardware-assisted | Uses CPU virtualization features | Better performance | Requires CPU support |
| Paravirtualization | Guest cooperates with hypervisor | Efficient communication | Compatibility requirements |
| Containers | Shares host kernel | Lightweight and fast | Shared-kernel risk |
| Emulation | Simulates another hardware platform | Supports different architectures | High performance overhead |

---

## 5. Security Issues in Virtualization

Virtualization provides isolation, but it also introduces new security risks.

Multiple virtual machines or containers share physical resources. A vulnerability in a shared component may therefore affect several workloads.

### VM Escape / Container Escape

A VM escape occurs when an attacker breaks out of a virtual machine and gains access to the host system.

A container escape occurs when an attacker breaks out of the container's isolation and accesses the host or other resources.

**Example from the lecture:** CVE-2024-21626 affected `runc`, a container runtime. A file descriptor handling issue could expose the host filesystem.

### Hypervisor Vulnerabilities

The hypervisor is a critical component because it manages the virtual machines.

If an attacker exploits a hypervisor vulnerability, they may be able to access or affect multiple guests.

Lecture examples:
- XSA-523: A Xen security advisory concerning unauthorized access to other domains' memory.
- XSA-509: A Xen security advisory concerning a memory leak that could cause denial of service.

### Resource Exhaustion

Resource exhaustion happens when one guest consumes too many shared resources.

Examples:
- Excessive CPU usage.
- Excessive memory consumption.
- Too much disk usage.
- Network bandwidth exhaustion.

This can slow down or disrupt other virtual machines on the same host.

### Management Plane Attacks

The management plane is used to control and administer virtualized infrastructure.

It is a high-value target because administrators can often create, modify, access and delete virtual machines through it.

Lecture examples:
- CVE-2023-34048: A VMware vCenter Server vulnerability involving an out-of-bounds write.
- CVE-2024-37085: A VMware ESXi authentication and Active Directory group authorization issue.

**Security lesson:** Management interfaces must be protected with strong authentication, restricted access and regular security updates.

### Insecure Images and Templates

Virtual machine images and container images can contain vulnerabilities or malicious software before they are deployed.

If an organization uses a compromised image, every system created from that image may inherit the problem.

Lecture example:
- CVE-2024-3094: The XZ Utils backdoor incident demonstrated how malicious code could enter a software supply chain through an upstream software release.

**Security lesson:** Images should come from trusted sources and be checked before deployment.

---

## 6. Side-Channel Attacks

A side-channel attack uses information leaked through the physical behaviour of a system rather than directly exploiting a traditional software vulnerability.

Examples of information that may leak:
- CPU cache activity.
- Branch prediction behaviour.
- Memory access patterns.
- Execution timing.
- Shared hardware resources.

### Why Are Side Channels a Virtualization Problem?

Virtual machines may be logically isolated, but they can share physical hardware.

An attacker running on the same physical machine may be able to observe shared hardware behaviour and infer information about another workload.

This is especially important in cloud environments, where customers may share physical infrastructure with other customers.

### Examples from the Lecture

| Vulnerability | Component | Main issue |
|---|---|---|
| CVE-2022-40982 (Downfall) | CPU | Information leakage involving Intel CPU vector instructions and shared hardware state. |
| CVE-2023-4969 (LeftoverLocals) | GPU | GPU local memory could expose information from another kernel or application. |
| CVE-2015-2877 | Hypervisor environment | A memory deduplication-related side-channel could reveal information about a neighbouring workload. |

**Important:** Side-channel attacks may leak information without directly modifying another system's data or causing a crash.

### Further Research

Compare:
- Meltdown.
- Spectre.
- Downfall.

Questions:
1. What shared hardware behaviour does each attack exploit?
2. What information can potentially be recovered?
3. Why does hardware sharing make isolation more difficult?

---

## 7. Security Comparison of Virtualization Methods

The lecture compares virtualization methods by considering their shared attack surface.

| Environment | Security consideration |
|---|---|
| Physical machines | Separate physical hardware provides stronger hardware separation, but systems still need security controls. |
| Type 1 hypervisor | A hypervisor vulnerability can affect multiple guests. |
| Type 2 hypervisor | The host OS and hypervisor are both part of the trusted environment. |
| Containers | Containers share the host kernel, creating a shared-kernel risk. |
| Emulation | Security depends on the emulator and its configuration. |

No virtualization method automatically guarantees complete security.

The correct choice depends on:
- Required isolation.
- Performance.
- Compatibility.
- Workload type.
- Threat model.
- Available security controls.

---

## 8. Mitigating Virtualization Security Risks

Virtualized environments need security controls at several levels.

### Patch Management

Keep the following updated:
- Hypervisors.
- Host operating systems.
- Guest operating systems.
- Container runtimes.
- Container images.
- Applications.

### Secure Configuration

Apply the principle of least privilege.

Other measures:
- Disable unused services and features.
- Close unnecessary ports.
- Enforce strong authentication.
- Restrict administrative access.

### Network Segmentation

Separate different types of network traffic.

For example:
- Management network.
- Guest virtual machine network.
- Host network.
- Application network.

Segmentation helps prevent an attacker from moving easily between different parts of an environment.

### Secure Image and Template Management

- Use trusted image sources.
- Scan images for known vulnerabilities.
- Keep images updated.
- Verify image integrity where possible.
- Avoid deploying unnecessary software.

### Monitoring and Logging

Monitor systems for:
- Unusual resource usage.
- Suspicious network connections.
- Unexpected administrative activity.
- Attempts to escape virtualized environments.
- Unexpected changes to virtual machine configurations.

### Hardening

**Guest hardening:** Secure the operating system and applications inside the VM or container.

**Host hardening:** Secure the physical machine, host OS and hypervisor.

Both are necessary.

---

## 9. Running a Virtual Machine

A virtual machine consists of several important components.

### VM Components

| Component | Purpose |
|---|---|
| Disk image | Stores the guest's partitions, filesystems and data. |
| Configuration | Defines virtual CPUs, RAM, devices and network settings. |
| Firmware state | Stores UEFI variables and boot configuration. |
| Memory state | Stores the guest's RAM and device state when paused or saved. |

### Virtual Disks

A virtual disk is stored as a file on the host.

It represents the blocks, partitions and filesystems that would normally exist on a physical disk.

Common disk formats:

| Format | Common association |
|---|---|
| RAW | Unstructured raw disk image |
| QCOW2 | QEMU |
| VMDK | VMware |
| VDI | VirtualBox |

### Converting Disk Images

The lecture gives this example:

```bash
qemu-img convert -f vmdk -O qcow2 disk.vmdk disk.qcow2
```

Explanation:
- `qemu-img`: Tool for managing disk images.
- `convert`: Converts one disk image format into another.
- `-f vmdk`: Specifies the input format.
- `-O qcow2`: Specifies the output format.
- `disk.vmdk`: Input file.
- `disk.qcow2`: Output file.

### Sparse Files

A sparse disk image does not necessarily use all the space that its maximum virtual size suggests.

For example, a virtual disk with a maximum capacity of 20 GB might use only 2 GB of physical storage if most of it is empty.

---

## 10. Virtual Machine Snapshots

A snapshot records the state of a virtual machine at a particular point in time.

### Disk Snapshot

A disk snapshot preserves previous disk blocks while new writes are stored separately in a new layer or delta.

This allows the VM to return to an earlier disk state.

### Memory Snapshot / Saved State

A memory snapshot saves the VM's RAM and device state.

It allows the VM to resume close to exactly where it stopped.

### Crash-Consistent Snapshots

A snapshot of a running guest may represent a state similar to suddenly cutting power if the guest has not been instructed to flush pending data.

This can cause filesystem or application consistency problems.

### Important: A Snapshot Is Not a Backup

A snapshot is not a replacement for a backup.

Reasons:
- It may be stored on the same physical disk as the VM.
- Disk corruption can affect both the VM and its snapshot.
- Restoring a snapshot rolls the VM back to an earlier state.
- It does not repair the underlying problem.

**Remember:** Restore means rollback, not repair.

---

## 11. Where Does a Virtual Machine's Memory Exist?

The guest's memory is managed by the host and hypervisor.

| VM state | Where memory may be stored |
|---|---|
| Running | Physical RAM and potentially host-backed memory files. |
| Paused or saved | Saved-state file on the host. |
| Host swapping | Some guest memory pages may be stored in the host's swap space. |
| Guest swapping | Guest memory pages may be stored inside the guest's virtual disk. |

### Security Implication

The host and hypervisor have access to the resources used by the guest.

An attacker with sufficient control of the host may be able to inspect guest memory.

Memory may contain:
- Passwords.
- Encryption keys.
- Authentication tokens.
- Running processes.
- Other sensitive information.

**Connection to Lab 2:** The lecture explains that a flag can be hidden in a running VM's memory rather than on its disk. This is why memory acquisition and analysis are relevant.

---

## 12. Containers

A container is an isolated process running on the host operating system's kernel.

Unlike a full VM, a container does not normally run its own independent kernel.

### Main Container Components

| Component | Explanation |
|---|---|
| Filesystem | Uses an image, writable layer and possibly folders mounted from the host. |
| Network | Uses virtual network interfaces, IP addresses and ports. |
| Users | Has user and group IDs. A process may appear to be root inside the container. |
| Control groups (cgroups) | Limit resources such as CPU and memory. |

### Containers vs. Virtual Machines

| Feature | Virtual Machine | Container |
|---|---|---|
| Kernel | Usually has its own guest OS kernel | Shares the host kernel |
| Isolation | Generally stronger OS-level separation | Process and namespace isolation |
| Startup | Usually slower | Usually faster |
| Resource usage | Higher | Lower |
| Main security concern | Hypervisor and guest vulnerabilities | Shared kernel and container configuration |

**Important:** Being root inside a container does not necessarily mean being root on the host. However, incorrect permissions and configuration can create serious security risks.

---

## 13. Running a Container Example

The lecture demonstrates running a container with Podman.

A cleaned-up example:

```bash
podman run -it --name demo-app \
  --volume ./data:/app/data:Z \
  --network my-net --ip 10.89.0.42 \
  --publish 8080:80 \
  --user 1001:1001 \
  --memory 256m --cpus 0.5 \
  docker.io/library/alpine:latest sh
```

### Explanation

| Option | Purpose |
|---|---|
| `podman run` | Creates and starts a container. |
| `-it` | Runs interactively with a terminal. |
| `--name demo-app` | Gives the container a name. |
| `--volume` | Mounts a host directory into the container. |
| `:Z` | Applies a private SELinux label to the mounted volume on supported systems. |
| `--network` | Selects the container network. |
| `--ip` | Assigns a static internal IP address, if supported by the network configuration. |
| `--publish 8080:80` | Maps host port 8080 to container port 80. |
| `--user 1001:1001` | Runs the process with the specified user and group IDs. |
| `--memory 256m` | Limits memory to 256 MB. |
| `--cpus 0.5` | Limits CPU usage to half a CPU. |
| `docker.io/library/alpine:latest` | Specifies the container image. |
| `sh` | Starts a shell inside the container. |

**Security lesson:** Container configuration matters. Resource limits, user permissions, mounted folders and network settings can all affect security.

---

## 14. Lab 2 – Virtual Machine and Memory Analysis

The lecture introduces Lab 2, which involves running a supplied virtual machine.

Main tasks:
1. Download the provided VM image.
2. Run it using a hypervisor.
3. Convert the disk image if the hypervisor requires another format.
4. Find a flag hidden in the running VM's memory.
5. Acquire and inspect the memory from the host.

### Searching Memory for Text

The lecture introduces the `strings` and `grep` commands.

Example:

```bash
strings mem.dump | grep -i "flag"
```

Explanation:
- `strings`: Extracts readable text from binary data.
- `mem.dump`: The memory image being examined.
- `|`: Sends the output of one command to another.
- `grep`: Searches text for a matching pattern.
- `-i`: Makes the search case-insensitive.

**Important:** Text inside a memory dump is not necessarily indexed like text in a normal document. Extracting readable strings can make it easier to find relevant information.

Memory analysis can reveal information that is not present in the virtual machine's disk image.

---

## 15. Lab 2 – SSH and Key Pairs

SSH (Secure Shell) is a protocol used to access a remote computer through an encrypted connection.

It allows a user to:
- Open a remote shell.
- Execute commands on another machine.
- Transfer files securely.
- Authenticate using passwords or cryptographic keys.

### SSH Key Pair

An SSH key pair consists of two related keys.

**Public key:**
- Can be shared.
- Usually stored in a file ending in `.pub`.
- Installed on the remote machine to allow authentication.

**Private key:**
- Must remain secret.
- Should never be shared.
- Is used to prove that the user controls the matching public key.

### How Public-Key Authentication Works

1. The user connects to a remote server.
2. The server checks whether the user's public key is authorized.
3. The server sends an authentication challenge.
4. The user's SSH client uses the private key to produce the required cryptographic proof.
5. The server verifies the proof using the public key.
6. If verification succeeds, access is granted.

**Important:** The private key should never be uploaded to GitHub or shared with other people.

### Why Use SSH Keys Instead of Only Passwords?

SSH keys allow authentication without sending a shared password over the connection.

They also provide a strong way to prove possession of the private key.

---

## 16. Important Commands

| Command | Purpose |
|---|---|
| `qemu-img info disk.qcow2` | Displays information about a virtual disk image. |
| `qemu-img convert -f vmdk -O qcow2 disk.vmdk disk.qcow2` | Converts a VMDK disk image to QCOW2. |
| `strings mem.dump` | Extracts readable strings from a memory dump. |
| `strings mem.dump \| grep -i "flag"` | Searches extracted strings for the word `flag`. |
| `podman run` | Creates and starts a container. |
| `ssh user@host` | Connects to a remote machine using SSH. |

---

## 17. Further Research and Discussion Questions

### Side-Channel Attacks

1. What is the difference between Meltdown, Spectre and Downfall?
2. How can shared CPU resources leak information between virtual machines?
3. Why are side-channel attacks difficult to detect using normal security logs?
4. What security trade-offs are involved when disabling hardware-sharing features?

### Container Image Security

1. Can a container image be compromised before it is deployed?
2. How can organizations verify where an image came from?
3. What do image signatures and provenance provide?
4. Why is version pinning useful?
5. Can vulnerability scanning detect every type of malicious code?

### Virtualization Security

1. What is the difference between a VM escape and a container escape?
2. Why is the hypervisor an important security boundary?
3. Why should management interfaces be isolated from ordinary guest networks?
4. Why is a VM snapshot not a complete backup?
5. What types of sensitive information might exist in a memory dump?

---

## 18. Connections to Lecture 01 – Introduction to Cyber Security

The virtualization concepts connect directly to the security principles introduced in Lecture 01.

| Lecture 01 concept | Connection to Lecture 02 |
|---|---|
| Attack surface | Hypervisors, containers and management interfaces introduce additional attack surfaces. |
| Least privilege | Containers and virtual machines should run with only the permissions they need. |
| Defense in depth | Virtualized environments need multiple layers of protection. |
| Confidentiality | Side-channel attacks and memory inspection can expose sensitive information. |
| Integrity | Compromised VM or container images can introduce malicious changes. |
| Availability | Resource exhaustion can disrupt multiple guests on the same host. |
| CVE and CVSS | Virtualization vulnerabilities can be identified and assessed using CVE and CVSS. |
| Malware | Virtual machines can provide controlled environments for investigating suspicious software. |

---

## 19. Key Takeaways

- Virtualization allows multiple isolated environments to share physical hardware.
- A host provides resources, while guests run virtual operating systems.
- A hypervisor creates and manages virtual machines.
- Type 1 hypervisors run directly on hardware; Type 2 hypervisors run on a host OS.
- Containers share the host kernel, unlike traditional virtual machines.
- Emulation allows software designed for one hardware architecture to run on another.
- VM escapes and container escapes can break isolation.
- Side-channel attacks can leak information through shared hardware without directly modifying another guest's data.
- Hypervisors, hosts, guests and container images all need security updates.
- Virtual machine snapshots are not replacements for backups.
- Guest memory can contain sensitive information accessible from the host.
- `strings` and `grep` can help search memory dumps.
- SSH uses public and private keys for secure authentication.
- Private SSH keys must never be shared or committed to GitHub.

---

## 20. References and Further Reading

### Lecture Slides

**L02 – Virtualization (PDF)**

Course lecture slides, T-401-ICYB, Reykjavík University, 24 November 2026.

[Download L02-virtualization.pdf](https://reykjavik.instructure.com/courses/10481/files/2822778/download?download_frd=1)

Relevance: Main source for the concepts, terminology, examples and security issues discussed in this lecture.

### Recommended Reading

| Resource | Description | Relevance to the course |
|---|---|---|
| [VirtualBox User Manual](https://www.virtualbox.org/manual/) | Official documentation for Oracle VirtualBox, including creating and managing virtual machines. | Helps understand Type 2 hypervisors and practical VM configuration. |
| [QEMU – qemu-img Documentation](https://www.qemu.org/docs/master/tools/qemu-img.html) | Official documentation for managing, inspecting and converting virtual disk images. | Useful for understanding virtual disk formats and the disk conversion commands used in Lab 2. |
| [Red Hat – What Is Virtualization?](https://www.redhat.com/en/topics/virtualization/what-is-virtualization) | Introduction to virtualization concepts, benefits and technologies. | Provides additional explanations of virtualization and its practical applications. |
| [VirtualBox – Virtual Storage and Disk Image Formats](https://www.virtualbox.org/manual/topics/storage.html) | Explains virtual storage, virtual disks and supported storage formats in VirtualBox. | Helps understand virtual disk images, storage configuration and VM disk management. |

### Additional Cybersecurity References

| Resource | Description | Relevance to the course |
|---|---|---|
| [CVE – Common Vulnerabilities and Exposures](https://www.cve.org/) | Database of publicly identified cybersecurity vulnerabilities. | Helps identify vulnerabilities affecting hypervisors, containers and virtualization software. |
| [NIST National Vulnerability Database](https://nvd.nist.gov/) | Provides vulnerability information, CVSS scores and technical details. | Useful for assessing the severity of virtualization-related vulnerabilities. |
| [Xen Security Advisories](https://xenbits.xen.org/xsa/) | Security advisories concerning vulnerabilities in the Xen hypervisor. | Provides examples of real hypervisor security issues. |
| [QEMU Documentation](https://www.qemu.org/docs/master/) | Official documentation for QEMU virtualization and emulation. | Useful for understanding virtual machines, emulation and disk management. |
| [Podman Documentation](https://docs.podman.io/) | Official documentation for Podman container management. | Supports the container commands and configuration discussed in the lecture. |
| [OpenSSH Manual](https://www.openssh.com/manual.html) | Official documentation for OpenSSH and secure remote access. | Useful for understanding SSH and public-key authentication. |

### Keywords

`Virtualization` · `Hypervisor` · `Virtual Machine` · `Type 1` · `Type 2` · `Containers` · `QEMU` · `VirtualBox` · `Disk Images` · `Snapshots` · `VM Escape` · `Side-Channel Attacks` · `SSH` · `Memory Analysis` · `Podman`

---

**Study note:** These notes summarize Lecture 02 and its recommended reading. The original lecture slides and official documentation should be used when checking exact technical details, vulnerability descriptions and affected software versions.
