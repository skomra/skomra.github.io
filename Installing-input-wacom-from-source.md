The **input-wacom** driver is a set of loadable kernel modules which allows new tablets to be used with systems using kernels as old as Linux 2.6.30. While this gets many of the updates that are pushed to the upstream Linux kernel driver, some differences may exist. This will be particularly apparent for users of older kernels. Because of this, we recommend upgrading your kernel if possible and only installing this driver when absolutely necessary.

This driver builds two separate kernel modules: [[wacom.ko and wacom_w8001.ko|Kernel-Drivers]]. The former is used for the vast majority of tablets (USB-attached for 2.6.30 - 3.16; USB/Bluetooth/I2C-attached for 3.17+), while the latter is used for older tablet PCs whose digitizers are connected via an internal serial interface. The [[hid-wacom.ko and wacom_i2c.ko|Kernel-Drivers]] modules (legacy modules for Bluetooth and I2C tablets, respectively) are ''not'' included with this driver.

## Installation ##
### Prerequisites ###
Before building, you'll need to ensure the necessary dependencies have been installed on your system:

<pre>
 sudo apt-get install linux-headers-$(uname -r) build-essential # on Debian, Ubuntu, Mint
 sudo yum install gcc "kernel-devel-uname-r == $(uname -r)"     # on RHEL, CentOS, Fedora
 sudo pacman -Syy                                               # on Arch
 sudo pacman -S linux                                           # on Arch
 sudo reboot                                                    # on Arch
 sudo pacman -S linux-headers                                   # on Arch
 sudo zypper install kernel-devel                               # on open SUSE 11.4
 sudo zypper install --type pattern devel_basis                 # on open SUSE 11.4
</pre>

### Download ###
In general, you should simply download and untar the latest release from the [releases page](https://github.com/linuxwacom/input-wacom/releases). If, however, you need to build a development version of the driver you will need to install and use the "git" tool to clone a copy of our repository. The developer should provide you with a git command to perform the necessary clone.

### Build / Install ###
Open a terminal and navigate into the extracted/cloned input-wacom directory. Next, copy and paste the following command to build and install the driver. If you get a "Build Failed" message at the end if your output, please contact the linuxwacom developers for support.

```sh
$ if test -x ./autogen.sh; then ./autogen.sh; else ./configure; fi && make && sudo make install || echo "Build Failed"
```

> **Note for Fedora, RHEL, & CentOS Users:**
> Fedora 24+, RHEL 7.4+, and CentOS 7.4+ require that you rebuild the initramfs to finish the installation. The command `sudo dracut --force` can be used for this. Note that this does not appear to work with Fedora 26 for some reason. Also note that if you have manually installed other kernel modules, running this command may or may not interfere with those modules. We need to investigate further to understand how to use dracut safely.

### Module Loading ###
The updated driver should automatically load after rebooting the system. You can verify the version number of the loaded kernel module by running the following command. Version numbers like "v2.00" indicate that the stock kernel module is still in use. A version number like "v2.00-0.38.0" indicates that version 0.38.0 of the input-wacom driver is loaded. Consult the "Troubleshooting" section below if the version number does not match what you expect.

```sh
$ grep "" /sys/module/wacom*/version
```

## Next Steps ##
Upgrading both the kernel driver and the X driver to the same version is recommended. Please see the instructions for [updating the xf86-input-wacom driver](https://github.com/linuxwacom/xf86-input-wacom/wiki/Building-The-Driver).

## Development ##
**If you are developing support for new devices, please develop against upstream kernels first.**
See [[For-Developers:-Submitting-Patches]]

## Troubleshooting ##
If the kernel driver does not seem to load after a reboot, please try running the following commands. This will force the kernel to reload the modules from the disk, which may be necessary if an old version is cached in your distribution's initramfs. If you experience this issue, please contact the linuxwacom developers.

```sh
sudo rmmod wacom
sudo rmmod wacom_w8001
sudo modprobe wacom
sudo modprobe wacom_w8001
```
