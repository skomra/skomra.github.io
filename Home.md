

**The Linux Wacom Project** manages the drivers, libraries, and documentation for configuring and running Wacom tablets under the Linux operating system. Our drivers are included in most major distributions and provide out-of-the box support for a wide variety of Wacom tablets and TabletPCs. The project consist of this (input-wacom) driver, the X driver and libwacom.

### For Users ###
Please note many tablets will be supported by a the kernel on your newer operating system. You will only need to install input-wacom if you have a newly released device or if you need a bugfix. In addition, new devices will have most of their features supported on kernels after 4.11 as we have enabled generic device support and devices are supported through the use of firmware HID Descriptors on these newer kernels.

Nevertheless, many users will want to know how to [install input-wacom from source](https://github.com/linuxwacom/input-wacom/wiki/Installing-input-wacom-from-source). 

Bugs:
-----
To submit a [bug](https://github.com/linuxwacom/input-wacom/issues), create an
issue on Github.


[[Wacom Tablet Set Up|Set-Up Your Tablet]]

 There is also a small [[FAQ]] which we hope will grow over time.

Please see the sidebar for other topics, and see the Wacom X Driver, and libwacom for issues associated with those projects. 

### For Developers ###

input-wacom contains the downstream and backport versions of the Linux Kernel Wacom driver. Please see the [[submitting patches page | https://github.com/linuxwacom/input-wacom/wiki/For-Developers:-Submitting-Patches]]. Also, please note the topics beginning with "For Developers" in the sidebar.

### Mailing Lists ###

### Legacy support ###
If you are running on kernels older than 2.6.30 or X servers older than 1.7, the old (old) website is still available
[here](http://linuxwacom.sourceforge.net/index_old.php).
</div>

### Sourceforge ###
This project was formerly hosted on Sourceforge, for historic questions you may want to check the [Sourceforge wiki archive](http://linuxwacom.sourceforge.net/wiki/index.php/Main_Page). 