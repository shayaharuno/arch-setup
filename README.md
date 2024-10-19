# Installation
 * BTRFS: `@.snapshots` subvolume is not needed for Timeshift snapshots

# General
 * Enable periodic TRIM: `sudo systemctl enable fstrim.timer`
 * Edit `/etc/makepkg.conf` to disable debug packages
 * Edit `/etc/pacman.conf` to enable colors, parallel downloads and `multilib` repo
 * Install `yay`: https://github.com/Jguer/yay
 * Packages: `yay -S --needed kdialog partitionmanager gwenview kcalc mpv blender krita steam qbittorrent telegram-desktop brave-bin p7zip kfind filelight spectacle unzip wl-clipboard ntfs-3g fuse2 fuse3 alsa-utils tuned tuned-ppd okular kdegraphics-mobipocket unrar ripgrep fd flatpak fwupd`
 * More packages: `yay -S --needed neovim alacritty zsh godot vesktop-bin visual-studio-code-bin ttf-jetbrains-mono-nerd ttf-mplus-nerd fastfetch obsidian telegram-desktop qbittorrent obs-studio zen-browser-bin`
 * Enable Tuned with `sudo systemctl enable --now tuned` and `sudo systemctl enable --now tuned-ppd`
 * Enable Bluetooth with `sudo systemctl enable --now bluetooth.service`
 * Enable `spoofdpi` with `sudo systemctl enable --now spoofdpi.service` and add `--proxy-server=http://127.0.0.1:8080` to Chromium-based browsers
 * Auto-mount windows partition if any
 * Install Git Credential Manager: https://github.com/git-ecosystem/git-credential-manager
 * Clone Neovim and Alacritty configs

# GRUB
 * Uncommenting `GRUB_TERMINAL_OUTPUT=console` in `/etc/default/grub` fixes slow GRUB
 * `GRUB_GFXMODE=1440x900x32,1280x1024x32,auto` makes text larger and fixes slowdowns
 * Boot flags: `quiet splash loglevel=3 systemd.show_status=auto rd.udev.log_level=3 mitigations=off nowatchdog`
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
 * For 2000+ series cards install `nvidia-open-dkms`, otherwise use `nvidia-dkms`
 * Enable suspend and other services: `sudo systemctl enable nvidia-{suspend,resume,hibernate,powerd,persistenced}`
 * In case of poor performance add `nvidia-boost.service` to `/etc/systemd/system` and enable it `sudo systemctl enable --now nvidia-boost`. Adjust clocks in `nvidia-boost.service` based on output of `nvidia-smi -q -d SUPPORTED_CLOCKS` if needed.
 * Enable HDR: `export KWIN_DRM_ALLOW_NVIDIA_COLORSPACE=1` in `/etc/environment/`
 * Video acceleration: `yay -S libvdpau libva-nvidia-driver`
<details>
  <summary>Some kernel flags that might be useful</summary>

   Add these to `/etc/modprobe.d/nvidia.conf`

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

</details>

# Wine
 * Install: `yay -S wine wine-mono winetricks`
 * Install fonts: `winetricks corefonts` or `winetricks allfonts`
 * Guitar Pro 8 confirmed working

# Steam
 * It's possible to use NTFS partition for game library
 * In that case move `compatdata` to Linux fs and symlink it with NTFS library

# Pro Audio
 * Use `rtcqs` to check audio performance
 * Use `linux-rt` kernel or add boot flags: `threadirqs preempt=full nohz_full=all`
 * `rtirq` for RT or `threadirqs` enabled kernels: install with `yay -S rtirq` and run with `sudo systemctl enable --now rtirq`
 * Install audio DAW and plugins: `yay -S sws reaper reapack lsp-plugins-clap zam-plugins-clap surge-xt-clap ot-urchin-clap ot-cryptid-clap ob-xd-lv2 js80p jc303-clap dragonfly-reverb-clap cardinal-clap dexed-clap libgme`
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
