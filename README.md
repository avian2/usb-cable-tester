# A tool for measuring USB cable resistance

![USB cable tester](figures/usb-cable-tester-photo.jpg)

This is a tool for measuring USB cable resistance very similar to the [FemtoCow's cable resistance tester][1]. It supports A-to-micro B, A-to-mini B, A-to-C and C-to-C cables. The measured resistance is the sum of the resistances of the Vbus, GND lines in the cable as well as contact resistance in connectors.

The tool allows measurement of resistance in the range of 100 milliohms with approximately 1% accuracy, which is much better than what a typical multimeter can achieve in this range. It is not a stand-alone instrument - in addition to this tool you need a laboratory power supply with an output of at least 2 V at 1 A and a voltmeter with a 2 V (or a similar) scale.

This repository contains design files that you can use to make your own copy of the tool:

* Gerber and Excellon drill files for PCB manufacture,
* (very simple) schematic and
* bill of materials.

The PCB layout has minimum copper clearance and track size of 6 mil.  Unfortunately this is required for the USB C connectors. This feature size should not be a problem for a modern PCB prototyping fab, but is pretty challenging to achieve if you intend to etch the PCB yourself. Other connectors have larger clearances, so if you don't need USB C connectors you might still be able to use this design.


## Warning about active USB C cables

Some USB C cables contain electronics for signal conditioning and/or cable identification. Although as far as I know using them with this tool shouldn't damage them, use caution and be aware that you might damage your cable.


## How to use

The following procedure measures the resistance of the cable at 1 A of current:

1. Set power supply output to 0 V, connect to the terminals marked *Supply*.

2. Connect voltmeter to terminals marked *Calibrate*, set to 2 V DC scale or similar.

3. Connect one end of the USB cable you want to measure to one of the two connectors on the right edge (type A or C).

4. Connect the other end of the cable to one of the three connectors marked *Short* (type mini-B, micro-B or C).

5. Increase power supply output until voltmeter reads 1 V.

6. Move voltmeter leads to terminals marked *Measure*.

7. Voltmeter reading directly shows resistance of cable in ohms.

8. Set power supply output to 0 V. Disconnect cable.

Alternatively, if your power supply doesn't allow you to accurately set
voltage, or if you want to measure resistance at a different current *Iset*, you can
use the following:

1. Set power supply output to 0 V, connect to the terminals marked *Supply*.

2. Connect voltmeter to terminals marked *Calibrate*, set to 2 V DC scale or similar.

3. Connect one end of the USB cable you want to measure to one of the two connectors on the right edge (type A or C).

4. Connect the other end of the cable to one of the three connectors marked *Short* (type mini-B, micro-B or C).

5. Increase power supply output until voltmeter reads approx. *Iset* / 1 ohm. Note voltage shown by voltmeter as *Ucalibrate*.

6. Move voltmeter leads to terminals marked *Measure*. Note voltage shown by voltmeter as *Umeasure*.

7. Set power supply output to 0 V. Disconnect cable.

Resistance of the cable can then be calculated as:

*Rcable* = *Umeasure* / *Ucalibrate*


## Note on accuracy

The accuracy of this tool largely depends on the accuracy of the 1 ohm resistor. 1% SMD resistors are cheap and widely accessible, so this is what is easily achievable. PCB layout has been carefully designed so that the resistances of the PCB traces and connecting cables, except for the short loopback trace, are not included in the measurement (Kelvin connections).

The accuracy of the power supply output voltage setting has no effect (using the second procedure), as long as it is reasonably stable over time.

The calibration of the voltmeter also doesn't affect the accuracy of the result as long as its scale is roughly linear over the 0.1 V to 1 V range. Any linear scale error is cancelled out in the equation above.

Note however that you are measuring the resistance of the cable as well as the contact resistance in the connectors. This means that measurements of the same cable will vary because connectors will sit slightly differently. Just slightly moving the cable can result in different readings. This depends a lot on the quality of connectors (both on the cable and on the tool itself).


## References

* [FemtoCow's cable resistance tester][1].
* [SZDIY USBcablecracker][2].
* Blog post about [measuring USB cables][3].

[1]: https://www.tindie.com/products/FemtoCow/usb-cable-resistance-tester/
[2]: https://github.com/szdiy/USBcablecracker
[3]: https://www.tablix.org/~avian/blog/archives/2019/06/measuring_usb_cable_resistance/
