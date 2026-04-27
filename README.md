# UBC Solar x [**PCBWay**](https://www.pcbway.com/) Sponsorship for ___ Showcase!
> Below are all the PCBs UBC Solar has sponsored with [**PCBWay**](https://www.pcbway.com/). 
> * ⭐ [**PCBWay**](https://www.pcbway.com/) provides reliable PCB manufacturing and assembly services, offering a wide range of cost-effective options for rapid prototyping and small-volume production. 
> * 🌟 [**PCBWay**](https://www.pcbway.com/) kindly supported all these project with manufacturing and design review! Please visit their site if you need PCB manufacturing or assembly services. 
> * ⭐ There are lots of options for low-cost prototyping and small series production. 
> * 🌟 Their 24/7 support for payments and for reviewing makes our teams production scale rapdiy!
# Author: Luke Santosham (Power and Signals)
## Acknowledgements 
A huge thank you to PCBWay for manufacturing the GPS Breakout Board. Their support was invaluable in converting this projects into a reliable component for our newest solar car. PCBWay provides high-quality PCB manufacturing and assembly services that are excellent for rapid prototyping and custom engineering projects.

<p align="center"><img width="389" height="419" alt="image" src="https://github.com/user-attachments/assets/ca6688d3-8d74-46ba-b76c-6e94bf4b5b8e" /></p>

<p align="center">_Figure 1: Front view render of the GPS breakout board_</p>

## Overview
The goal of the GPS project was to develop a breakout board that could interface with our telemetry board to give us location data for both real-time pit crew analysis and post-race strategy analysis.

When reviewing our solar car's performance, having accurate location data is critical as it allows us to corroborate other data (such as speed and acceleration) with our car’s position on track. This is the first iteration of this board and is part of UBC Solar’s initiative to move towards full in-house production.

The main features of this board include:
* Access to the full GNSS satellite constellation for location tracking worldwide.
* Dead reckoning for accurate position estimation in case of a lost satellite connection.
* An active antenna for preemptive filtering of GNSS signals.
* I2C and UART communication with our telemetry board.
* A rechargeable backup 3V battery to enable “hot starts” which allows reception of location data 2 seconds after startup

## Schematic
The GPS breakout board schematic can be broken up into 4 main sections: the connectors, the power, the NEO-M9V, and the debug LEDs.

<p align="center"><img width="930" height="904" alt="image" src="https://github.com/user-attachments/assets/77a5a36d-553f-4e1d-b968-746f00a07743" /></p>

<p align="center"> *Figure 2: Schematic of the GPS breakout board* </p>

### 0. Connectors
The GPS breakout board interfaces with the telemetry board using 14 asymmetric male headers to prevent it being connected incorrectly. The multiple ground pins ensure a more uniform ground plane which is critical for other sections of the board such as the coplanar waveguide.

It also connects to an exterior active antenna using an industry-standard SMA connector. A bias-T circuit is used to ensure that power and GNSS signals can be transmitted using the same cable.

Finally, the breakout board has two male pins that can be shorted to disable the backup battery.

### 1. Power
This section houses the standard decoupling capacitor along with this backup 3V battery. A simple charging circuit is also implemented to allow the backup battery to charge when not in use.

### 2. NEO-M9V
The NEO-M9V is the main IC for this project. It receives data from the GNSS signal as well as data from an integrated IMU and uses both sources to calculate the car’s location. In the event that the GNSS signal is lost, the NEO-M9V enters dead reckoning mode and makes its best prediction of the car’s location using the IMU data. The final location solution is then broadcast to the telemetry board using I2C.

### 3. Debug LEDs
Debug LEDs were added to the board to indicate power and satellite reception. The TIMEPULSE pin on the NEO-M9V can be configured to blink when the board is receiving a satellite signal. Therefore, along with using it for its intended purpose of providing a synchronized clock, we used it as a debug LED to indicate if the NEO-M9V was in dead reckoning mode.




