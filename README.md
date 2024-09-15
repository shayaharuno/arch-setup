# Installation
 * BTRFS: `@.snapshots` subvolume is not needed for Timeshift snapshots

# General
 * Edit `/etc/makepkg.conf` to disable debug packages
 * Edit `/etc/pacman.conf` to enable colors, parallel downloads and `multilib` repo
 * Install `yay`: https://github.com/Jguer/yay
 * Packages: `yay -S --needed kdialog spoofdpi-bin partitionmanager gwenview kcalc mpv qtcreator coppwr-bin blender krita obs-studio steam qbittorrent equibop element-desktop telegram-desktop brave-bin ttf-iosevka-nerd ttf-iosevkaterm-nerd p7zip kfind filelight fastfetch spectacle cmake ninja unzip wl-clipboard ntfs-3g fuse2 fuse3 alsa-utils tuned tuned-ppd alacritty neovim okular kdegraphics-mobipocket unrar ripgrep fd bluez bluez-utils realtime-privileges`
 * Enable Bluetooth with `sudo systemctl enable --now bluetooth.service`
 * Enable `spoofdpi` with `sudo systemctl enable --now spoofdpi.service` and add `--proxy-server=http://127.0.0.1:8080` to Chromium-based browsers
 * Auto-mount windows partition if any
 * Install Git Credential Manager: https://github.com/git-ecosystem/git-credential-manager
 * Clone Neovim and Alacritty configs

# GRUB
 * Uncommenting `GRUB_TERMINAL_OUTPUT=console` in `/etc/default/grub` fixes slow GRUB
 * `GRUB_GFXMODE=1440x900x32,1280x1024x32,auto` makes text larger and fixes slowdowns
 * Boot flags: `quiet splash loglevel=3 systemd.show_status=auto rd.udev.log_level=3 mitigations=off threadirqs preempt=full nohz_full=all nowatchdog`
 * Apply changes: `grub-mkconfig -o /boot/grub/grub.cfg`

# Environment Variables
 * Put user-specific enironment variables to `~/.bash_profile`
 * Fix fractional scaling:
   ```
   export QT_SCALE_FACTOR_ROUNDING_POLICY=RoundPreferFloor
   export STEAM_FORCE_DESKTOPUI_SCALING=1.5
   ```

# Intel Graphics
 * Vulkan driver: `yay -S vulkan-intel lib32-vulkan-intel`
 * Video acceleration: `yay -S intel-media-driver onevpl-intel-gpu libva-utils`

# NVIDIA Graphics
 * Best option is `nvidia-dkms` package (works with any kernel)
 * `nvidia-open-dkms` currently has performance issues
 * Video acceleration: `yay -S libvdpau libva-nvidia-driver`
 * Create `/etc/modprobe.d/nvidia.conf`:
   ```
   # Suspend fix
   options nvidia NVreg_PreserveVideoMemoryAllocations=1
   options nvidia NVreg_TemporaryFilePath=/var/tmp
   # Setting it to 0 might help with slowdowns, setting it to 1 only works for 2000+ cards
   options nvidia NVreg_EnableGpuFirmware=1
   # Wayland fix
   options nvidia_drm modeset=1
   options nvidia_drm fbdev=1
   ```
 * Add `nvidia-boost.service` to `/etc/systemd/system` as a temporary mitigation of GSP issue
 * Enable services: `sudo systemctl enable --now nvidia-{suspend,resume,hibernate,powerd,persistenced,boost}`

# Wine
 * Install: `yay -S wine wine-mono winetricks`
 * Install fonts: `winetricks corefonts` or `winetricks allfonts`
 * Guitar Pro 8 confirmed working

# Steam
 * It's possible to use NTFS partition for game library
 * In that case move `compatdata` to Linux fs and symlink it with NTFS library

# Pro Audio
 * Use `rtcqs` to check audio performance
 * `rtirq` for RT or `threadirqs` enabled kernels: install with `yay -S rtirq` and run with `sudo systemctl enable --now rtirq`
 * Install audio DAW and plugins: `yay -S sws reaper reapack lsp-plugins-clap zam-plugins-clap surge-xt-clap ot-urchin-clap ot-cryptid-clap ob-xd-lv2 js80p jc303-clap dragonfly-reverb-clap cardinal-clap dexed-clap`
 * Reaper setup: edit `ui_scale=*` in `~/.config/REAPER/reaper.ini` and manually add `/usr/lib/vst3/` to VST path

# Development
 * Extract Vulkan SDK to `~/Tools/VulkanSDK/1.x.xxx` and symlink it to `current`, then add `source ~/Tools/VulkanSDK/current/setup-env.sh` to `~/.bash_profile`
 * NVIDIA Nsight works well under sudo

# Advanced Debugging With GDB
 * Install `debuginfod`: `yay -S debuginfod`
 * Add `set debuginfod enabled on` to `~/.gdbinit`

# MX Master 3S
 * This seems essential as this mouse prevents PC from sleeping properly unless the driver is installed
 * AUR: `yay -S logiops`
 * Copy `logid.conf` to `/etc/logid.conf`
 * `sudo systemctl enable --now logid`

# RME Babyface Pro
 * Use Pro Audio profile
 * Set `PCM-AN1-AN1`, `PCM-AN2-AN2`, `PCM-AN1-PH3` and `PCM-AN2-PH4` in `alsamixer` to 100 (fixes audio after sleep)
 * Optionally add `IN3`/`IN4` monitoring
