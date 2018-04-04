Issue: Newer Wacom Devices on Centos 7.4+ and RHEL 7.4+

### Issue Summary ###
"Recent Centos 7/RHEL 7 *changed* support for newer Wacom devices by
transferring control of Wacom devices to the hid subsystem. While the
HID subsytem has full upstream kernel support for Wacom devices, the
RHEL/Centos kernel does not."

### Wacom Devices Affected as of October 2017: ###
1. Intuos Pro (Second Generation)
0. Cintiq Pro 13 and 16
0. DTH-1152
> Note: Future devices will also be affected.

### Issue Fix ###
Build an input-wacom driver version 0.37.0 or later. Please view the installation instructions on the [[input-wacom installation page|Installing-input-wacom-from-source]].

