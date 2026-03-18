# StepStick DC Driver
A dual DC/H-bridge driver, designed as a drop-in replacement for for a standard stepstick.  
Designed around the `TB67H481FNG` IC. Datasheets can be found [here](Components/TB67H481FNG/).

![iso top view](media/iso_top.png)
![iso bottom view](media/iso_bottom.png)

## Specs
- Dual H-Bridge : Can drive two DC loads in both directions
- 1.8A Max per channel
- Accepts an input power voltage between 8.4 and 44v
- Based around a 4 layer PCB, to improve heat dissipation (a heatsink and active cooling is higly recommended)
- A maximum intensity can be configured with the `MS1` and `MS2` pins
- Can be enabled or disabled with the `en` pin, just like a standard stepstick
- Compatible with both 5v and 3.3v logic voltage

## Pinout
![pinout](media/top.png)

## Configuration
If the resistors on the BOM are respected, the maximum intensity per channel can be configured with the `MS1` and `MS2` pins :

| MS1 | MS2 | Torque            | Max current per channel   |
|:---:|:---:|:-----------------:|:-------------------------:|
|  L  |  L  | 100%              | 1.8A                      |
|  L  |  H  | 71%               | 1.3A                      |
|  H  |  L  | 38%               | .7A                       |
|  H  |  H  | 0% (Output OFF)   | 0A                        |

If left open, a pin will be pulled down (considered L).
The configuration is the same for both channels.  

## Control
Channel A and B are both controlled by their own two pins Ix1 and Ix2 :

| Ix1 | Ix2 | Ox1 | Ox2 |       Mode       |
|:---:|:---:|:---:|:---:|:----------------:|
|  L  |  L  |  L  |  L  |    Short Brake   |
|  L  |  H  |  L  |  H  | Couter clockwise |
|  H  |  L  |  H  |  L  |     Clockwise    |
|  H  |  H  |  H  |  H  |    Short brake   |

If left open, a pin will be pulled down (considered L).
If you do not want to use one of the channels, you can simply not connect the output to anything.

## Fabrication notes
The constraints have been setup for Aisler's Beautiful Boards service.  
It is advised to use a .8mm total thichness instead of the standard 1.6mm to improve the thermal dissipation.

## Real world testing
To be done.
