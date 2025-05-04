# BMS-Carrier
Carrier Board for the Battery Management System of the Midnight Sun Solar Rayce Car

## Requirements
- Serve as the main logic board for the BMS of the vehicle.
- Interface with current sensing and analog front-end boards to sense current and monitor/balance the battery pack's Li-Ion cells.
- Control the main relays for the battery and solar panels.
- Control the fans used for cooling the battery pack.
- Implement a kill-switch which will override control of the relays if pressed. 

## Design Overview 
### AFEs
The AFE boards measure and balance cells on the battery pack while also measuring cell temperature. The AFE interface uses isoSPI, a proprietary LT protocol built for their BMS ICs. The interface must provide isolation between every node, as each AFE is referenced to a different level within the pack and isolation must be maintained between high and low voltage systems for safety. 

### Current Sense
An isolated I2C interface allows for communication to a current sensing board, while maintaining isolation between high and low voltage systems. An optocoupler provides isolation for the incoming “alert” signal from current sense.

### Relays
BMS Carrier has individual control over the relays which comprise the main power switch, which are pack negative, pack positive, and solar relay. Each relay is individually controlled with a low side N-Channel MOSFET. The relays limit their back EMF to 0, eliminating the need for flyback diodes. 

### Kill Switch
The sources of the MOSFETs for each relay are tied together to the drain of a 4th N-Channel MOSFET, controlled by the kill switch to provide overriding control over the energizing of the relays.

## Schematic 
![BMS-SCH-1](https://github.com/liamssky/BMS-Carrier/blob/main/BMS-SCH-1.png)
![BMS-SCH-2](https://github.com/liamssky/BMS-Carrier/blob/main/BMS-SCH-2.png)
![BMS-SCH-3](https://github.com/liamssky/BMS-Carrier/blob/main/BMS-SCH-3.png)

## PCB layout
![BMS-LAYOUT-1](https://github.com/liamssky/BMS-Carrier/blob/main/BMS-LAYOUT-1.png)

## 3D Model
![BMS-3D-FRONT](https://github.com/liamssky/BMS-Carrier/blob/main/BMS-3D-FRONT.png)


## Revision 1.0
![PCS-REV1](https://github.com/liamssky/PCS/blob/main/PCS-REV1.png)

This board was soldered by me and I wound the coupled-inductor / transformer which I calculated the ideal inductance, winding ratio, and size for. 

## Next Steps

Revision 1.2 has been created with modifications made from my findings during testing and review of datasheets and application notes. This board will be assembled soon and tested further.

