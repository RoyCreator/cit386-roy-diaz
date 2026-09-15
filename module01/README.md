# Module 01 – Small-Business Workload Analysis

**Student:** Roy Diaz  
**Course:** CIT 386  
**Business:** PC Building and Repair Shop  

## Business Description

The selected small business is a PC building and repair shop. The company builds custom computers, upgrades existing systems, diagnoses hardware and software problems, removes malware, installs operating systems, and provides technical support.

The business serves individual customers, gamers, students, and small companies. Employees need a reliable system to organize customer information, repair orders, computer specifications, inventory, invoices, and appointments.

## Selected Workload

The selected workload is a web-based repair ticket and customer management system.

The system would allow employees to:

- Create customer profiles.
- Register computers brought in for service.
- Record hardware and software problems.
- Track diagnostic and repair progress.
- Document replacement parts.
- Update repair statuses.
- Prepare invoices.
- Notify customers when their computers are ready.
- Review previous repair history.

This workload is important because losing repair records could cause delays, incorrect repairs, billing problems, and dissatisfied customers.

## Workload Requirements

The repair management system should provide:

- Secure employee authentication.
- Centralized customer and repair records.
- Access from computers and mobile devices.
- Daily automated backups.
- Protection of customer information.
- Reliable availability during business hours.
- Support for additional employees and locations.
- Reasonable operating costs for a small business.
- Recovery options if information is deleted or corrupted.

## Deployment Options

### VirtualBox

VirtualBox is a hosted hypervisor that runs on an existing laptop or desktop computer.

A Linux virtual machine can be created inside VirtualBox without purchasing additional hardware or paying a monthly fee.

**Advantages:**

- Approximately $0 per month.
- Uses the student's existing computer.
- Quick to install and configure.
- Easy to create and delete virtual machines.
- Good for testing and learning.
- The Linux environment can be restarted or recreated if something breaks.

**Disadvantages:**

- Depends on the resources of the host computer.
- The virtual machine is normally available only while the host computer is running.
- Performance may be lower than dedicated hardware.

For this workload, VirtualBox is a strong option because the student only needs a simple Linux environment for practice.

### Hyper-V

Hyper-V is a virtualization platform from Microsoft that can run virtual machines on Windows systems.

It could also be used to create a Linux practice server.

**Advantages:**

- Approximately $0 per month when available on a compatible Windows system.
- Supports Linux virtual machines.
- Good performance.
- Useful for learning virtualization.

**Disadvantages:**

- Requires a compatible version of Windows.
- May require additional configuration.
- Provides no major advantage over VirtualBox for a simple student practice server.

Hyper-V could support this workload, but VirtualBox may be simpler for a basic learning environment.

### Proxmox Host

Proxmox is a bare-metal hypervisor that is normally installed directly on a dedicated computer or server.

It is commonly used to run multiple virtual machines.

**Advantages:**

- Good performance.
- Supports multiple virtual machines.
- Useful for larger virtualization labs.
- Provides centralized management.

**Disadvantages:**

- Requires dedicated hardware.
- The hardware must remain powered on.
- Uses additional electricity.
- More complicated than necessary for one practice Linux server.

Proxmox would work, but it would be excessive for this workload because the student only needs one temporary Linux server.

### Physical PC

A physical PC could be used by installing Linux directly on the hardware.

**Advantages:**

- Full access to the computer's hardware.
- No virtualization overhead.
- Good performance.

**Disadvantages:**

- Requires a separate computer or dedicated hardware.
- Higher hardware and electricity costs.
- Harder to reset compared with a virtual machine.
- Unnecessary for a simple practice environment.

A physical PC is not the best choice because this workload does not require direct access to dedicated hardware.

### Microsoft Azure

Microsoft Azure is a public cloud platform that can provide Linux virtual machines through Microsoft's infrastructure.

**Advantages:**

- Quick deployment.
- Remote access through the internet.
- Easy to increase resources.
- Does not require local server hardware.

**Disadvantages:**

- Creates recurring cloud charges.
- Requires an internet connection.
- More expensive than using an existing computer.
- Cloud scalability is unnecessary for this workload.

Azure could run the Linux server successfully, but the cost would not be justified for a student practice environment.

## Deployment Model Comparison

| Deployment Option | Cost | Setup | Hardware Required | Scalability | Best Fit |
|---|---|---|---|---|---|
| VirtualBox | Very Low | Easy | Existing Computer | Low | Student Practice Lab |
| Hyper-V | Very Low | Moderate | Existing Windows Computer | Moderate | Windows Virtualization |
| Proxmox Host | Moderate | Moderate | Dedicated Computer | High | Multiple Virtual Machines |
| Physical PC | Moderate to High | Moderate | Dedicated Computer | Low | Direct Hardware Access |
| Microsoft Azure | Ongoing Monthly Cost | Easy | No Local Server | High | Cloud Workloads |

## Recommended Deployment Model

The recommended deployment option for this workload is **VirtualBox**.

The Linux server does not need high availability, large amounts of storage, direct hardware access, or significant room for growth.

Cost is the most important requirement because the workload is being used by a student with little or no budget.

VirtualBox is the best choice because it uses an existing computer and does not create recurring cloud charges.

It also allows the student to create, delete, restart, and rebuild the Linux virtual machine easily. This makes it ideal for learning Linux commands and experimenting without risking important information.

## Conclusion

All five deployment options could technically run a Linux server, but they are designed for different situations.

Hyper-V is a good virtualization option for Windows systems, while Proxmox is better for larger virtualization environments. A physical PC provides direct hardware access, and Microsoft Azure provides cloud scalability and remote access.

For a simple Linux practice server, these features are unnecessary.

VirtualBox provides the best combination of low cost, easy setup, flexibility, and recovery. For this reason, VirtualBox is the most appropriate deployment option for the workload.