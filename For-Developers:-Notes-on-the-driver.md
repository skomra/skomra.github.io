This wiki page is intended to be a place to record notes about the 
internal workings of the Wacom Kernel driver.

**In range while exiting**

Hopefully this clarifies "in range while exiting"... I'll be using the
classic definition of "in range" (i.e., "in range" is further from the
tablet than "in prox") and assuming the use of one of the classic
non-HID tablets (Intuos5, Intuos Pro, Cintiq 24, Cintiq 27)

Imagine that you have a pen on the tablet surface (i.e., BTN_TOUCH = 1
and ABS_PRESSURE > 0) and that you pick it up and completely remove it
from proximity. Normally the driver would first receive a few reports
with decreasing pressure, then a few reports with increasing distance,
a couple "in range" reports, and finally the "out-of-prox" report.
Nothing special.

Now, however, imagine that you have a pen on the tablet surface and
that you pick it up very quickly but not entirely out of proximity. If
you're unlucky, the tablet can send a report indicating contact and
then immediately afterwards send a report indicating "in range".
Because in-range packets are handled by "wacom_intuos_inout" rather
than "wacom_intuos_general", the function needs to explicitly send
userspace data consistent with the "in-range" state (i.e., BTN_TOUCH =
0, ABS_PRESSURE = 0, ABS_DISTANCE = maximum). If this doesn't happen,
userspace is left thinking that the pen is still touching the tablet
until you either completely remove it from proximity (causing the
"exit report" code to reset everything to zero) or bring it closer to
the tablet so that it starts sending in-prox reports that are handled
by "wacom_intuos_general".