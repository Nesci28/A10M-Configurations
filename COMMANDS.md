# List of Useful Commands

### Unified Bed Leveling
````
;------------------------------------------
;--- Setup and initial probing commands ---
;------------------------------------------
M502            ; Reset settings to configuration defaults...
M500            ; ...and Save to EEPROM. Use this on a new install.
M501            ; Read back in the saved EEPROM.

M190 S65        ; Not required, but having the printer at temperature helps accuracy
M104 S210       ; Not required, but having the printer at temperature helps accuracy

G28             ; Home XYZ.
G29 P1          ; Do automated probing of the bed.
G29 P2 B T      ; Manual probing of locations USUALLY NOT NEEDED!!!!
G29 P3 T        ; Repeat until all mesh points are filled in.

G29 T           ; View the Z compensation values.
G29 S1          ; Save UBL mesh points to EEPROM.
G29 F 10.0      ; Set Fade Height for correction at 10.0 mm.
G29 A           ; Activate the UBL System.
M500            ; Save current setup. WARNING: UBL will be active at power up, before any [`G28`](/docs/gcode/G028.html).
;---------------------------------------------
;--- Fine Tuning of the mesh happens below ---
;---------------------------------------------
G26 C P5.0 F3.0 ; Produce mesh validation pattern with primed nozzle (5mm) and filament diameter 3mm
                ; PLA temperatures are assumed unless you specify, e.g., B 105 H 225 for ABS Plastic
G29 P4 T        ; Move nozzle to 'bad' areas and fine tune the values if needed
                ; Repeat G26 and G29 P4 T  commands as needed.

G29 S1          ; Save UBL mesh values to EEPROM.
M500            ; Resave UBL's state information.
;----------------------------------------------------
;--- Use 3-point probe to transform a stored mesh ---
;----------------------------------------------------
G29 L1          ; Load the mesh stored in slot 1 (from G29 S1)
G29 J           ; No size specified on the J option tells G29 to probe the specified 3 points
                ; and tilt the mesh according to what it finds.
                ```
````

### Homing Offset

G28
M211 S0
G0 X1 Y-2 Z0
M428
M500

### BLTouch Offsets
M851 (To check infos)
M851 [X<linear>] [Y<linear>] [Z<linear>]
M851 X-39 Y1 Z0
M500

### Configure ESteps
M92 (To check infos)
M92 X81.2 Y81.73 Z410.36
M500

### StealthChop
M569 (To check infos)
M569 S0 Y
M500

### Bed Centering
<!-- X:124.00 Y:-116.00 Z:-12.00 -->
|------- 112.5 ------|
|                    |
|                    |
|                    |
|                    |
112.5            112.5
|                    |
|                    |
|                    |
|                    |
|------- 112.5 ------|
X = 112.5 - 124 = -11.5
Y = 112.5 - 116 = -3.5