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

## Deployment Model Comparison

### On-Premises Deployment

With an on-premises deployment, the application and its data would be stored on a server located inside the repair shop.

**Advantages:**

- Direct control over the server and data.
- Ability to customize the hardware.
- Local access that may continue if the internet connection fails.

**Disadvantages:**

- High initial hardware costs.
- Responsibility for maintenance and security.
- Manual backup requirements.
- Risk of data loss from theft, fire, flooding, or hardware failure.
- Difficulty supporting remote access and business growth.

### Public Cloud Deployment

With a public cloud deployment, the application and its data would run through a provider such as Amazon Web Services, Microsoft Azure, or Google Cloud.

**Advantages:**

- Lower initial hardware costs.
- Access from different locations.
- Automated backup and recovery options.
- Easier expansion as the business grows.
- Provider-managed infrastructure.
- Usage-based pricing.

**Disadvantages:**

- Dependence on an internet connection.
- Continuing monthly expenses.
- Possible unexpected charges if resources are not monitored.
- Security and permissions must be configured correctly.

### Hybrid Deployment

A hybrid deployment combines local technology with public cloud services. For example, the shop could keep diagnostic tools and temporary repair files on local computers while storing customer records, repair tickets, and backups in the cloud.

**Advantages:**

- Flexibility in deciding where information is stored.
- Cloud backups for important business records.
- Local access to tools that do not require the internet.
- Better support for different types of workloads.

**Disadvantages:**

- More complicated administration.
- Both local and cloud systems must be secured.
- Possible data synchronization problems.
- Higher support requirements than a cloud-only system.

## Recommended Deployment Model

The recommended deployment model is the public cloud.

A public cloud solution is appropriate because the repair shop may not have the budget or employees necessary to maintain its own server. The cloud would allow employees to access repair tickets and customer records from authorized devices without purchasing expensive server equipment.

Cloud services also provide backup, recovery, monitoring, and scalability options. If the business hires additional technicians or opens another location, the system can expand without replacing the entire infrastructure.

The company should use multifactor authentication, strong passwords, role-based access control, encryption, automated backups, and activity logging. Employees should only receive access to the information necessary for their jobs.

## Conclusion

A cloud-based repair ticket and customer management system would help the PC building and repair shop organize its daily operations. Compared with on-premises and hybrid deployment, the public cloud offers the best balance of cost, accessibility, reliability, recovery, and scalability.

The final solution should protect customer information while allowing technicians to manage repairs efficiently from authorized devices.