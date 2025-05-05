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

- (explain the codes and functions used)
