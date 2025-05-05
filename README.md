# Interfacing IWR6843AOP mmWave sensor with Radxa CM5 Module

## Brief introduction

- Sensor module used   -> https://www.mistralsolutions.com/product-engineering-services/products/som-modules/60ghz-industrial-radar-module-rom/
- profile_2d.cfg       -> .cfg file provided in the out of box demo file (https://www.mistralsolutions.com/software-downloads/)
- radar_raw_dump.py    -> dumps the raw sensor data to a .txt dile in raw_dump folder.
- mmwave_to_mavlink.py -> Reads and parses data from AoP module into format required for ```OBSTACLE_DISTANCE_3D``` and sends the message to the flight controller
- reference to understand TLV format of UART communication used here https://dev.ti.com/tirex/explore/node?node=A__AaagUFIod1NcG0sE-noAfw__radar_toolbox__1AslXXD__LATEST

## Dependencies

- numpy
- pyserial
- apscheduler
- pymavlink 

## mmwave_to_mavlink.py

### mavlink_loop()

- shows system is alive by sending heartbeat messages
- responds to specific incoming messages from flight controller with dedicated callbacks
- runs indefinitely in a background thread to process MAVLink traffic

### send_obstacle_distance_3D_message()

- sends updated ```OBSTACLE_DISTANCE_3D``` message to the flight controller
- The MAVLink message is sent in the background at the rate of 60Hz here

### serialConfig()

- initialises the CLI and Data UART ports and dumps the .cfg file to the AOP module

### parseConfigFile()

- Obtain profile and frame configuration information from .cfg file

### readAndParseData68xx()

- read UART messages from Data port and store in buffer
- identify start of message by locating start of magic word (refer to link provided for UART comms)
- if type of message is ```MMWDEMO_UART_MSG_DETECTED_POINTS```, then obtain parameters.
- Clear the buffer of data that has already been processed

### update()
- update the parameters to be sent in ```OBSTACLE_DISTANCE_3D``` to the FC
