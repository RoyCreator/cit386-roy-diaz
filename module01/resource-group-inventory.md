# Resource Group Inventory

**Student:** Roy Diaz  
**Course:** CIT 386  
**Module:** 01  
**Resource Group:** `cit386-shared-rg`

## Overview

This document inventories the resources contained in the shared Azure resource group used for CIT 386. The purpose of the inventory is to identify each Azure resource, explain its function, identify dependencies related to the virtual machine, and determine which resources may continue generating charges when the virtual machine is stopped.

The shared environment is deployed in the **East US 2 (Virginia)** region.

## Resource Inventory

| Resource Name | Resource Type | Region | Purpose | Exists Because of VM? |
|---|---|---|---|---|
| `cit386-shared-vm` | Virtual Machine | East US 2 | Provides the compute resources used to run the operating system and workload. | Yes |
| `cit386-shared-vm_OsDisk` | Managed Disk | East US 2 | Stores the operating system and persistent data for the virtual machine. | Yes |
| `cit386-shared-vm-nic` | Network Interface | East US 2 | Connects the virtual machine to the Azure virtual network. | Yes |
| `cit386-shared-ip` | Public IP Address | East US 2 | Provides a public network address that can be used to reach the virtual machine. | Yes |
| `cit386-shared-nsg` | Network Security Group | East US 2 | Controls inbound and outbound network traffic using security rules. | Yes |
| `cit386-vnet` | Virtual Network | East US 2 | Provides the private Azure network used by the virtual machine and its network interface. | Yes |
| `cit386storage` | Storage Account | East US 2 | Provides Azure storage for files, objects, logs, or other persistent information. | No |

## Virtual Machine Dependencies

A virtual machine appears as one item in the Azure portal, but several separate Azure resources are required for it to operate.

The main virtual machine is:

`cit386-shared-vm`

It depends on the following resources:

- `cit386-shared-vm_OsDisk` for operating system storage.
- `cit386-shared-vm-nic` for network connectivity.
- `cit386-vnet` to provide the network where the network interface operates.
- `cit386-shared-ip` to provide public connectivity.
- `cit386-shared-nsg` to control permitted network traffic.

These resources are managed separately even though they work together as part of the virtual machine environment.

## Resources That Can Continue Billing When the VM Is Stopped

Stopping or deallocating a virtual machine can stop its compute charges, but that does not mean the entire Azure environment becomes free.

### `cit386-shared-vm_OsDisk`

The managed operating system disk continues to store data after the virtual machine is stopped.

Azure charges for managed disk storage independently from virtual machine compute usage, so the disk can continue generating charges while the VM is stopped.

### `cit386storage`

The storage account can continue generating charges because stored data remains in Azure even when the virtual machine is not running.

Storage charges depend on factors such as the quantity of data stored, storage tier, and operations performed.

### `cit386-shared-ip`

The public IP address may continue generating charges even when the VM is stopped because public IP resources can be billed independently of VM compute.

The exact charge depends on the type and configuration of the Azure public IP resource.

## Resources That Normally Do Not Have a Direct Compute Charge

The following resources support the environment but do not normally create the same type of direct compute charge as the virtual machine:

- `cit386-shared-vm-nic`
- `cit386-shared-nsg`
- `cit386-vnet`

These resources are still important because they provide network connectivity and security for the workload.

## Resource Group Deletion

If the entire `cit386-shared-rg` resource group is deleted, the resources contained inside it are deleted as part of the same lifecycle operation.

This includes:

- Virtual machine
- Managed operating system disk
- Network interface
- Public IP address
- Network security group
- Virtual network
- Storage account

The `cit386archive` storage account shown in the activity is not part of `cit386-shared-rg`. It belongs to the separate `cit386-archive-rg` resource group and therefore survives deletion of `cit386-shared-rg`.

## Dependency Summary

The basic dependency relationship is:

`cit386-shared-vm`

- uses `cit386-shared-vm_OsDisk`
- connects through `cit386-shared-vm-nic`
- the NIC connects to `cit386-vnet`
- the NIC can use `cit386-shared-ip`
- network traffic is controlled by `cit386-shared-nsg`

The `cit386storage` resource is also located inside the resource group but is not required simply for the virtual machine to exist.

## Conclusion

The Azure virtual machine is not a single independent resource. It relies on several separate compute, storage, networking, and security resources.

The inventory also demonstrates why stopping a virtual machine does not necessarily stop all Azure charges. Persistent resources such as managed disks, storage accounts, and some public IP configurations can remain allocated and continue generating costs.

Understanding these dependencies is important before deleting a resource group because deleting the group can remove every resource and all persistent data contained within it.