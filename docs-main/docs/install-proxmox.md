---
hide:
- toc
---

# Proxmox Configuration

**1. Copy vNetC and SDLC vma files to host:**

- Copy the the virtual machines (VMs) files to your Proxmox host. These are:
  - ```vzdump-qemu-vnc-x.x.x.x.vma.zst```: This is the backup for the **vNetC** VM.
  - ```vzdump-qemu-SDLC_x.x.x.x.vma.zst```: This is the backup for the **SDLC** VM.
  - ```vzdump-qemu-verity-satori.x.x.x.vma.zst```: This is the backup for the **Satori** VM.

**2. List VMIDs in Use:**

In Proxmox, each VM has a unique identifier called a VMID. To view the full list of VMIDs currently in use on your Proxmox server, run the following command:

```qm list```

**3. Add the VMs and Assign Each an Unused VMID**

After checking which VMIDs are already in use, select an *unused* VMID for each VM. Use the ```qmrestore``` command to restore the backups. For example:

- For vnetc, if VMID 110 is free, you restore it with: ```qmrestore vzdump-qemu-vnc-6.3.0.3509.vma.zst 110```

- For SDLC, if VMID 111 is free, you restore it with: ```qmrestore vzdump-qemu-SDLC_6.3.0.1.D20.vma.zst 111```

- For Satori, if VMID 112 is free, you restore it with: ```qmrestore vzdump-qemu-verity-satori.1.2.18.vma.zst 112```

**4. Edit the CPU, RAM, and Network for each VM:**

Configure the resources for each VM via the Proxmox GUI (web interface).

  - **CPU & RAM**: Set the correct number of CPUs and amount of RAM.
   - **Network Configuration:**

     - **vNetC:** For vNetC, configure the first network adapter (net0) to ensure it is connected to the correct bridge and has the correct VLAN Tag (if using VLAN trunking).
     - **SDLC:** For SDLC, configure the second network adapter (net1) similarly, ensuring it connects to the correct bridge with the correct VLAN Tag.
     - **Satori:** For Satori, configure the only network adapter (net0) to ensure it is connected to the correct bridge and has the correct VLAN Tag.

**5. Start the VMs:**

After configuring the VMs, start them from the Proxmox GUI:
 - Find the vnetc VM and click on "Start".
 - Find the SDLC VM and click on "Start".
 - Find the Satori VM nad click on "Start".

**6. Continue Setup Process for vNetC, SDLC and Satori from Referenced Document(s):**
 
 After starting the VMs, follow the remaining instructions in the separate document(s) (linked below) to complete the setup for the vNetC, SDLC and Satori systems.


Key Steps Simplified:

1. Copy files to your Proxmox host. 
1. List VMIDs to find available IDs.
1. Restore VMs using ```qmrestore``` with available VMIDs.
1. Edit CPU, RAM, and network settings for each VM.
1. Start the VMs.
1. Continue setup from the provided documentation.

### VNetC, SDLC and Satori Configuration

- [Configure the vNetC from the Console](install-kvm.md/#configure-the-vnetc-console)

- [Configure the SDLC from the Console](install-kvm.md/#configure-the-sdlc-console)

- [Configure Satori from the Console](install-vmware.md/#configure-satori-vm-console)
