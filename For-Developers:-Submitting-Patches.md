**If you are developing support for new devices, please develop against upstream kernels first.**

### Developing ###

The input-wacom driver is available through git for developers to hack on. Before using it, you should install your distribution's **git**, **autoconf**, and **automake** tools. Afterwards, you may clone the repository as follows:

<pre>
 git clone git://git.code.sf.net/p/linuxwacom/input-wacom linuxwacom-input-wacom
 cd linuxwacom-input-wacom
</pre>

### Submitting ###
Patches to input-wacom have no guarantee of being accepted into upstream kernels. Thus, patches to input-wacom which touch the 4.5/3.17 folders must be accepted to the Linux kernel first.

To do this, submit them to [linux-input@vger.kernel.org](http://vger.kernel.org/vger-lists.html#linux-input) where they must be approved by Jiri Kosina. After Jiri accepts them into one of his trees, they can be (backported and) applied to input-wacom.

#### Resources for submitting upstream patches ####

* http://nickdesaulniers.github.io/blog/2017/05/16/submitting-your-first-patch-to-the-linux-kernel-and-responding-to-feedback/
* http://elixir.free-electrons.com/linux/latest/source/Documentation/process
* https://kernelnewbies.org/FirstKernelPatch

### input-wacom (backport) support ###

Once a device is supported upstream, feel free to submit patches for backported support to the the [linuxwacom-devel](https://lists.sourceforge.net/lists/listinfo/linuxwacom-devel) mailing list



