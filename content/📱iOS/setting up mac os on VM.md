

https://archive.org/details/macos-collection - iso here

https://github.com/DrDonk/unlocker - unlocker for vmware workstation pro

---
error: The CPU has been disabled by the guest operating system. Power off or reset the virtual machine.

Fix

Don't let the "The CPU has been Disabled by the Guest Operating System macOS AMD" error slow you down. Watch this video now and fix the problem effortlessly. Like, comment, and share with others who might find this tutorial helpful. Subscribe to our channel for more useful tech tutorials and stay ahead of the curve.

Open .vmx file in VM folder using notepad and append the following to it

```

smc.version = "0" cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011" cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111" cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110" cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001" cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001" cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000" cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011" cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111" smbios.reflectHost = "TRUE" hw.model = "MacBookPro14,3" board-id = "Mac-551B86E5744E2388" 

```

---

Installing mac os 

Go to disk utility when VM Boots up

Switch over to Disk Utility (IIRC, should be in one of the menus), see if the HDD device is there. Click on it to select, make sure the partition map scheme is GUID Partition Table. If a volume is present (named Macintosh HD?), select and make sure it is in Mac OS Extended (Journaled) format. Erase/repartition if needed, and see if that fixes the MIA disk issue.

---