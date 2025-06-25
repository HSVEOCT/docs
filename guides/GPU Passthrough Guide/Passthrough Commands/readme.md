## Optional Steps

_This step is not necessary for the passthrough, but helps keeping things clean._

For ignoring some annoying “warnings” in your `dmesg` output, do the following:

```bash
nano /etc/modprobe.d/kvm.conf
```

Add the following line:

```bash
options kvm ignore_msrs=Y report_ignored_msrs=0
```

Hit **Ctrl + X → Y → Enter** to save changes.

## Setting the Boot Arguments

### For **Intel** CPUs

For **GRUB**;  
Replace the current similar line with this one in your grub file:

```bash
nano /etc/default/grub
```

_Make these changes to that file:_

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt initcall_blacklist=sysfb_init"
```

Hit **Ctrl + X → Y → Enter** to save changes.

---

### For **AMD** CPUs

For **GRUB**;  
Replace the current similar line with this one in your grub file:

```bash
nano /etc/default/grub
```

_Make these changes to that file:_

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet iommu=pt initcall_blacklist=sysfb_init"
```

Hit **Ctrl + X → Y → Enter** to save changes.

---

Your system might not be relying on Grub, but **systemd** instead.  
This is often the case when you’re using **ZFS**.  
So for **systemd**;

# Intel CPUs (Systemd)

```
nano /etc/kernel/cmdline
```

```bash
root=ZFS=rpool/ROOT/pve-1 boot=zfs intel_iommu=on iommu=pt initcall_blacklist
=sysfb_init
```

# AMD CPUs (systemd)

```
nano /etc/kernel/cmdline
```

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet iommu=pt initcall_blacklist=sysfb_init"
```
