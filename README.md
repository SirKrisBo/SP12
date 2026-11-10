This project increases total available sample memory in the SP12 to 20s.
Note, I will not be held accountable for any damage to your SP12 or anyone attempting to modify their SP12. All repairs and mods should be carried out by a suitably qualified repairer.

I've been annotating the source code for a but over a year now but I hadn't done much with AI. I fired up Claude a few days ago and after the ground work I had done identifying code from data (and some 1541 code I found that the SP12 bit bangs directly via the disk port) turns out I had made plenty of progress to get this moving.

If anyone is interested in developing for the SP12, it can be useful to fully understand the hardware. I've previously decoded the two PALs IC62 (turbo only) and IC69. I've also decoded the PROMs IC67 and IC88 so the full schematic can be understood. Relevant files are in this repo.

I'll keep a clean ROM pair in this repo with no significant mods other than the following:
- Splash screen updated to say "Vers 3.0 Rambo" as a tip of the hat to the original planned Rambo upgrade.
- 20s of sample memory available (assuming hardware changes have been completed). Note that max file size remains 2.5s. This is a hardware limitation. In fact, if you record 8 x 2s samples, that's 16s usage, but because of how memory is arranged into 8 segments there is only room for a max 0.5s file size (8 x 0.5 = 4 seconds). This cannot be changed without significantly altering the hardware.
- All factory sounds and parameters for factory sounds have been removed. All pads are set to tune by default and odd pads to output 7, evens to output 8.
- If you attempt to load sounds from firmware v2.6 it will clear memory first. This is necessary to avoid errors.
- Cassette save/load has been removed to make space for memory management. Pressing disk, 1 displays Cassette Gone.
- All pads have been changed to A1..D8 as per SP1200. Any pad can be selected from the sample, assign voice screen by pressing the pad you want to record a sample to. Numbers still work if you really want to use numbers. I've also added the same functionality to the truncate page. Number keys silently select, pads select and play the sample.

I only made these changes to make it easier to use all 32 pads. No other mods have been made to this firmware to keep it as stock as possible. I may make other changes but for now, here's a close to stock firmware that allows you to add more memory.

I'm usually around on the SP12/SP1200 Facebook group. Feel free to ask any questions there.

**NOTE IF YOU DECIDE TO DO THIS MOD**

**You'll need to remove IC48 and pick up a cable that can interpose the socket and connect to the PCB. This means moving the fly wire from IC83 and the capacitor on IC48 to the underside of the PCB.**
If you don't do this, you may lose memory on power on.
