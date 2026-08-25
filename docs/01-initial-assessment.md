# Initial System Assessment

## Project Background

This project involves repurposing an old gaming laptop into a headless Linux home lab server.

When the laptop was last regularly used, the internal display was experiencing problems and was believed to be faulty. During the initial assessment for this project, however, the internal display successfully produced a clear image without any immediately obvious visual defects. The condition and reliability of the display therefore remain under investigation.

Regardless of the display's condition, the long-term goal is to configure the laptop as a headless server. Once configured and tested, the server will normally remain powered on and be administered remotely across the local network from another computer. The laptop's display and HDMI output will remain available as backup methods for direct troubleshooting if remote access is unavailable.

## Stage 1 Initial Power-On Test

The laptop successfully powered on during the initial assessment.

During the initial boot test, the system did not boot into an operating system. Instead, it attempted an EFI PXE network boot over IPv6, which failed.

![EFI PXE IPv6 boot failure](../images/01-pxe-boot-failure.jpg)

## Initial Observations

The PXE boot attempt suggests that the system did not locate a usable local boot device before attempting to boot from the network.

At this stage, possible causes include:

- No operating system installed
- Missing or damaged bootloader
- Internal storage not being detected
- Failed internal storage
- Internal storage having previously been removed

No conclusion has been reached yet.

## Next Diagnostic Step

The next step will be to inspect the BIOS/UEFI configuration and determine whether the internal storage device is detected before physically opening the laptop.


## Stage 2 - BIOS and Storage Diagnostics

Following the initial PXE boot failure, further diagnostics were performed to determine why the laptop could not locate a bootable operating system and whether an internal storage device was being detected.

### Boot Device Check

After restarting the laptop, the system displayed a message stating that the default boot device was missing or that the boot process had failed.

The Boot Option Menu was inspected and contained no available bootable devices.

This confirmed that the system could not locate a bootable device. However, this alone did not confirm whether an internal storage device was physically installed, as a blank, failed, disconnected, or otherwise undetected drive could potentially produce similar symptoms.

The BIOS/UEFI configuration was therefore inspected.

### BIOS/UEFI Inspection

The InsydeH2O BIOS Setup Utility was accessed using the F2 key during startup.

The BIOS reported the following system information:

- CPU: Intel Core i7-10750H @ 2.60 GHz
- Installed memory: 65,536 MB (64 GB)
- SATA mode: AHCI

The Main section of the BIOS was inspected for detected storage devices.

The following SATA ports were reported as:

- SATA Port 1: Not Present
- SATA Port 4: Not Present

![BIOS showing no detected SATA storage](../images/02-bios-storage-not-present.jpg)

*Figure 2 - BIOS/UEFI Main screen showing no storage devices detected on SATA Port 1 or SATA Port 4.*


The OffBoard SATA Controller Configuration and OffBoard NVMe Controller Configuration were also inspected.

No storage devices were reported as present in either configuration.

### Current Diagnostic Conclusion

The BIOS/UEFI is currently detecting no SATA or NVMe storage devices.

This is consistent with the previous observations:

- The laptop failed to boot from local storage.
- The system fell back to an EFI PXE network boot attempt.
- The PXE boot attempt failed.
- A "Default Boot Device Missing or Boot Failed" message was displayed.
- The Boot Option Menu contained no bootable devices.
- No SATA storage devices were detected by the BIOS.
- No NVMe storage devices were detected by the BIOS.

At this stage, there are two primary possibilities:

1. The laptop's previous internal storage device has been physically removed.
2. A storage device remains installed but is not being detected due to a connection, hardware, or device failure.

A physical inspection is required before reaching a final conclusion.

### Troubleshooting Process

The investigation was deliberately performed from the least invasive diagnostic steps before moving to physical hardware inspection.

The troubleshooting process so far has been:

PXE boot failure  
→ Check Boot Option Menu  
→ No bootable devices found  
→ Enter BIOS/UEFI  
→ Check SATA storage  
→ No SATA devices detected  
→ Check NVMe storage  
→ No NVMe devices detected  
→ Physical inspection required

### Next Step - Physical Hardware Inspection

The next stage of the initial assessment will involve opening the laptop and inspecting the internal hardware.

Before opening the laptop, the system will be completely powered down and disconnected from external power and peripherals.

The inspection will determine:

- Whether an internal SSD or HDD is physically installed
- Whether any installed storage device is correctly connected
- Which SATA and/or M.2 storage interfaces are available
- Whether there are any obvious hardware or connection problems
- What type of replacement storage would be required if no drive is installed

No replacement storage will be purchased until the laptop's internal storage configuration has been physically confirmed.
