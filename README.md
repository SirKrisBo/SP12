Alright, I've created this to document where I'm up to with trying to increase the sound memory available in the SP-12.

I've spent a lot of time in the schematic and toying with the memory but I'm fairly sure that the Z80 ASM is my blocker. This is just a collection of thoughts so it won't be particularly well orgainsed.

I'm going to preface this by making it clear up front that I am not a coder, I'm not an electrical engineer, I'm just some bloke who has been tinkering for years and wants to try and get the most out of my old SP12.

It's proving to be a right pain to nail down where in the firmware the SP-12 is deciding which pair of sound memory chip select signals to use. I've decided this is probably beyond me and thought I'd share some of what I have learned so far in case anyone can chime in. And if it's not going to be a solo effort, that means let's move this to a community effort, which also means let's make this open source.

I'm fairly certain I understand how the SP-12 can support 20s of memory in theory (which Dave Rossum himself confirmed in a video about the new SP1200). If you open up page 10 of 21 of the schematics in the service manual (page 72 of the PDF), you'll see that there are 8 signals coming from IC48 which is a 74HCT138. These are 8 sound memory chip select signals.

In its stock form, the SP12 is using SMCS0 and SMCS1 for the EPROM sounds. As you can see in the schematic, which of the SMCS that is active is determined by the inputs (SMA16, SMA17 and SMA18). These are sound memory address signals. It's important not to confuse these with A0 to A15 which are from the Z80's 16-bit memory interface. As far as the Z80 is concerned, the sound memory isn't really memory, it's just data. That's why there's is a whole bunch of logic ICs that form an external memory controller.

Anyway, different combinations of SMA16/17/18 correspond to different SMCS signals being active (SP12 circuit is active low). So if we see 000, that's SMCS0, 001 is SMCS1, 010 is SCMS2, 011 is SCMS3, 100 is SMCS4, 101 is SMCS5, 110 is SMCS6 and 111 is SMCS7.

If you look again at the schematic, you'll see that SMCS0 and SMCS1 are used for EPROM sounds (although the nets aren't named) and in the pages following SMCS6 and SMCS7 are used for the 192KB of Turbo memory.

If you keep scrolling down, you'll see that there's a page called Sound RAM Expansion (page 15 of 21 or page 77 of the pdf). On the left is every connection required to add another two 192KB banks of sound memory, including SMCS2-5.

I initially thought there might be something in the PAL (IC62) From what I can tell, the purpose of IC62 is to manage where data is being sent by sending strobes depending on what combination of signals it receives. This effectively maps the ports the Z80 uses to communicate across the SP-12. For example, when IC62 receives and I/O write with A7 = 1, A6 = 0, A5 = 1, that port range is $A0-$BF which is for the LCD display (also qualified by IORQ = 1, RD = 1 and RW = 1). So IC62 then sends a signal to the LCD chip enable so it starts receiving data on. See the IC62 logic equations for reference.

The outputs of IC62 that influence sound memory are CESM and and enable signal that connects to a 74HCT138 (IC41). The ENB signal to IC41 does have some influence in the sound memory world, but it doesn't have anything to do with the SMA16-18 signals. CESM however connects directly to the IC48 (ENB) that generates the SMCS signals. When CESM is active, it's just telling that a sound memory access cycle is happening, but it doesn't select which bank of sound memory is selected.

Where the bank selection actually happens is with 

Some success I did have in my early hardware testin was condensing the 24 x 8KB memory chips into two SRAMs (one for MSB and one for LSB). I wrote some logic equations for a 22V10 GAL that replaced IC49 with an interposer PCB which fans out the CMCS signals, instead using the SMCS signals as an address line which has the effect of creating 8LB "windows" that the SP12 acesses within the larger SRAMs. So if the firmware is aboe to be understood and modified to utilise memory attached to SMCS2-5, you wouldn't need to purchase 48 memory chips, it could be done with four, possibly even two.
