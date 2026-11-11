**SP-12 20s memory expansion install guide - Rambo**

This mod replaces the SP12 sound memory (RAM and ROM) with two 512KB SRAMs although it can be done with 1 x 512KB and 1 x 256KB, I just use 2 x 512KB for simplicity. This gives 20s of battery-backed sample memory when a new firmware is installed (V3.0 Rambo).

**BEFORE YOU START**
- Acknowledge that you're doing this at your own risk. You're responsible for your own safety and your machine. Make sure you don't work on the machine while it's plugged into mains power and that you follow ESD precautions.
- Tools - you'll need soldering skills, a decent iron and a TL866ii programmer for the 16V8 and the firmware EPROMs.
- Get some antistatic IC storage tubes for your removed RAM chips, factory sound ROMs and IC48 (74HCT138)
- Note that in doing this mod, the factory ROM sounds and Cassette saving/loading are gone 
- Note that if you've saved any beats using factory sounds, those sounds will be gone also. The new firmware clears any data that references ROM sounds.
- The PCB is quite large and includes some sensitive components. I suggest buying an ESD-safe mat to work on.

**BOM:**
Rambo PCB Parts
Part              Value                    Link
LSB1              512KB SRAM               https://www.digikey.com.au/en/products/detail/alliance-memory-inc/AS6C4008-55PCN/4234586
MSB1              512KB SRAM               https://www.digikey.com.au/en/products/detail/alliance-memory-inc/AS6C4008-55PCN/4234586
U1                SN74HC138N               https://www.digikey.com.au/en/products/detail/texas-instruments/SN74HC138N/277221
C1                0.1uF                    https://www.digikey.com.au/en/products/detail/vishay-beyschlag-draloric-bc-components/K104K10X7RF5UH5/2356754
C2                10uF 16V                 https://www.digikey.com.au/en/products/detail/panasonic-industry/ECA-1CM100I/2688653
C3                0.1uF                    https://www.digikey.com.au/en/products/detail/vishay-beyschlag-draloric-bc-components/K104K10X7RF5UH5/2356754
C4                0.1uF                    https://www.digikey.com.au/en/products/detail/vishay-beyschlag-draloric-bc-components/K104K10X7RF5UH5/2356754
C5                10uF 16V                 https://www.digikey.com.au/en/products/detail/panasonic-industry/ECA-1CM100I/2688653
R1                10K 1/4W                 https://www.digikey.com.au/en/products/detail/yageo/MFR-25FRF52-10K/14626
R2                10K 1/4W                 https://www.digikey.com.au/en/products/detail/yageo/MFR-25FRF52-10K/14626
CN2               36-way IDC pin socket    https://www.digikey.com.au/en/products/detail/sullins-connector-solutions/PPPC182LFBN-RC/810257
CN3               36-way IDC pin header    https://www.digikey.com.au/en/products/detail/same-sky-formerly-cui-devices/SSK03-MPH-254-B18/28772107
J1                16-way IDC pin header    https://www.digikey.com.au/en/products/detail/same-sky-formerly-cui-devices/SSK03-MPH-254-B8/28772204

36-way Ribbon     Cable
Part              Value                    Link
36-way IDC        D89136-0101HK            https://www.digikey.com.au/en/products/detail/3m/D89136-0101HK/1885884
36-way IDC        D89136-0101HK            https://www.digikey.com.au/en/products/detail/3m/D89136-0101HK/1885884
Ribbon cable      3365/36SF                https://www.digikey.com.au/en/products/detail/3m/3365-36SF/3867399
My IDC tool       HT-214                   https://www.aliexpress.com/item/1005005494894754.html

16-way Ribbon Cable
Part              Value                    Link
IC48 adaptor      ADIP 16Z-LC              https://www.digikey.com.au/en/products/detail/assmann-wsw-components/ADIP-16Z-LC/924320
16-way IDC        D89136-0101HK            https://www.digikey.com.au/en/products/detail/cvilux-usa/CA2116SA100/15519178
Ribbon cable      3365/16 300              https://www.digikey.com.au/en/products/detail/3m/3365-16-300/1107219

SP12 Parts
Part              Value                    Link
IC26 PAL          16V8 (turbo only)        https://www.digikey.com.au/en/products/detail/microchip-technology/ATF16V8B-15PU/1118926
CN2               36-way IDC pin socket    https://www.digikey.com.au/en/products/detail/same-sky-formerly-cui-devices/SSK03-MPH-254-B18/28772107
CN3               36-way IDC pin header    https://www.digikey.com.au/en/products/detail/same-sky-formerly-cui-devices/SSK03-MPH-254-B18/28772107

**Preparing your SP12**
1. Unplug the mains, open the machine.
2. Unplug CN5 (connector near the audio jacks) and CN1 (50-way ribbon cable). Set the top housing aside.
3. Disconnect CN6, unscrew the LM350 from the chassis (VR4), unscrew all 1/4" jacks (16 in total), unscrew the PCB from the bottom of the chassis and gently remove it.
4. Remove all sound RAM and ROM chips from the lower right corner of your PCB, leave all memory chips under the power supply.
5. **Non-turbo only:** take three of the removed 6264 RAM chips and populate IC117, IC118 and IC119 (additional sequencer memory).
6. **Non-turbo only:** Program the jed file from the repo to a 16V8 GAL and replace the PAL at IC62.
7. Remove IC114 (ROM A 27C128) and IC115 (ROM B 27C64) and program the ROM A and ROM B files from the repo to new 27C128 and 27C64.
8. Check if your PCB has ECO 144 on the top or bottom of the main PCB. Refer to pages 94-95 of the SP12 Service Manual and ECO144.jpg in the repo for reference. ECO 144 connects a 1k resistor via fly wire between pin 2 of IC83 and pin 5 of IC48 and a 0.1uF cap between IC48 pins 5 and 8.
9. **If your PCB has ECO144 on the underside, skip the next step.**
10. If your PCB has ECO144 on the top side of the PCB, remove the fly wire/1k resistor and the 0.1uF cap from IC83/IC48 and solder to the underside of the PCB.
11. Remove IC48.
12. Solder a 36-way 

 **Bulding and connecting the board**
1. Build the Rambo PCB as per the schematic in the repo. Ensure CN2 is populated with a female IDC on the underside of the PCB and CN3 is populated with a pin header on the top side of the PCB.
2. Make the 36-way and 16-way ribbon cables as per the BOM, ensuring pin 1 is at the top left of all connectors.
3. Check chip orientation and us a multimeter to ensure there are no shorts between +5VS and GND. Best to also check every connection is as per the schematic.
4. Connect a 36-way ribbon cable from CN3 on the SP12 PCB to the Rambo PCB.
5. Connect a 16-way ribbon cable from IC48 socket to J1.
6. Connect the Rambo PCB to the SP12 PCB via CN2 on the underside of the Rambo PCB.

 **Reassembling your SP12**
1. Place the SP12 PCB back in the chassis.
2. Replace all 1/4" jack screws.
3. Replace all PCB screws.
4. Screw VR4 back to the chassis.
5. Reconnect CN1, CN5, CN6 and replace the top shell.
6. Let her rip!

Please raise an issue in the repo if I've missed any steps.
