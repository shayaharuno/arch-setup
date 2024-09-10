# General
 * Enable `multilib` repo
 * Install `yay` for AUR
   * Edit `/etc/makepkg.conf` to disable debug packages
 * Packages: `yay -S --needed kdialog spoofdpi-bin partitionmanager gwenview kcalc mpv qtcreator coppwr-bin blender krita obs-studio steam qbittorrent equibop element-desktop telegram-desktop brave-bin ttf-iosevka-nerd ttf-iosevkaterm-nerd p7zip kfind filelight fastfetch spectacle cmake ninja unzip wl-clipboard ntfs-3g fuse2 fuse3 alsa-utils tuned tuned-ppd alacritty neovim okular kdegraphics-mobipocket unrar ripgrep fd`
 * Enable `tuned` with `sudo systemctl enable tuned` and `sudo systemctl enable tuned-ppd`
 * Make SpoofDPI autorun on login and add `--proxy-server=http://127.0.0.1:8085` to Chromium-based browsers
 * Auto-mount windows partition if any
 * Install Git Credential Manager
 * Clone Neovim and Alacritty configs
 * For bluetooth install `bluez` and `bluez-utils` then enable with `sudo systemctl enable bluetooth.service`

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
 * For Wayland to work, add `nvidia_drm.modeset=1`
 * Disable GSP until fixed: `nvidia.NVreg_EnableGpuFirmware=0` (only works with closed source kernel module)
 * Enable NVIDIA hibernate/resume/suspend daemons and add `nvidia.NVreg_PreserveVideoMemoryAllocations=1`
 * All of the above may be added to `/etc/modprobe.d/nvidia.conf`
   ```
   options nvidia NVreg_PreserveVideoMemoryAllocations=1
   options nvidia NVreg_TemporaryFilePath=/var/tmp
   options nvidia NVreg_EnableGpuFirmware=0
   options nvidia_drm modeset=1
   options nvidia_drm fbdev=1
   ```
 * Add `nvidia-booster.service` to `/etc/systemd/system` as a temporary mitigation of GSP issue
 * Uncommenting `GRUB_TERMINAL_OUTPUT=console` in `/etc/default/grub` fixes slow GRUB

# Wine
 * Install: `yay -S wine-staging wine-mono winetricks`
 * Install all fonts through `winetricks`
 * Guitar Pro 8 confirmed working

# Steam
 * It's possible to use NTFS partition for game library
 * In that case move `compatdata` to Linux fs and symlink it with NTFS library

# Audio
 * Use `rtcqs` to check audio performance
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
 * `sudo systemctl enable logid`

# RME Babyface Pro
 * Use Pro Audio profile
 * Set `PCM-AN1-AN1`, `PCM-AN2-AN2`, `PCM-AN1-PH3` and `PCM-AN2-PH4` in `alsamixer` to 100 (fixes audio after sleep)
 * Optionally add `IN3`/`IN4` monitoring
