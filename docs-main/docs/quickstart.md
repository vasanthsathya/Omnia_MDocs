---
hide:
- toc
---

# Quickstart


!!! note "Verity EULA Acceptance"

    Use of this the Verity software requires acceptance of the [EULA](eula.md).

**Verity Quickstart has four steps.**  Upon completing these steps, the administrator will have an operational network fabric with a working underlay network and can begin adding tenants.

   1. **Verity Installation** — VMware, KVM, Proxmox, or GNS3 (lab).
   1. **Initial Setup**
      1. Import an inventory file (FDC*.csv). [An *example* FDC inventory import file is available in Downloads](downloads.md).
      1. Set up DHCP server and install SONiC images into the platform.
   1. **Underlay Settings** — provision the underlay network and reserved ranges.
   1. **Onboarding Devices** — power up and connect the SONiC devices. Use bulk FDC import or manual onboarding as needed.