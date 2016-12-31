# Various Inkscape extensions

 - K4o Raster -> Raster 2 Laser GCode generator
 - 
 
#Descriptions
- Raster 2 Laser GCode generator is an extension to generate Gcode for the K40 laser cutter/engraver based on the Grbl Arduino Uno controller, it can generate various type of outputs from a simple B&W (on/off) to a more detailed Grayscale (pwm)
- This extension is based on 305 Engineering's script
- The script has been altered to make the G code conform to Grbl 1.1e laser mode. All laser gcodes must be incorporated into the motion command e.g. G1 X0.10 Y2.10 F1000 S100 (where S100 is the laser command)
- The script starts will M4 laser on and ends with M5 laser off. Inbetween lines there is no need for laser off commands. G0 will automatically turn off the laser


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
I have created all the file except for png.py , see that file for details on the license
