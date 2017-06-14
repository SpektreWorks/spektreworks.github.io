---
layout: default
title: Copter Carrier Board
order: 0
permalink: /carrier_board
nav:
- Introduction: introduction
- - Features At-A-Glance: features-at-a-glance
- Power: power
---

<p align="center">
    <img src="/assets/images/AngleFoamTop.jpg" class="img-responsive" style="max-width:500px"  />
</p>

# Introduction
The primary purpose of the SpektreWorks Multi-Rotor Carrier Board for the Pixhawk Cube is to reduce the rat’s nest of wires and modules typically associated with a multi-rotor assembly. It provides built-in power distribution, redundant power supplies for the autopilot, built-in fail-over power selection, a separate payload power regulator, and many other features.

While this carrier board is geometrically optimized for quadcopters and octocopters, it provides connections for every function of the Pixhawk autopilot. Therefore, this board can be integrated into any vehicle type that is supported by the Pixhawk Cube.
 
## Features At-A-Glance
- Up to 12-cell Lithium battery (50.4V)
- 140A continuous current with 280A surges
- Power and signal for ESCs conveniently located in corners
- 12V navigation light power available at each corner
- Built-in power distribution
- Built-in voltage and current sense
- Redundant power supplies for flight critical components
- Payload connectors with resettable fuses for 5V, 12V, and direct battery power
- Good power and error indicator lights
- Built-in buzzer with volume control
- Connectors for every function of Pixhawk Cube
- Easily accessible PWM voltage level selector (3.3V or 5V)
- Resistant to ground bounce on PWM signal
- Connector-compatible with standard ProfiCNC carrier board
- Connector ports for debugging IO and FMU processors

# Power

The system battery should be connected directly to the large pads labeled “MAIN PWR”. Pads are available on both top and bottom of the board. No external power brick is necessary, as voltage and current sense is done directly on the board. Pay special attention to the polarity symbols, as there is no reverse protection. Batteries up to 12S, or 50.4V, may be used.

The power distribution system is rated to supply 140A to the ESCs when exposed to stagnant air at room temperature, with surges up to 280A. If the board will have continuous airflow across it (exposed to prop wash during flight), significantly higher currents may be sourced. Alternatively, if the board will be mounted within an enclosure or if flown on a very hot day, it may be necessary to de-rate the current capacity. For users that expect to operate their vehicle continuously at high currents (over 100A), it is recommended that ground testing is done with a temperature gun prior to flight. The surface of the carrier board should never exceed 100°C.

In order to accurately read the voltage and current using the built-in sensors on the board, the following parameters should be set in the Pixhawk Cube:

|    Parameter           |    Value    |
|------------------------|-------------|
|    BATT_AMP_OFFSET     |    0.45     |
|    BATT_AMP_PERVOLT    |    50       |
|    BATT_CURR_PIN       |    3        |
|    BATT_MONITOR        |    4        |
|    BATT_VOLT_MULT      |    15.3     |
|    BATT_VOLT_PIN       |    2        |



### General Use Power Connectors
There are three general use power connectors to source power for external devices and payloads. They are labeled as J1, J14, and J19 in white ink on the board. Molex brand Clik-Mate connectors are used for the power connectors.


| Reference	| Voltage         | Max Current | Pinout                 | Mating Part Number|
|-----------|-----------------|-------------|------------------------|-------------------|
| J1        | Battery Voltage | 3A	        | 1-3: Battery, 4-6: GND | Molex 5023800600  |
| J14       | 5.3V            | 1.5A        | 1-2: 5.3V, 3-4: GND    | Molex 5023800400  |
| J19      	| 12.2V	          | 2A	        | 1-2: 12.2V, 3-5: GND   | Molex 5023800500  |

All three general use power connectors are independently fused with resettable fuses. If a short occurs, the fuse will cut power to the offending connector. If this occurs, identify the short and remove it. Wait a couple of minutes and the fuse should reset. **The fuses may not react instantly and damage may occur to your carrier board if an external device has a short.** SpektreWorks is not responsible for damage caused by an external device.

### ESC Connections
At each corner of the board are solder pads for ESC power. The power wires from your ESCs may be soldered to the pads on the top or bottom surface.

Next to the ESC power pads are 3x3 0.1” header pins. The top row of pins provides power for navigation lights. The center pin is 12V and the right pin is ground. The left pin is unused and should be removed. The bottom two rows of pins are for the ESC PWM signal. **Make sure you do not plug in an ESC cable into the top row of this connector.** These two rows correspond to two of the “Main Out” connections of the Pixhawk Cube. The rows are labeled in white ink on the board. The “S”, “+”, and “-“ correspond to the PWM signal, power, and ground, respectively.  All eight Main Out connections are available in the four corners of the board. It helps to look at the header pins from the side to see which row corresponds to which label.

<p align="center">
    <img src="/assets/images/PWMPins.png" class="img-responsive" style="max-width:900px"  />
</p>

By default, the board does not supply power to the ESC PWM connections. However, if no BEC is available to power the ESCs, the user may bridge JP1 with solder to provide 5.3V from the board to the ESCs. **If JP1 is bridged with solder, do not plug a BEC into the ESC connections.**

<p align="center">
    <img src="/assets/images/PWMJumper.png" class="img-responsive" style="max-width:800px"  />
</p>

Most commercially available ESCs expect 3.3V PWM signals from the autopilot to control the motor. This is the default setting of a Pixhawk Cube. If, however, you require 5V PWM signals, there is a convenient switch for this on the carrier board. The switch is located on the right side of the board and is labeled “3V PWM” and “5V PWM”. Use a pen or a sharp tool to slide the switch to the desired voltage.

### Aux Pins
Additionally, the six “Aux Out” connections are available as part of a 3x8 group of headers on the right side of the board. Refer to the labels in white ink to identify each pin. By default, the board does not supply power to the center pins of the Aux channels. If desired, the board can supply 5.3V to the Aux rail by bridging the pads of JP2 with solder. **If JP2 is bridged with solder, do not connect an external power supply to the Aux pins.**

<p align="center">
    <img src="/assets/images/JP2Bridge.png" class="img-responsive" style="max-width:800px"  />
</p>
