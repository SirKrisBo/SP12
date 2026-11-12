**NOTE IF YOU DECIDE TO DO THIS MOD**

**You'll need to remove IC48 and pick up a cable that can interpose the socket and connect to the PCB. This means moving the fly wire from IC83 and the capacitor on IC48 to the underside of the PCB. See the install instructions and pages 94-95 of the service manual.**

If you don't do this, you may lose memory on power on.

This project increases total available sample memory in the SP12 to 20s.

Note, I will not be held accountable for any damage to your SP12 or anyone attempting to modify their SP12. All repairs and mods should be carried out by a suitably qualified repairer.

I've been annotating the source code for a but over a year now but I hadn't done much with AI. There's been a lot of progress with firmware mods recently so when Chase Smith (from the FB group) shared with me how he managed to get the SP12 to use 20s of Ram, I signed up for a Claude account. Turns out that after the ground work I had done identifying code from text/data and annotating the source, I had made more than enough progress to get this moving.

If anyone is interested in developing for the SP12, it can be useful to fully understand the hardware (especially for an emullator). I've previously decoded the two PALs IC62 (turbo only) and IC69. I've also decoded the PROMs IC67 and IC88 so the full schematic can be understood. Relevant files are in this repo.

I'm usually around on the SP12/SP1200 Facebook group. Feel free to ask any questions there.
