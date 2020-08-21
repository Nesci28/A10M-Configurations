# GCODES

### Start
```
​;------------------------------------------
;*** Start Dual Nozzle/Bed Preheating ***
M140 S{material_bed_temperature_layer_0} ; start preheating the bed
M104 S{material_print_temperature_layer_0} ﻿T0 ; start preheating hotend
G28 ; home
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
M190 S{material_bed_temperature_layer_0} ; heat to Cura Bed setting
M109 S{material_print_temperature_layer_0} ﻿T0 ; heat to Cura Hotend
;*** End Preheating ***

​;------------------------------------------
;*** Single Print Start Tone
; M300 S1000 P500 ; chirp to indicate starting to print
;*** End Single Start Tone

​;------------------------------------------
;*** Setting up the Tools
;*** T0 (100 - 0)
M163 S0 P1
M163 S1 P0
M164 S0
;*** T1 (0 - 100)
M163 S0 P0
M163 S1 P1
M164 S1
;*** T3 (50 - 50)
M163 S0 P0.5
M163 S1 P0.5
M164 S2
;*** T4 (75 - 25)
M163 S0 P0.75
M163 S1 P0.25
M164 S3
;*** T5 (25 - 75)
M163 S0 P0.25
M163 S1 P0.75
M164 S4

​;------------------------------------------
;*** Draw a Nozzle Cleaning line on the Left Side of Bed
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little
G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
```

### End
```
M104 S0 ;extruder heater off
M140 S0 ;bed heater off
G91 ;relative positioning
G1 E-1 F300 ;retract the filament 1mm
G1 Z10 E-3 X-20 Y-20 F6000 ;move Z up and retract filament 3mm
M106 S255 ;fan at 100% to cool nozzle
G90 ;absolute positioning
G28 X0 Y0 ;home X and Y
G1 Y190 ;move bed forward
M84 ;steppers off
G4 P120000 ;wait 2 minutes (120 seconds)
M106 S0 ;fan off
```