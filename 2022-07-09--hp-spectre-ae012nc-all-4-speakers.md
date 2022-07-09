# HP Spectre ae012nc All 4 Speakers
Steps to get all 4 speakers and internal mic working. Tested on Ubuntu 22.04., previously speakers were working, but mic popped.

1. Install hdajackretask (`apt install alsa-tools-gui`)
2. Set the following pin config:
- Set pin `0x14` to "Internal speaker"
- Set pin `0x17` to "Internal speaker (back)"
- Set pin `0x1e` to "Dock Line out"
3. `Apply now`  isn't working for some reason, but `Install boot override`  worked fine, after reboot all 4 speakers are working.

Hdajackretask boot override installs the following files:
- `/etc/modprobe.d/hda-jack-retask.conf`
- `/lib/firmware/hda-jack-retask.fw`

https://bugzilla.kernel.org/show_bug.cgi?id=189331