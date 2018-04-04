
USB tablets with touch include USB tablet PCs and the Bamboo Pen & Touch series of tablets.  Because their stylus/eraser & touch or touch/pad are exported as two separate kernel devices they have some idiosyncrasies we'll explore briefly.  BambooPT examples will be shown because except for the pad (tablet buttons) they also apply to a USB tablet PC. See also [USB Tablets with Touch](https://github.com/linuxwacom/xf86-input-wacom/wiki/USB-Tablets-with-Touch) in the X driver wiki.

### Touch arbitration ###
Historically, we turn touch off when stylus is in proximity, in the kernel and X server. So, clients in userland would not get touch events when stylus is active. That was mainly a workaround to cope with the lack of palm rejection on Linux.

To prepare for simultaneous pen and touch support in userland, touch_arbitration parameter is added to kernel 4.9. With touch_arbitration, users have the opportunity to let kernel report touch events along with pen events. This feature has been backported to kernel 2.6.38 and later in input-wacom.

touch_arbitration can be temporarily changed/set:
<pre>
1.	directly when Wacom kernel driver is loaded:
    a.	modprobe wacom (default state where driver is loaded with arbitration on)
    b.	modprobe wacom touch_arbitration=0 (forced off state)
    c.	modprobe wacom touch_arbitration=1 (forced on state)

2.	by the touch_arbitration file at /sys/module/wacom/parameters through commands:
    a.	“echo Y > /sys/module/wacom/parameters/touch_arbitration” (on)
    b.	“echo N > /sys/module/wacom/parameters/touch_arbitration” (off)
</pre>
Parameter set through above approach will be lost after a system reboot. To make the setting permanent, it needs to go into a static configuration file, which allows the driver to be loaded with the predefined parameter. The configure file can be different with different distributions or versions. 

For Fedora and ArchLinux, the follow approach is used.
<pre>
Add wacom.conf to /etc/modprobe.d with the following contents:

# this option will load wacom driver with touch arbitration turned on
# replace 1 with 0 if you need to turn it off
options wacom touch_arbitration=1
</pre>
Other distributions or versions may use different files. For example, /etc/modules (used by some Ubuntu versions) as well as /etc/modprobe.conf and /etc/rc.modules are found in other Linux distributions.

