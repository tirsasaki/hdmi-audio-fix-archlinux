# HDMI Audio Fix for Archlinux (KDE Plasma)

## Problem Description

A common issue on Linux systems where HDMI audio doesn't work immediately after boot, even though the device appears as active in system settings. The audio typically starts working after the system goes to sleep mode and wakes up.

## System Information

- **OS**: EndeavourOS & CachyOS (Arch-based)
- **Desktop Environment**: KDE Plasma 6.4.5
- **Graphics Platform**: Wayland
- **Hardware**: Intel UHD Graphics with HDMI output
- **Audio System**: PipeWire

## Solution

### Steps to Fix:

Kernel Parameters (GRUB)
Edit GRUB configuration:
```bash
sudo nano /etc/default/grub
```

Add to `GRUB_CMDLINE_LINUX_DEFAULT`:
```
snd_hda_intel.dmic_detect=0
```

Update GRUB:
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Verification

After applying the KDE audio settings:
1. Restart your computer
2. Test audio immediately after login
3. HDMI audio should now work without requiring sleep mode

## Contributing

If you found this solution helpful or have additional fixes for similar issues, feel free to contribute!



---

**Keywords**: Linux, HDMI audio, KDE Plasma, PipeWire, EndeavourOS, Arch Linux, Intel graphics, audio fix
