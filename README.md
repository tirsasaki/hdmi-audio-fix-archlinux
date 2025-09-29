# HDMI Audio Fix for Linux

## Problem Description
A common issue on Linux systems where HDMI audio doesn't work immediately after boot, even though the device appears as active in system settings. The audio typically starts working after the system goes to sleep mode and wakes up.

## System Information
- **OS**: All Linux distributions (Arch, Ubuntu, Fedora, Debian, openSUSE, etc.)
- **Desktop Environment**: KDE Plasma, GNOME, Xfce, or any DE
- **Graphics Platform**: X11 and Wayland
- **Hardware**: Intel, AMD, NVIDIA graphics with HDMI output
- **Audio System**: PipeWire, PulseAudio, or ALSA

## Solution

### Steps to Fix:

**Kernel Parameters (GRUB)**

Edit GRUB configuration:
```bash
sudo nano /etc/default/grub
```

Add to `GRUB_CMDLINE_LINUX_DEFAULT`:
```
snd_hda_intel.dmic_detect=0
```

Update GRUB:

**For most distributions (Arch, Debian, Ubuntu, Mint, etc.):**
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

**For Fedora, RHEL, CentOS, AlmaLinux, Rocky Linux:**
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

**For UEFI systems on Fedora/RHEL (if standard command fails):**
```bash
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```

## Verification
After applying the kernel parameters:
1. Restart your computer
2. Test audio immediately after login
3. HDMI audio should now work without requiring sleep mode

## Contributing
If you found this solution helpful or have additional fixes for similar issues, feel free to contribute!

---
**Keywords**: Linux, HDMI audio, KDE Plasma, GNOME, PipeWire, PulseAudio, EndeavourOS, Arch Linux, Ubuntu, Fedora, Debian, Intel graphics, NVIDIA, AMD, audio fix
