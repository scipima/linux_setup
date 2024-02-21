# linux_setup
steps to make your linux OS working and performing well.

[Nvidia Optimus Guide for Debian](https://www.youtube.com/watch?v=9qoUl8i03Wg)

__ Uninstall Bumblee / Primus __ 
$ sudo apt remove primus libprimus-vk1 nvidia-primus-vk-common nvidia-primus-vk-wrapper primus-libs primus-nvidia primus-vk primus-vk-nvidia bumblebee bumblebee-nvidia

$ sudo apt purge primus libprimus-vk1 nvidia-primus-vk-common nvidia-primus-vk-wrapper primus-libs primus-nvidia primus-vk primus-vk-nvidia bumblebee bumblebee-nvidia

__ Xorg X server Intel Display Driver __
$ sudo apt remove xserver-xorg-video-intel

__ Nvidia Drivers __
$ sudo apt install nvidia-driver firmware-misc-nonfree

Reboot the system:
$ systemctl reboot

__ Debugging Tools __
$ sudo apt install intel-gpu-tools nvidia-smi vulkan-tools

__ Ensure the Drivers Works Part 1 __
$ nvidia-smi -l
$ vkcube

__ Ensure the Drivers Works Part 2 __
$ sudo intel_gpu_top
$ glxgears


Kernel (https://wiki.debian.org/NvidiaGraphicsDrivers)

[How to install Backports in Debian/Ubuntu/Mint](https://www.youtube.com/watch?v=pcJe1LqOBv4)

In some cases, if you're aiming to install the bleeding-edge version of the NVIDIA driver from Debian Backports, you may also need to install the kernel from backports to match it. For Debian 10, you might do this with:

# sudo apt install -t bookworm-backports linux-image-amd64 firmware-linux firmware-linux-nonfree 
# sudo apt install -t bookworm-backports linux-headers-amd64
