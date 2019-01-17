# Diagnosing FreeBSD graphics subsystem

## Contents

* [Listing available PCI devices](#listing-available-pci-devices)

* * *

## Listing available PCI devices

It's advised to install `dmidecode` package. To list the devices you
may use one of the following commands:

* `sudo dmidecode`
* `sudo pciconf -lvbce` - long list
* `sudo pciconf -lv` - short list
* `xrandr --listproviders`
* `glxinfo | grep render`
* `devinfo -vr`

Now I know that Radeon Carizzo == Radeon Wani

Message from drm-fbsd11.2-kmod-4.11g20181210:

The drm-stable-kmod port can be enabled for amdgpu (for AMD GPUs starting with
the HD7000 series / Tahiti) or i915kms (for Intel APUs starting with HD3000 /
Sandy Bridge) through kld_list in /etc/rc.conf. radeonkms for older AMD GPUs
can be loaded and there are some positive reports if EFI boot is NOT enabled
(similar to amdgpu).

For amdgpu: kld_list="amdgpu"
For Intel: kld_list="/boot/modules/i915kms.ko"
For radeonkms: kld_list="/boot/modules/radeonkms.ko"

Please ensure that all users requiring graphics are members of the
"video" group.

Older generations are supported by the legacy kms modules (radeonkms / 
i915kms) in base or by installing graphics/drm-legacy-kmod.

