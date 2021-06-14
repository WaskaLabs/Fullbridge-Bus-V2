# Fullbridge-Bus-V2
TO-247 Full-bridge with full wave voltage doubled capacitor bank. A fully integrated High Side for SSTCs, DRSSTCs, and HV sources.

PCB and Kits available for sale in the WaskaLabs store on tindie.com

The full-bridge bus 2.0 is a fully integrated "high side" system designed for SSTC, DRSSTC Tesla coils, and other high power inverter applications.


Finished System Specs:

- Works with 110 and 220 AC voltages (requires relevant components for voltage!)
- High current design capable of ~300+ Apk
- Low stray inductance bridge design
- TO-247 MOSFETs or IGBTs - Surface mounted for easy and fast replacement
- Direct mount to large 100mm X 120mm heatsink for maximum temperature handling
- 10A RMS bridge rectifier and bus capacitors (voltage doubler configuration, can be set up as standard rectified) with high current input for mains AC or variac AC voltage.
- Safety circuits (6x20mm fuse (Comes with fast-blow 10A), bus capacitor bleeder resistor)
- Gate drive components (Series resistor, antiparallel switch-off diode, TVS diode) and marked solder pads for easy GDT connection.
- Snubber capacitors (0.66uF total)
- Optional diodes (freewheel or TVS on inverter output)
- High current screw connectors used (All metal)
- Optional MMC and CT board for all-in-one DRSSTC system (Coming soon)


Comes with:

- PCB
- SMD components (pre-soldered)
- Connectors (pre-soldered)
- Bridge rectifier (pre-soldered)
- Bleeder resistor (pre-soldered)
- Fuse holder and 10A fast-blow fuse (pre-soldered)
- 4x silicone heat pads
- Printed hole placement guide


Required - Not included in kit:

- Bus capacitors (~$4 each eBay, Amazon) (Choose appropriate voltage for your country)
- IGBTs or MOSFETs (Mouser, Digikey) (Spec for your specific design)
- 100x120mm Heatsink ($10 on Amazon)
- M3 screws and nylon standoffs
- GDT (DIY or available as an addon)


IGBT and MOSFET recommendations:

- FGA60N65SMD (Best in my experience) (Great for DRSSTC)
- FGA60N60SMD (Similar to 60N65) (Great for DRSSTC)
- IRFP460 (Great for higher frequency, low current SSTC designs)


Rectifier & Bus:

The voltage doubler configuration doubles the peak-to-peak voltages seen on the AC input. For example, US mains is 110V RMS, but ~170Vpp. So if US mains is connected directly to the input, it should charge the capacitor bank to 2 x 170V (~340V). The capacitors on the bus are connected in series, so each capacitor should be rated to hold the full Vpp of the mains input (in the US, I like to use 250V). It is highly advisable to spec these caps to handle >30% more than the voltage you expect to see in them, so a 500V total cap charged to 340V is a safe bet. In 220V land, you will want to use 450V capacitors for a total of 900V. Bare in mind that the total capacitance of the bus will decrease by half as the voltage doubles. So two 250V 1000uF caps in series will give you 500V at 500uF. This should be kept in consideration when designing the system.

Recommendations:

- US mains (110V RMS) - 250V 1000uF capacitors (10mm lead spacing, 35mm dia max)
- International mains (220V RMS) - 450V 680 - 1000uF capacitors (10mm lead spacing, 35mm dia max)

If you plan to modify the board to a standard rectified voltage, spec your caps accordingly. I would suggest ~100V caps for US mains (200V total rating), doubling it for 220V mains, at the highest uF you can get in the correct footprint to fit the PCB.

The KBU-1010 bridge rectifier is rated for 10A continuous and 300A surge. If you plan to run high currents monitor the temperature of the rectifier and add a heatsink if needed. The fuse is a 6x20 cylindrical type and are standard and available cheap online or locally at hardware stores. 


Inverter & Gates:

The inverter portion is pretty straightforward. The switches (IGBTs or MOSFETs) are connected directly to the heatsink with a silicone heat pad (sil pad) to electrically isolate the switches from the heatsink (Very important!). The pins of the switches should be bent upwards before mounting, then bent to contact the pads and soldered in place. Removal can be done with a soldering iron, but the simple solution is to use hot air to heat the pads. It is easier to do this after unscrewing the switches from the heatsink, otherwise you may not be able to disconnect it easily. The leads can also be clipped first if this becomes an issue.

