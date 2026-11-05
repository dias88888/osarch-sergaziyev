# Lab 0 - Inventory

Pair: Sergaziyev (worked alone, no partner took part)
First driver: Sergaziyev
Machine: MacBook Air, Apple M2, macOS (no virtual machine yet)
Date: 05.11.2026, 17:00

## What I did

All values were taken from the terminal only. The graphical "About This Mac" window was not opened.

```bash
sysctl -n machdep.cpu.brand_string
sysctl hw.physicalcpu hw.logicalcpu
system_profiler SPMemoryDataType
sysctl hw.memsize
system_profiler SPStorageDataType SPNVMeDataType
diskutil info /
df -h /
df -h /System/Volumes/Data
system_profiler SPHardwareDataType | grep -i -E "firmware|model"
sysctl kern.hv_support
sysctl machdep.cpu.features
sw_vers; uname -m
```

## Result

| What | Value | Where I got it |
|---|---|---|
| CPU model | Apple M2 | `sysctl -n machdep.cpu.brand_string` |
| Cores / threads | 8 physical / 8 logical (no SMT) | `sysctl hw.physicalcpu hw.logicalcpu` |
| RAM size | 16 GB (17179869184 bytes) | `sysctl hw.memsize` |
| RAM type and modules | LPDDR5, Hynix. One entry, no slots, no removable modules. Memory is part of the chip package, so it cannot be upgraded | `system_profiler SPMemoryDataType` |
| RAM speed | Not shown by this command on Apple Silicon, so not measured | `system_profiler SPMemoryDataType` |
| Disk model | APPLE SSD AP0256Z, 251 GB, GPT | `system_profiler SPNVMeDataType` |
| Disk type | SSD, NVMe (Apple Fabric), SMART Verified | `system_profiler SPStorageDataType` |
| Free space on the volume for VMs | 178.86 GB free of 245.11 GB (Data volume, /System/Volumes/Data) | `system_profiler SPStorageDataType`, `df -h /System/Volumes/Data` |
| Firmware | Not BIOS or UEFI. Apple Silicon uses its own boot firmware (iBoot). System Firmware Version 20457.1.29. macOS does not show a firmware date | `system_profiler SPHardwareDataType` |
| Hardware virtualization | Present and enabled: kern.hv_support = 1 (Hypervisor.framework) | `sysctl kern.hv_support` |

Note on virtualization: the VMX flag is an Intel term and does not exist on ARM, so grep for it printed nothing on the M2. On Apple Silicon the correct check is `kern.hv_support`.

Note for the next labs: the CPU is ARM, so I need ARM64 images (Ubuntu Server ARM64,