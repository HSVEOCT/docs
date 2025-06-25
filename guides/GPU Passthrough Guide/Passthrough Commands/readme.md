## HSVE Proxmox PCI-E Passthrough Guide

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

### Intel CPUs (Systemd/ZFS)

```
nano /etc/kernel/cmdline
```

```bash
root=ZFS=rpool/ROOT/pve-1 boot=zfs intel_iommu=on iommu=pt initcall_blacklist
=sysfb_init
```

### AMD CPUs (Systemd/ZFS)

```
nano /etc/kernel/cmdline
```

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet iommu=pt initcall_blacklist=sysfb_init"
```

---

For **Grub** only

```bash
update-grub
```

For **Systemd** only

```bash
pve-efiboot-tool refresh
```

Reboot to commit changes with:

```bash
reboot
```

**Configuring IOMMU

Once the host is up and running again we need to check if IOMMU is enabled and working. We can do this by running the following commands.

For **Intel**:

```bash
dmesg | grep -e DMAR -e IOMMU
```

For **AMD**:
```bash
dmesg | grep -e DMAR -e IOMMU -e AMD-Vi
```

If there's no output you've done something wrong, please retrace your steps or contact us (Email: support@hsve.cc).

You should be seeing something like this:
"DMAR: IOMMU Enabled"

The next steps is enabling the modules required for GPU passthrough:

Enable the neccesary modules by running the following command:

```bash
nano /etc/modules
```
Add the following lines to this file:
```bash
vfio
vfio_iommu_type1
vfio_pci
```
Hit **Ctrl** + **X** > **Y** **Enter** to Save changes.

After changing the following modules you need to refresh your initramfs with the following command:
```bash
update-initramfs -u -k all
```

Lets check if remapping has been enabled with the following command:
```bash
dmesg | grep remapping
```
You should see something like "Interrupt remapping enabled / IRQ Remapping Enabled"

If your system doesn't support Remapping you can run this command to enable remapping. **However please be aware that this option could make your system unstable.**

```bash
nano /etc/modprobe.d/iommu_unsafe_interrupts.conf
```
Add the following line:
```bash
options vfio_iommu_type1 allow_unsafe_interrupts=1
```
Hit **Ctrl** + **X** > **Y** > **Enter** to save your changes.

---

## Blacklisting driver modules to give VM full access to Hardware.
```bash
nano /etc/modprobe.d/pve-blacklist.conf 
```
```bash
blacklist nouveau
blacklist nvidia
blacklist nvidiafb
blacklist snd_hda_codec_hdmi
blacklist snd_hda_intel
blacklist snd_hda_codec
blacklist snd_hda_core
blacklist radeon
blacklist amdgpu
```
Hit **Ctrl** + **X** > **Y** > **Enter**

# Blacklisting your Devices
To find the corresponding IDs for your PCI devices run the following command:
```bash
lspci -nn | grep -i {device}
```
Replace {device} = vga,usb,audio,wireless etc.

You will see an output similar to the below screenshot: <br></br>
![Screenshot of output- lspci command](<Screenshot 2025-06-25 121951.png>)
<br></br>

As you can see the IDs of my GPU are **10de:1287** and **1002:67d**.

You may decide you want to find the IDs of your USB controllers too just incase you need to whitelist these down the line due to issues.

To blacklist the devices from use by Proxmox and full access use to your VM run the following commands.

```bash
nano /etc/modprobe.d/vfio-pci.conf
```
Add the device IDs in the blank file like this:
```bash
options vfio-pci ids=1234:5678,1234:5678 disable_vga=1
```
Replacing the **1234:5678** with your actual IDs, if you only have 1 GPU remove the other IDs from the command.

***Example:***
```bash
options vfio-pci ids=10de:1287 disable_vga=1
```
You can also add **disable_idle_d3=1** to the end of the line to disable the D3 device power state which will prevent certain hardware from entering low power mode, which can cause issues when passed through to VMs. 

Hit **Ctrl** + **X** > **Y** > **Enter** to save changes.

Once all of the above is sorted reboot your machine once again with the command below:
```bash
reboot
```

# Adding your Devices to your VM(s)
When your host has rebooted we can finally start adding our devices like GPUs to our Virtual Machines! If you're passing through to HSVE macOS watch the following video below to ensure you have the correct settings.

If you're also unsure on how to passthrough devices to your VM please watch our following video : https://youtu.be/uQxYpokYkZs