The Gate Drive Transformer (GDT, typically 1:1:1:1:1) should be wound and phased. The secondary windings of the GDT should be soldered directly to the pads with the phase wires soldered to the pads with silkscreen around them, and the anti-phase ends soldered to the other pad. Make sure to wind the GDT with enough extra wire to make it easy to mount (I like to mount them to the side of the heatsink). One important note is that the GDT secondaries should ALL BE LENGTH MATCHED to avoid skew in the timing between the switches. 

The gate components are not one size fits all. The gates and waveforms should be thoroughly tested to assure the switching waveform is correct. If it isn't, you may need to change gate resistors and remove the diodes, etc. until you can get it right. The TVS diodes are SMAJ26 26V TVS which is designed for up to 24V drive voltages. If using lower voltages you may want to change the value of the TVS. Tuning gates is not in the scope of this document, but it is an art and takes some time to get right. But having a proper driver, GDT, gate components, and the right switches are important in getting this right. A good resource for this is Ritchie Burnett's GDT waveform troubleshooting guide.


Step by Step Assembly:

1. Spec and purchase all components for your design. Refer to BOM.
2. Solder bus caps onto PCB and test the DC voltage across the bus as well as voltage drain from bleeder resistor (recommended through a variac!).
3. Drill and tap all M3 holes in the PCB (Use printable guide). Aluminum is soft, so be careful here! If you accidentally strip the holes, you can run a longer screw all the way through and a nut on the back of the heatsink.
4. Screw down TO-247 IGBT switches with a sil pad to keep it electrically separated from the heatsink. I like to use thermal paste on both sides of the silpad for added thermal conduction. Make sure to bend the pins upwards so the PCB fits in between them.
5. Mount the PCB to the heatsink using standoffs (3 - 5mm is usually fine). Make sure the PCB connections and solder points do NOT and will NOT touch the heatsink!!
6. Bend the IGBT switch leads down to the pads and solder them in place.
7. Mount the GDT and solder the wires to the gate drive pads. Ensure correct phasing.


Testing Gates:

1. Connect a proper driver to the GDT primary and drive the gates at a frequency as close as possible to your desired operation frequency (Function generator to the GDT driver works well)
2. Test the Gates:
	1. Probe the gate drive signal to assure gate waveforms look good using an oscilloscope.
	2. Change out components or circuit elements as needed to get a good gate drive waveform. Not always needed.
	3. Assure all gates look good before proceeding...


Testing Inverter:

1. Make sure you are interrupting the output or have a high enough impedance to not drain your capacitors. This is design dependant, but should be done for any SSTC/DRSSTC design
2. Connect the load to the inverter output (Primary coil you plan to drive or high Z load for low voltage testing) (NO SECONDAY IF SSTC/DRSSTC)
3. Connect a variac and set the DC bus voltage to a low test voltage (~20-50V)
4. Hook up an oscilloscope between D/S leads on one of the switches and test the waveform. Do this with all switches. Assure they are all switching properly before proceeding.
5. Now test the output of the inverter. Be sure you are seeing a proper square wave. If you see a stair step pattern, one of the switches may be phased wrong. You may see droop in the center of the square wave depending on your load. Careful with MMCs here is using DRSSTCs. You wont be driving at resonance so this may give you a weird output. Try removing it if it causes issues.
6. Now you can increase the voltage and watch the waveforms on the scope to assure it is working as expected.


Troubleshooting:

- Make sure all gates are phased properly and being driven in the correct direction
- Test different gate drive components and values
- Make sure none of the switches are bad. Rare but it happens. If the bridge blows, all the switches may need to be replaced even if some seem okay
- Make sure you are providing enough drive current to the GDT
- Make sure your load has enough impedance to not just drain the caps too fast to see inverting voltages

This design is meant to be configurable and modular to be able to fit many topologies. There are far too many variations in application, drive methods, and use cases for me to be able to help in the debugging. If you have issues getting it to work, do your research and read up on forums. I have provided schematics and resource information on the system so that you have all information necessary to figure out the issue. But standard troubleshooting like adding/removing components and thinking through the design will be the only way to get it running. I am happy to help when I can, but ultimately what you build with this cannot be fixed IT style.
