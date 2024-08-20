# General
 * Install `yay` for AUR
 * Add neccesary boot flags for nvidia, e. g. `nvidia_drm.modeset=1`
 * Enable nvidia hibernate/resume/suspend daemons
 * Install SpoofDPI and auto-run it on login
 * Auto-mount windows partition if any

# Audio
 * Use `rtcqs` to check audio performance

# RME Babyface Pro
 * Use Pro Audio profile
 * Set `PCM-AN1-AN1`, `PCM-AN2-AN2`, `PCM-AN1-PH3` and `PCM-AN2-PH4` in `alsamixer` to 100 (fixes audio after sleep)
 * Optionally add `IN3`/`IN4` monitoring
