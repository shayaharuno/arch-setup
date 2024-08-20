# General
 * Enable multilib repo
 * Install GCM
 * Install `yay` for AUR
 * Add neccesary boot flags for NVIDIA, e. g. `nvidia_drm.modeset=1`
 * Enable NVIDIA hibernate/resume/suspend daemons
 * Install SpoofDPI and auto-run it on login
 * Auto-mount windows partition if any
 * Packages: `sudo pacman -Sy cmake ninja unzip wl-clipboard ntfs-3g fuse2 fuse3 ardour alsa-utils power-profiles-daemon`
 * AUR: `yay -Sy coppwr-bin logiops equibop brave-bin`
 * Setup `/etc/logid.conf`
 * For bluetooth install `bluez` and `bluez-utils` then enable with `sudo systemctl enable bluetooth.service`

# Steam
 * Add `STEAM_FORCE_DESKTOPUI_SCALING=1.5` to `/etc/environment` to force UI scale
 * Move `compatdata` to Linux fs and symlink it with NTFS library

# 86Box
 * Install Steam, then install `lib32-libxi`, `lib32-pipewire` and `lib32-fuse3` to run x86 builds 

# Audio
 * Use `rtcqs` to check audio performance

# RME Babyface Pro
 * Use Pro Audio profile
 * Set `PCM-AN1-AN1`, `PCM-AN2-AN2`, `PCM-AN1-PH3` and `PCM-AN2-PH4` in `alsamixer` to 100 (fixes audio after sleep)
 * Optionally add `IN3`/`IN4` monitoring
