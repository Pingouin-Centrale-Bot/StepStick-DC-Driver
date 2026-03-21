# StepStick DC Driver V2
A dual DC/H-bridge driver, designed as a drop-in replacement for a standard stepstick.  
Can drive two DC motors, or be used as four independent half-bridges.  
Designed around the `TB67H453FNG` IC. Datasheets can be found [here](Components/TB67H453FNG/).

![iso top view](media/iso_top.png)
![iso bottom view](media/iso_bottom.png)

## Specs
- Dual H-Bridge : Can drive two DC loads in both directions, or four DC loads unidirectionally
- 3.3A Max per channel
- Accepts an input power voltage from 4.5v to 44v
- Based around a 4 layer PCB, to improve heat dissipation (a heat sink and active cooling is highly recommended)
- The maximum intensity can be configured with the trimmer, by adjusting Vref
- Can be enabled or disabled with the `en` pin, just like a standard stepstick
- Compatible with both 5v and 3.3v logic voltage (If using 5v to power VCC, you must adjust the trimmer so that Vref stays below 3.3v!)

## Pinout
![pinout](media/top.png)

You can use the `Pololu_Breakout_A4988` symbol from the default KiCad library, with its accompanying default footprint. Here is a pinout correspondence for the pins :

| StepStick DC Driver | Pololu A4988 |
|:-------------------:|:------------:|
|         OB1         |      1B      |
|         OB2         |      1A      |
|         OA2         |      2A      |
|         OA1         |      2B      |
|         IA2         |      DIR     |
|         IA1         |     STEP     |
|         IB2         |     RESET    |
|         IB1         |      MS3     |
|         MSB         |      MS2     |
|         MSA         |      MS1     |
|         VCC         |      VDD     |
|          NC         |     SLEEP    |

> [!WARNING]
> You need to add a 100uf capacitor between the `VM` and `GND` pins.

## Configuration
If the resistors on the BOM are respected, the maximum intensity per channel can be configured by setting the `Vref` voltage :  
Imax(A)=Vref(v)
The driver will regulate the intensity to prevent it from getting higher.

The configuration is common to both H-bridge.

## Control
Channel A and B are both controlled by their own two pins `Ix1` and `Ix2`.  
They are 3 ways to control the outputs, configured respectively by `MSx` :

| MSx |       Mode       |
|:---:|:----------------:|
|  L  |    Phase/Enable control         |
|  H  |  PWM control                    |
| Hi-z/Open| Individual half bridge control |

### Phase/Enable control (MSx=Low)

| Ix1 | Ix2 | Ox1 | Ox2 |       Mode       |
|:---:|:---:|:---:|:---:|:----------------:|
|  L  | L/H |  L  |  L  |    Short Brake   |
|  H  |  L  |  L  |  H  |     Reverse      |
|  H  |  H  |  H  |  L  |     Forward      |

### PWM control (MSx=High)

| Ix1 | Ix2 | Ox1 | Ox2 |       Mode       |
|:---:|:---:|:---:|:---:|:----------------:|
|  L  |  L  |  Hi-Z  |  Hi-Z  |    Coast   |
|  L  |  H  |  L  |  H  |     Reverse      |
|  H  |  L  |  H  |  L  |     Forward      |
|  H  |  H  |  L  |  L  |     Short brake      |

### Individual half bridge control (MSx=Hi-z/Open)

| Ixx | Oxx |       Mode       |
|:---:|:---:|:----------------:|
|  L  |  L  |    Short Brake   |
|  H  |  H  |     Reverse      |

> [!NOTE]
> Current limiting does not work in half bridge mode, so beware of currents!

### All

If left open, a pin will be pulled down (considered L).
If you do not want to use one of the channels, you can simply not connect the output to anything.

## Fabrication notes
The constraints have been set up for Aisler's Beautiful Boards service.  
It is advised to use a .8mm total thickness instead of the standard 1.6mm to improve the thermal dissipation.

## Real world testing
To be done.

# StepStick DC Driver V1
See [here](/V1/).