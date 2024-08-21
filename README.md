# General
 * Enable `multilib` repo
 * Install Git Credential Manager
 * Install `yay` for AUR
   * Edit `/etc/makepkg.conf` to disable debug packages
 * Install SpoofDPI and auto-run it on login
 * Auto-mount windows partition if any
 * Packages: `sudo pacman -Sy spectacle cmake ninja unzip wl-clipboard ntfs-3g fuse2 fuse3 ardour alsa-utils power-profiles-daemon`
 * AUR: `yay -Sy coppwr-bin equibop brave-bin`
 * Configure `MX Master 3S` `/etc/logid.conf`
 * For bluetooth install `bluez` and `bluez-utils` then enable with `sudo systemctl enable bluetooth.service`

# MX Master 3S
 * AUR: `yay -Sy logiops`
 * `sudo systemctl enable logid`
 * Copy `logid.conf` to `/etc/logid.conf`

# NVIDIA (Discrete Mode)
 * `dkms` package is OK for any kernel (long rebuild times though)
 * Regular `nvidia` package is specific to `linux` kernel (regular Arch Kernel)
 * For Wayland to work, add `nvidia_drm.modeset=1`
 * Fix GSP slowdowns: `nvidia.NVreg_EnableGpuFirmware=0`
 * Enable NVIDIA hibernate/resume/suspend daemons (`nvidia.NVreg_PreserveVideoMemoryAllocations=1` may also be needed)
 * All of the above could be added to `/etc/modprobe.d/nvidia.conf` instead
   ```
   options nvidia NVreg_PreserveVideoMemoryAllocations=1
   options nvidia NVreg_TemporaryFilePath=/var/tmp
   options nvidia NVreg_EnableGpuFirmware=0
   options nvidia_drm modeset=1
   options nvidia_drm fbdev=1
   ```
 * `GRUB_TERMINAL_OUTPUT=console` fixes slow GRUB

# Steam
 * Move `compatdata` to Linux fs and symlink it with NTFS library

# Fractional Scaling
  * `QT_SCALE_FACTOR_ROUNDING_POLICY=RoundPreferFloor`
  * `STEAM_FORCE_DESKTOPUI_SCALING=1.5`

# 86Box
 * Install Steam, then install `lib32-libxi`, `lib32-pipewire` and `lib32-fuse3` to run x86 builds 

# Audio
 * Use `rtcqs` to check audio performance

# RME Babyface Pro
 * Use Pro Audio profile
 * Set `PCM-AN1-AN1`, `PCM-AN2-AN2`, `PCM-AN1-PH3` and `PCM-AN2-PH4` in `alsamixer` to 100 (fixes audio after sleep)
 * Optionally add `IN3`/`IN4` monitoring
