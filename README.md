
# TMDA Interference Dataset

This dataset provides interference measurements with Wireless Sensor Networks (WSN) on Time Division Multiple Access (TDMA) timeslot level on low-cost hardware. The sniffer nodes run on a TDMA based protocol with a superframe duration of 100 ms and 100 timeslots 0.9 ms each. The average signal level of each timeslot is measured directly on the sensor nodes and is reported to the network  coordinator. 
This enables the possibility to measure the distributed interference for every node in the WSN in time and amplitude. The additional time aspect will allow identifying certain patterns in the interference.
# Measurement Procedure

## Hardware and Protocol
Measurements in this dataset are conducted with  the  Energy  and  Power  Efficient  Synchronous  SensorNetwork (EPhESOS) protocol [1]. EPhESOS is a Time Division Multiple Access (TDMA) network protocol for industrial application, where every node within the network gets a dedicated timesot where it is allowed to transmit data. The beacon of the network and the possible timeslots are collected in a so-called superframe that is repeated continously.  The following figure depicts the superframe format of the EPhESOS protocol.

<img src="Images/ephesos_frame.png" height="50%" width="50%" >


As hardware platform, the Nordic™ NRF52840 controller with integrated transceiver used. For the communication in the WSN the EPhESOS protocol is combined with the Bluetooth Low Energy (BLE) physical (PHY) layer. 

<img src="Images/hardware.png" height="30%" width="30%" >

The measurements itself are conducted by  sniffer  nodes,  which  report  the average  signal  level  of  each  timeslot  to  the  network  coordinator, where all data is collected. The average signal level of the timeslots is measured using energy detection, a feature in 802.15.4 and available in  many  commercial  transceiver  controller  like  the  NRF52840.  It allows  an  automatic  averaging  of  the  signal  level  of  the  current channel for a duration of 128 μs, which is used to measure the signal level within all timeslots of the superframes.



## Schematic Interference Detection


<img src="Images/meas_idea.gif" height="100%" width="100%" >




# Example Measurement

To  demonstrate  the  interference  measurement  and  visualize  the patterns of periodic interference, experiments with the following setupare  conducted.  In this measurement two interferer are placed nearby which transmit at a period of 102.4 ms and 92.4 ms,respectively. The following figure  depicts  the measurement,  showing  the interference  of  the  timeslots  over  100  superframes.

<img src="Images/example_meas_raw.png" height="70%" width="70%" >

 If in a timeslot the measured signal level is above a −90 dBm threshold, it  is marked  black,  otherwise  it  is  left  empty.  In the dataset also the corresponding RSSI values are available, though not depicted here for easier understandn.  
 
The  first  interference  with  the  102.4 ms  period  is larger compared to the 100 ms superframe duration, therefore the  interference  is  observed  in  each  subsequent  superframe  shifted to the right, resulting in the lines moving to the right in the Figure. The second interference with 92.4 ms has a lower period, i.e., the resulting interference is every superframe several timeslots earlier. This pattern is  hard  to  distinguish  from  the  additional  noise  and  random  access of the real measurement.





# Dataset


# Literature

[1] H.  Bernhard,  A.  Springer,  A.  Berger,  and  P.  Priller,    “Life  cycle  of wireless  sensor  nodes  in  industrial  environments,”  in2017  IEEE  13th International  Workshop  on  Factory  Communication  Systems  (WFCS), 2017, pp. 1–9.