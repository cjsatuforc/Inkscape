# Inkscape extension

 - K40 Raster -> Raster 2 Laser GCode generator
 
#Descriptions
- Raster 2 Laser G Code generator is an extension to generate laser engraving G code for the K40 laser cutter/engraver based on the Grbl (Arduino Uno controller), it can generate various type of engraving formats from a simple B&W (on/off) to a more detailed Grayscale (pwm)
- Best is the grey scale 10 bits pixel format
- This extension is based on 305 Engineering's original script
- The script has been altered to make the G code conform to Grbl 1.1e laser mode. All laser gcodes must be incorporated into the motion command e.g. G1 X0.10 Y2.10 F1000 S100 (where S100 is the laser command) and single M4/5 commands
- The script starts with a single 'M4' aka laser on and ends with 'M5' aka laser off. Inbetween lines there is no need for laser off commands. G0 will automatically turn off the laser while G1 turns it on again (laser is alternating between G0/1 commands)
- Tip; J Tech Photonics has written an excellent Gcode cutter Inkscape extension that I use for laser cutting


#Installing:

Simply copy all the files in the folder "Extensions" of Inkscape

>Windows ) "C:\<...>\Inkscape\share\extensions"

>Linux ) "/usr/share/inkscape/extensions"

>Mac ) "/Applications/Inkscape.app/Contents/Resources/extensions"


for unix (& mac maybe) change the permission on the file:

>>chmod 755 for all the *.py files

>>chmod 644 for all the *.inx files



#Usage of "Raster 2 Laser GCode generator":

[Required file: png.py / raster2laser_gcode.inx / raster2laser_gcode.py]

- Step 1) Resize the inkscape document to match the dimension of your working area on the laser cutter/engraver (Shift+Ctrl+D)

- Step 2) Draw or import the image

- Step 3) To run the extension go to: Extension > K40 Raster > Raster 2 Laser GCode generator

Following steps are to run the K40 Laser cutter engraver:

- Step 4) Upload the gcode.txt file into your Gcode sender (e.g. Cheton CNC on Github is a great one!)

- Step 5) Place the work object into the K40 cutter / engraver and jog the controls on the Gcode sender to the desired space

- Step 6) Issue a $C command to the K40 Controller to check the Gcode and cycle the feed

- Step 7) Set the K40 PWM/Manual switch to PWM

- Step 8) Cycle the Gcode on the Gcode sender and watch the K40 Laser cutter engraver doing its job (wear eye protection)


#Note
305 Engineering has created all the files except for png.py , see that file for details on the license.

Author (which is me writing this) has modified the script to fix the G code for Grbl otherwise Grbl would not run smoothly.
Grbl load every row into its ring buffer separately, so if the SXXX command is separate, it fills it in a separate block. Now you have bocks with motion and without motion. The planner is not able to glue the motions between blocks and the result is stutter.
Same for the M3 or M4 commands, the G parser sees them separately and stops the motion to allow the Spindle aka laser head to stop and start again. This is not what is desired. There is no need for multiple M commands since that is included into the G0 and G1 commands. G0 in Grbl always stops the laser by default and switches it on when it sees a G1 command without encounter a definite M5 stop command!
