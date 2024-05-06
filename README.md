# Debian and Linux Setup
This repo gathers steps to make your linux OS working and performing well.

## NVIDIA
This is perhaps the most problematic of issues, as errors can crop up from multiple things.
In general, have a look at these websites before doing anything else. 

* [NvidiaGraphicsDrivers](https://wiki.debian.org/NvidiaGraphicsDrivers)
* [NVIDIA Optimus](https://wiki.debian.org/NVIDIA%20Optimus)

As per the first link, if the output of the following command has more than 1 row, you have Optimus installed. 
```
lspci -nn | egrep -i "3d|display|vga"
```

You can then run the following to get the suggested driver. 
```
nvidia-detect
```

Now, **before you install the NVIDIA drivers**, you must install the kernel headers for your distribution. 
```
sudo apt install linux-headers-amd64
```

If you're not in Debian stable, but using backports, then you need the `-t` flag, like so (if you're on Debian 12 Bookworm).
```
sudo apt install -t bookworm-backports linux-image-amd64
```

You can then install the drivers (remember that this assumes that you follow the instructions on how to change your `/etc/apt/sources.list`, as stated in the instructions on the same webpage).
```
sudo apt install nvidia-driver firmware-misc-nonfree
```

If you have an extremely modern NVIDIA GPU that was manufactured after the release of your Debian version, it may not work even after installing the newest backported driver that claims to support your card. If so, you likely need to upgrade the non-free firmware package on your system as well by installing the firmware-misc-nonfree package from backports. For instance, on a Debian 10 system with backports enabled:
```
sudo apt install -t buster-backports firmware-misc-nonfree
```

## Other resources
### Purge conflicting packages and re-install
Below I list a few YouTube videos that helped troubleshoot a few issues i nthe past, and may be helpful to someone out there. 

[Nvidia Optimus Guide for Debian](https://www.youtube.com/watch?v=9qoUl8i03Wg)

Uninstall `bumblebee` & `Primus` 
```
sudo apt remove primus libprimus-vk1 nvidia-primus-vk-common nvidia-primus-vk-wrapper primus-libs primus-nvidia primus-vk primus-vk-nvidia bumblebee bumblebee-nvidia
```

Purge packages completely
```
sudo apt purge primus libprimus-vk1 nvidia-primus-vk-common nvidia-primus-vk-wrapper primus-libs primus-nvidia primus-vk primus-vk-nvidia bumblebee bumblebee-nvidia
```

Remove `Xorg X server` `Intel Display Driver`
```
sudo apt remove xserver-xorg-video-intel
```

Install Nvidia Drivers
```
sudo apt install nvidia-driver firmware-misc-nonfree
```

Reboot the system:
```
systemctl reboot
```

Debugging Tools to check whether the installation went through.
```
sudo apt install intel-gpu-tools nvidia-smi vulkan-tools
```

Check 1: Ensure the Drivers Works Part 1
```
nvidia-smi -l
vkcube
```

Check 2: Ensure the Drivers Works Part 2
```
sudo intel_gpu_top
glxgears
```


### Deal with older Kernel
[How to install Backports in Debian/Ubuntu/Mint](https://www.youtube.com/watch?v=pcJe1LqOBv4)

In some cases, if you're aiming to install the bleeding-edge version of the NVIDIA driver from Debian Backports, you may also need to install the kernel from backports to match it. 
For Debian 12, you might do this with:
```
sudo apt install -t bookworm-backports linux-image-amd64 firmware-linux firmware-linux-nonfree
sudo apt install -t bookworm-backports linux-headers-amd64
```
