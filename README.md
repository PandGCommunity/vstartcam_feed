VSTARTCAM
=========

VSTARTCAM - OpenWRT custom packages for extends functionality


Supporting
==========

If you like our work, please consider supporting us on [Opencollective](https://opencollective.com/openipc) or [PayPal](https://www.paypal.com/donate/?hosted_button_id=C6F7UJLA58MBS). Thanks a lot !!!
<p align="center">
<a href="https://opencollective.com/openipc" target="_blank"><img src="https://opencollective.com/webpack/donate/button@2x.png?color=blue" width=300 /></a>
<a href="https://www.paypal.com/donate/?hosted_button_id=C6F7UJLA58MBS"><img src="https://www.paypalobjects.com/en_US/IT/i/btn/btn_donateCC_LG.gif" alt="PayPal donate button" /> </a>
</p>


License
=======

This sources is free software; you can redistribute it and/or modify it under the terms of
the GNU Lesser General Public License as published by the Free Software Foundation;
either version 2.1 of the License, or (at your option) any later version.

You should have received a copy of the GNU Lesser General Public License along with this
script; if not, please visit http://www.gnu.org/copyleft/gpl.html for more information.


Software
========

* libsrtp        =>
* libsrtp2       =>
* pjproject      =>
* rt5350f-wm8988 =>
* two_motor_74HC =>


Usage
=====

    cd OpenWRT
    mkdir vstartcam
    echo "src-git vstartcam https://github.com/PandGCommunity/vstartcam_feed.git" >./feeds.conf  # if not have it in feeds.conf
    ./scripts/feeds update vstartcam        # or ./scripts/feeds update -a
    ./scripts/feeds install rt5350f-wm8988  # or ./scripts/feeds install -a

    make menuconfig                         # select rt5350f-wm8988 in kernel modules dir (Sound Support)
    make package/rt5350f-wm8988/compile     # {clean,compile,install}
    make package/rt5350f-wm8988/install     # {clean,compile,install}

    make package/index V=99                 # Create index of packages

