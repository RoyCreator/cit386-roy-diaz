# Virtual Machine Build Log

**Student:** Roy Diaz  
**Course:** CIT 386  
**Module:** 01  

## Host Computer

| Setting | Value | Reason / Notes |
|---|---|---|
| Make and Model | Apple MacBook Air | This is the physical computer hosting the virtual machine. |
| Model Identifier | Mac15,12 | Identifies the MacBook Air hardware model without exposing the device serial number. |
| Processor | Apple M3 | The Apple M3 supports virtualization and is capable of running an ARM64 Linux virtual machine. |
| Host CPU | 8 cores: 4 performance cores and 4 efficiency cores | Provides sufficient processing resources for macOS and the virtual machine. |
| Total Memory | 16 GB | Provides enough memory to assign 4 GB to Kali while keeping sufficient RAM available for macOS. |
| Virtualization Setting | Already available through Apple Silicon virtualization | Apple Silicon provides hardware virtualization support without requiring a traditional BIOS or UEFI virtualization switch to be manually enabled. |

## Guest Virtual Machine Settings

| Setting | Value | Reason |
|---|---|---|
| VM Name | `KALI` | The name clearly identifies the virtual machine as the Kali Linux environment. |
| Guest Operating System | Kali Linux | Kali Linux provides a Linux environment for command-line, networking, and security practice. |
| Architecture | ARM64 (aarch64) | ARM64 is appropriate for the Apple M3 host architecture and avoids unnecessary cross-architecture emulation. |
| Virtualization Software | UTM with QEMU 10.0 ARM Virtual Machine | UTM provides the virtualization environment used to run the Kali Linux guest on macOS. |
| Memory | 4096 MiB (4 GB) | Four gigabytes provides enough memory for Kali Linux coursework while leaving approximately 12 GB available to the host operating system. |
| CPU | Default | The default CPU configuration is sufficient for the Kali Linux workload and avoids unnecessary manual CPU configuration. |
| Processor Count | 4 CPU cores | UTM uses the Apple Silicon performance-core count when the CPU core setting is left at Default. The MacBook Air has four performance cores. |
| Virtual Disk Size | 24.09 GB | This provides enough storage for Kali Linux, applications, updates, and course files without assigning excessive host storage. |
| Disk Format | QCOW2 | QCOW2 is the virtual disk format used by QEMU and UTM and supports sparse storage allocation. |
| Disk Allocation | Dynamically allocated / sparse | Physical host storage is consumed as data is written rather than reserving the entire virtual disk capacity immediately. |
| Network | Shared Network (`virtio-net-pci`) | Shared networking provides internet and network access through the host without requiring a more complicated network configuration. |

## Guest Disk File

The Kali Linux virtual disk is stored at:

`/Users/roydiaz/Library/Containers/com.utmapp.UTM/Data/Documents/KALI.utm/Data/731DF9C4-3BD8-4C76-BAB2-E773801F6B06.qcow2`

### Disk Information

| Item | Value |
|---|---|
| Disk Format | QCOW2 |
| Configured Virtual Disk Size | 24.09 GB |
| Current Host Storage Used | Approximately 20 GB |
| Apparent QCOW2 File Size | Approximately 31 GB |
| Allocation Type | Dynamically allocated / sparse |

The `du -h` command showed that the disk currently consumes approximately 20 GB of physical storage on the Mac.

The configured virtual disk capacity shown in UTM is 24.09 GB. The QCOW2 file is sparse, so the amount of physical host storage consumed does not have to match the apparent size of the virtual disk file.

The `ls -lh` command reported an apparent QCOW2 file size of approximately 31 GB, while `du -h` reported approximately 20 GB of actual host storage usage. This demonstrates that the virtual disk uses sparse allocation.

## Problem Encountered

While documenting the virtual disk, my first attempt to check the disk size did not work because I entered the placeholder text `PASTE-THE-DISK-PATH-HERE` instead of the actual path.

The terminal returned:

`No such file or directory`

I corrected the problem by locating the real Kali QCOW2 disk file with the `find` command and then running `ls -lh` and `du -h` using the complete disk path.

After using the correct path, I was able to verify both the apparent file size and the actual amount of host storage being consumed.

## Conclusion

The Kali Linux virtual machine is hosted on an Apple M3 MacBook Air with 16 GB of memory. The guest is configured with 4 GB of RAM, four effective CPU cores, ARM64 architecture, shared networking, and a dynamically allocated QCOW2 virtual disk.

Recording these settings makes it possible for another person to understand how the virtual machine was configured and reproduce a similar environment without needing access to the original computer.