A common complaint on Debian 12 Bookworm is inability to do video or graphics accleration or load any GUI with a new AMD Radeon GPU in the RX 6000 or RX 7000 series.

At the time of writing (December 2023) this affects the following ranges and models:

* Navi 2x / RDNA2: RX 6300M, RX 6400, RX 6450M, RX 6500M, RX 6500 XT, RX 6550M, RX 6600S, RX 6600M, RX 6600, RX 6600 XT, RX 6650M, RX 6650M XT, RX 6650 XT, RX 6700S, RX 6700M, RX 6700, RX 6700 XT, RX 6750 XT, RX 6800S, RX 6800M, RX 6800, RX 6800 XT, RX 6850M XT, RX 6900 XT, RX 6950 XT
* Navi 3x / RDNA3: RX 7600S, RX 7600M, RX 7600, RX 7600M XT, RX 7700S, RX 7700 XT, RX 7800 XT, RX 7900M, RX 7900 GRE, RX 7900 XT, RX 7900 XTX

The problem is that the Bookworm `firmware-amd-graphics` package does not ship the required firmware for these devices.

If you've updated the kernel or rebuilt the initramfs, you'll have seen complaints about missing files starting with `gc_11_0_3` (RX 6000) or `gc_11_0_4` (RX 7000). This is the problem.

Get all the files which start `gc_11_0_3` and `gc_11_0_4` from the [upstream linux-firmware](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/amdgpu) and place them in `/lib/firmware/amdgpu/`

Rebuild the initramfs with `sudo update-initramfs -u -k all`

The previous messages about missing `gc_11_0_x` should be gone.

Reboot and the system should successfully load the GUI and 3D acceleration should work.

There might be other missing files but those probably don't matter, those are the firmware for other models of card. You can ignore those messages, or you can try to find all the files from upstream and place them in `/lib/firmware/amdgpu/`, but this will just consume space in your root filesystem and initramfs. The only benefit is that `update-initramfs` complains less. There are some files which just don't exist upstream or in any AMD driver, so there will always be at least a few missing files no matter what you do.

References:

* <https://www.reddit.com/r/debian/comments/18nzkoe/issue_unable_to_hardware_render_video_on_modern/>
* <https://www.reddit.com/r/debian/comments/18k2jhh/debian_12_amd_graphics_not_loading_gui/>