# fluiddpi-ender3-hemera-bltouch
Creality Ender 3 Pro 4.2.7 contoller with hemera hotend and bltouch controlled by Raspberry Pi3 running fluiddpi

[stepper_x]
step_pin: PB9
dir_pin: PC2
enable_pin: !PC3
microsteps: 16
rotation_distance: 40
endstop_pin: ^PA5
position_endstop: 0
position_max: 235
homing_speed: 50

[stepper_y]
step_pin: PB7
dir_pin: PB8
enable_pin: !PC3
microsteps: 16
rotation_distance: 40
endstop_pin: ^PA6
position_endstop: 0
position_max: 235
homing_speed: 50

[stepper_z]
step_pin: PB5
dir_pin: !PB6
enable_pin: !PC3
microsteps: 16
rotation_distance: 8
endstop_pin: probe:z_virtual_endstop
#position_endstop: 0.0
position_max: 250
position_min: -5

[extruder]
max_extrude_only_distance: 100.0
step_pin: PB3
dir_pin: !PB4
enable_pin: !PC3
microsteps: 16
rotation_distance: 7.6
nozzle_diameter: 0.400
filament_diameter: 1.750
heater_pin: PA1
sensor_type: EPCOS 100K B57560G104F
sensor_pin: PC5
control: pid
# tuned for stock hardware with 200 degree Celsius target
pid_Kp: 30.149
pid_Ki: 1.595
pid_Kd: 142.453
min_temp: 0
max_temp: 250

[heater_bed]
heater_pin: PA2
sensor_type: EPCOS 100K B57560G104F
sensor_pin: PC4
control: pid
# tuned for stock hardware with 50 degree Celsius target
pid_Kp: 54.027
pid_Ki: 0.770
pid_Kd: 948.182
min_temp: 0
max_temp: 130

[bltouch]
sensor_pin: ^PB1
control_pin: PB0
x_offset: -40
y_offset: 2.5
#z_offset: 0.0

[bed_mesh]
speed: 120
horizontal_move_z: 5
mesh_min: 15, 15
mesh_max: 175, 202
probe_count: 5,3
algorithm: bicubic
fade_start: 1
fade_end: 10
fade_target: 0

[safe_z_home] 
home_xy_position: 115,115 # Change coordinates to the center of your print bed
z_hop: 10                 # Move up 10mm z_hop_speed: 5

[fan]
pin: PA0

[mcu]
serial: /dev/serial/by-id/usb-1a86_USB_Serial-if00-port0
restart_method: command


[screws_tilt_adjust]
screw1: 70.5,37.5
screw1_name: front left screw
screw2: 240,37.5
screw2_name: front right screw
screw3: 240,207.5
screw3_name: rear right screw
screw4: 70.5,207.5
screw4_name: rear left screw
horizontal_move_z: 10
speed: 50


[printer]
kinematics: cartesian
max_velocity: 300
max_accel: 3000
max_z_velocity: 5
max_z_accel: 100


[virtual_sdcard]
path: ~/gcode_files

[pause_resume]
recover_velocity: 25

[display_status]

[display]
lcd_type: st7920
cs_pin: EXP1_7
sclk_pin: EXP1_6
sid_pin: EXP1_8
encoder_pins: ^EXP1_5, ^EXP1_3
click_pin: ^!EXP1_2

[output_pin beeper]
pin: EXP1_1

[board_pins]
aliases:
  EXP1_1=PC6,EXP1_3=PB10,EXP1_5=PB14,EXP1_7=PB12,EXP1_9=<GND>,
  EXP1_2=PB2,EXP1_4=PB11,EXP1_6=PB13,EXP1_8=PB15,EXP1_10=<5V>,
  PROBE_IN=PB0,PROBE_OUT=PB1,FIL_RUNOUT=PC6

[gcode_macro CANCEL_PRINT]
description: Cancel the actual running print
rename_existing: CANCEL_PRINT_BASE
gcode:
  TURN_OFF_HEATERS
  CANCEL_PRINT_BASE
