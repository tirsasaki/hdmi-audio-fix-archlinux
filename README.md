# HDMI Audio Fix for EndeavourOS (KDE Plasma)

## Problem Description

A common issue on Linux systems where HDMI audio doesn't work immediately after boot, even though the device appears as active in system settings. The audio typically starts working after the system goes to sleep mode and wakes up.

## System Information

- **OS**: EndeavourOS (Arch-based)
- **Desktop Environment**: KDE Plasma 6.4.5
- **Graphics Platform**: Wayland
- **Hardware**: Intel UHD Graphics with HDMI output
- **Audio System**: PipeWire

## Solution

The issue is resolved through **ALSA Configuration**. This solution addresses the hardware-level audio driver initialization problem.

### Steps to Fix:

1. Create ALSA configuration file:
```bash
sudo nano /etc/modprobe.d/alsa-base.conf
```

2. Add the following content:
```
# Intel HDA audio fix
options snd-hda-intel model=auto
options snd-hda-intel enable_msi=1
```

3. Save the file and restart your system

### Why This Works:

This configuration ensures that the Intel HDA audio driver initializes properly during boot with the correct parameters. The `model=auto` option allows ALSA to automatically detect the appropriate codec model, while `enable_msi=1` enables Message Signaled Interrupts for better performance and compatibility.

## Alternative Solutions (If Above Doesn't Work)

<details>
<summary>Click to expand alternative solutions</summary>

### Method 1: KDE Audio Settings
1. Open **System Settings** in KDE Plasma
2. Navigate to **Multimedia** → **Audio**
3. Set your **HDMI device** as the **highest priority** and **default**
4. Enable **"Switch all running applications when changing the default device"**
5. Apply settings and restart

### Method 2: Systemd Service
Create an audio reset service:
```bash
sudo nano /etc/systemd/system/audio-fix.service
```

Content:
```ini
[Unit]
Description=Fix audio after boot
After=graphical.target

[Service]
Type=oneshot
User=your_username
ExecStart=/bin/bash -c 'sleep 5 && systemctl --user restart pipewire pipewire-pulse'
RemainAfterExit=true

[Install]
WantedBy=graphical.target
```

Enable the service:
```bash
sudo systemctl enable audio-fix.service
```

### Method 3: Kernel Parameters (GRUB)
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

### Method 4: Manual Audio Reset
If you need to reset audio manually:
```bash
systemctl --user restart pipewire pipewire-pulse
```

</details>

## Verification

After applying the KDE audio settings:
1. Restart your computer
2. Test audio immediately after login
3. HDMI audio should now work without requiring sleep mode

## Notes

- This solution is persistent and will survive system updates
- The ALSA configuration affects hardware-level driver initialization
- Works specifically well with Intel graphics and HDMI audio
- **Do not delete** the `/etc/modprobe.d/alsa-base.conf` file once it's working

## Contributing

If you found this solution helpful or have additional fixes for similar issues, feel free to contribute!



---

**Keywords**: Linux, HDMI audio, KDE Plasma, PipeWire, EndeavourOS, Arch Linux, Intel graphics, audio fix
