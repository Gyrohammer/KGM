# [Klipper for the Kobra Go!](https://reddit.com/r/anycubic/comments/10cwm16/install_klipper_on_kobra_go_or_neo/){target=_blank}
Thanks to /u/xpeng121 we now have Klipper on the Go! Klipper is similar to marlin, but offloads a lot of the complex calculations to a head unit (pc/raspi) which allows for faster print speeds and artifact-reduction. 

### Euipment Needed
|Item|Quantity|Description|
| ----------- | ----------- | ----------- |
|RaspberryPi/Linux Box| 1 | The 'head unit' of the operation, these handle the klipper instance.|
|32-Bit Motherboard with USB| 1 | The mainboard continues to operate the actual printer. It acts on instructions sent from the head.|

!!! note "Note on Pi Usage"
    A raspberry pi is not the end-all-be-all of a klipper setup, but it is one of the more compact and well supported solutions on the market. If a Pi is unobtainable for whatever reason, or out of your budget, dont worry! If you have an older laptop or PC you can use that to run klipper. You just need a machine that is capable of running linux, if you have that you can run klipper! To install and configure follow the guides on the main site, [Klipper.org](https://www.klipper3d.org/){target=_blank}

This mod can be done with a completely stock machine! It should be the first upgrade one performs if they have the ability to do so.

### Installing Klipper

1. Clone the klipper repository onto a local drive with the following command: 

``` git clone https://github.com/Klipper3d/klipper.git ```

2. To compile the firmware, follow the tutorial found on the official site: [Klipper Installation and Configuration](https://www.klipper3d.org/Installation.html)

3. Install the firmware by moving the compiled bin file onto an SD card. Rename this file to firmware.bin and insert it into the printer. Turn the printer on and wait for about 5min while it updates. Remove after that time and reboot.

4. Config file:
   
    !!! warning
        **Please review these settings and fully understand them before implementation. I've blocked some out that could be problematic and should throw errors. Ensure this is correct before you deploy!**

    ??? note "Kobra Go"
        ~~~
        # This file contains a configuration for the Anycubic Kobra Go printer.
        #
        # See docs/Config_Reference.md for a description of parameters.
        #
        # To build the firmware, use the following configuration:
        #   - Micro-controller: Huada Semiconductor HC32F460
        #   - Communication interface: Serial (PA3 & PA2) - Anycubic
        #
        # Installation:
        #  1. Rename the klipper bin to `firmware.bin` and copy it to an SD Card.
        #  2. Power off the Printer, insert the SD Card and power it on.
        #  3. The the LCD will be stuck on the Firmware-update screen.
        #     Just Wait for 3-5 minutes to ensure the firmware is flashed.
        #  4. After waiting, shutdown the printer and remove the SD Card.

        [stepper_x]
        step_pin: PA12
        dir_pin: PA11
        enable_pin: !PA15
        microsteps: 16
        rotation_distance: 40
        endstop_pin: !PH2
        position_endstop: -13
        position_min:-13
        position_max: 236
        homing_speed: 50

        [stepper_y]
        step_pin: PA9
        dir_pin: PA8
        enable_pin: !PA15
        microsteps: 16
        rotation_distance: 40
        endstop_pin: ^!PC13
        position_endstop: -9
        position_min:-9
        position_max: 230
        homing_speed: 50

        [stepper_z]
        step_pin: PC7
        dir_pin: !PC6
        enable_pin: !PA15
        microsteps: 16
        rotation_distance: 8
        endstop_pin: ^PC14
        position_endstop: 0
        position_min: -10
        position_max: 255
        homing_speed: 5

        [extruder]
        step_pin: PB15
        dir_pin: PB14
        enable_pin: !PA15
        microsteps: 16
        rotation_distance: 31.07
        max_extrude_only_velocity: 25
        max_extrude_only_accel: 1000
        nozzle_diameter: 0.400
        filament_diameter: 1.750
        heater_pin: PB8
        sensor_type: ATC Semitec 104GT-2
        sensor_pin: PC3
        min_extrude_temp: 170
        min_temp: 0
        max_temp: 250
        control: pid
        pid_kp: 19.56
        pid_ki: 1.62
        pid_kd: 200.00

        [heater_bed]
        heater_pin: PB9
        sensor_type: EPCOS 100K B57560G104F
        sensor_pin: PC1
        min_temp: 0
        max_temp: 120
        control: pid
        pid_kp: 97.1
        pid_ki: 1.41
        pid_kd: 1675.16

        [bed_mesh]
        speed: 200
        horizontal_move_z: 2.5
        mesh_min: 5, 5
        mesh_max: 215, 215
        probe_count: 5, 5

        [probe]
        pin: PA1
        x_offset: -20.8
        y_offset: 0
        z_offset: 0
        samples: 3
        samples_result: average
        samples_tolerance_retries: 3
        sample_retract_dist: 0.5
        speed: 2
        lift_speed: 4

        [safe_z_home]
        home_xy_position: 0, 0
        speed: 5
        z_hop: 10
        z_hop_speed: 15

        [controller_fan controller_fan]
        pin: PB12

        [heater_fan extruder_fan]
        pin: PB13

        [fan]
        pin: PB5
        cycle_time: 0.00005 #20kHz

        [output_pin enable_pin]
        pin: PB6
        static_value: 1
        # This pin enables the bed, hotend, extruder fan, part fan.

        [mcu]
        serial: /dev/serial/by-id/usb-1a86_USB_Serial-if00-port0
        restart_method: command

        [printer]
        kinematics: cartesian
        max_velocity: 300
        max_accel: 500
        max_z_velocity: 4
        max_z_accel: 100
        ~~~

5. Additional Starting Gcode

    This can be added to the main directory of klipper through the webui. Simply create a new file inside the directory named, gcode.cfg and paste the code below into it. 

    ??? note "Start Print Macro"
        ```
        [gcode_macro START_PRINT]
        gcode:
            {% set BED_TEMP = params.BED_TEMP|default(60)|float %}
            {% set EXTRUDER_TEMP = params.EXTRUDER_TEMP|default(190)|float %}
            M140 S{BED_TEMP} ;Start bed heating
            G21 ;metric values
            G90 ;Use absolute coordinates
            G28 ; Home all axes
            G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
            G1 X0.1 Y20 Z30 F5000.0 ; Move to start position
            M109 S{EXTRUDER_TEMP} ; Set and wait for nozzle to reach temperature
            M190 S{BED_TEMP} ;wait bed temp
            G92 E0 ; Reset Extruder
            G1 Z0.3 ; Start close to bed
            G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
            G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
            G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
            G92 E0 ; Reset Extruder
            G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
            G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish

        [gcode_macro END_PRINT]
        gcode:
            M400 ; Wait for current moves to finish
            M220 S100 ; Reset Speed factor override percentage to default (100%)
            M221 S100 ; Reset Extrude factor override percentage to default (100%)
            G91 ; Set coordinates to relative
            G1 F2400 E-1 ; Retract filament 3mm at 40mm/s to prevent stringing
            G0 F5000 Z20 ; Move Z Axis up 20mm to allow filament ooze freely
            # Turn off bed, extruder, and fan
            M140 S0
            M104 S0
            M106 S0

            G90 ; absolute pos
            G1 X5 Y220 F3000 ;clear head and bring bed to the front
            # Disable steppers
            M84 ; Disable stepper motors

        [delayed_gcode startup_gcode]
        initial_duration: 0.1
        gcode:
            G28

        #[gcode_macro POWER_OFF_PRINTER]
        #gcode:
        #  {action_call_remote_method(
        #    "set_device_power", device="printer", state="off"
        #  )}

        #[gcode_macro POWER_ON_PRINTER]
        #gcode:
        #  {action_call_remote_method(
        #    "set_device_power", device="printer", state="on"
        #  )}
        ```


    !!! info
        This gcode macro will auto-home your printer after it is connected to klipper.

## Slicer Settings

Within most slicers there is an area for start and end gcode. These fields contain gcode that is run at the start and end of a print, often for prepping or storing the print head before a print. 

### Start Print Field

```
M104 S0 ;for removing temp gcode added by slicer automatically

M140 S0 ;for removing temp gcode added by slicer automatically

START_PRINT BED_TEMP=bed_temp_variable_of_your_slicer EXTRUDER_TEMP=extruder_temp_variable_of_your_slicer
```

### End Print Field
```
END_PRINT
```

