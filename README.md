Here are the **minimum system requirements** for running Windows 11:

1. **Processor**: 1 gigahertz (GHz) or faster with two or more cores on a compatible 64-bit processor or system on a chip (SoC).
2. **RAM**: 4 gigabytes (GB) or more.
3. **Storage**: 64 GB or larger storage device.
4. **System Firmware**: UEFI, Secure Boot capable.
5. **TPM**: Trusted Platform Module (TPM) version 2.0.
6. **Graphics Card**: Compatible with DirectX 12 or later, with a WDDM 2.0 driver.
7. **Display**: High definition (720p) display, 9" or greater monitor, 8 bits per color channel.
8. **Internet Connection**: Internet connectivity is necessary for updates and to download and use some features.

Does your current PC meet these requirements, or are you planning to upgrade?

You can use the "PC Health Check" tool provided by Microsoft to check if your system meets the requirements for Windows 11. However, if you prefer using the Command Prompt, here are a few commands you might find useful:

1. **Check Processor**:
```sh
wmic cpu get caption
```

2. **Check RAM**:
```sh
wmic memorychip get capacity
```

3. **Check Storage**:
```sh
wmic logicaldisk get size,freespace,caption
```

4. **Check BIOS Mode**:
```sh
wmic bios get smbiosbiosversion
```

5. **Check TPM Version**:
```sh
tpm.msc
```

6. **Check Graphics Card**:
```sh
dxdiag
```
This will bring up the DirectX Diagnostic Tool, where you can see details about your graphics card.

These commands will help you verify if your system meets the minimum requirements. Let me know if you need any further assistance!



You can use the following script in PowerShell to check if your system meets the minimum requirements for running Windows 11:

```sh
# Check Processor
$processor = Get-WmiObject Win32_Processor | Select-Object -ExpandProperty Name

# Check RAM
$ram = (Get-WmiObject Win32_ComputerSystem).TotalPhysicalMemory / 1GB

# Check Storage
$storage = Get-PSDrive -PSProvider FileSystem | Where-Object {$_.Used -gt 0} | Select-Object Name, @{Name="FreeSpace(GB)";Expression={$_.Free/1GB}}, @{Name="UsedSpace(GB)";Expression={$_.Used/1GB}}

# Check BIOS Mode
$bios = Get-WmiObject Win32_BIOS | Select-Object -ExpandProperty SMBIOSBIOSVersion

# Check TPM Version
$tpm = Get-WmiObject -Namespace "Root\CIMv2\Security\MicrosoftTpm" -Class Win32_Tpm | Select-Object -ExpandProperty SpecVersion

# Check Graphics Card
$graphics = Get-WmiObject Win32_VideoController | Select-Object -ExpandProperty Description

# Display Results
Write-Output "Processor: $processor"
Write-Output "RAM: $([math]::Round($ram,2)) GB"
Write-Output "Storage:"
$storage | Format-Table -AutoSize
Write-Output "BIOS Mode: $bios"
Write-Output "TPM Version: $tpm"
Write-Output "Graphics Card: $graphics"
```

This script will gather all the relevant information and display it in a comprehensive manner. If you need any assistance running this script or interpreting the results, feel free to ask!




