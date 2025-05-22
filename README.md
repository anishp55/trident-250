# klipper_config

currently kind of a mess, working on fixing it up so its easier to understand.
if you see anything that could use fixing, feel free to open an issue.

i currently have
 * beacon ABL with touch and scanning calibration before print.
 * beacon ABL implements the nifty Nozzle Thermal Calibration offset from @YanceyA/BeaconPrinterTools
 * ECRFv2 - mostly works, need to see if i can implement per gate servo angle to help with loading and print
   the fixes for some of the hardware to fix loading issues.
     
   
notes: when using orcaslicer with this config i've found that you need to include the following for the
start gcode.  The first 2 lines seem to be the most important.  I've set mine to beacon contact calibration temp
```
M104 S150 ; Stops OrcaSlicer from sending temp waits separately
M140 S55
MMU_START_SETUP INITIAL_TOOL={initial_tool} TOTAL_TOOLCHANGES=!total_toolchanges! REFERENCED_TOOLS=!referenced_tools! TOOL_COLORS=!colors! TOOL_TEMPS=!temperatures! TOOL_MATERIALS=!materials! FILAMENT_NAMES=!filament_names! PURGE_VOLUMES=!purge_volumes!
MMU_START_CHECK
PRINT_START_MMU BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP=[first_layer_temperature[initial_extruder]] CHAMBER=[chamber_temperature] ADAPTIVE=YES
SET_PRINT_STATS_INFO TOTAL_LAYER=[total_layer_count]
MMU_START_LOAD_INITIAL_TOOL
LINE_PURGE
```

otherwise filament changes take forever, not sure why.