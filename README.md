
# TMDA Interference Dataset

This dataset provides interference measurements with Wireless Sensor Networks (WSN) on Time Division Multiple Access (TDMA) timeslot level on low-cost hardware. The sniffer nodes run on a TDMA based protocol with a superframe duration of 100 ms and 100 timeslots 0.9 ms each. The average signal level of each timeslot is measured directly on the sensor nodes and is reported to the network  coordinator. 
This enables the possibility to measure the distributed interference for every node in the WSN in time and amplitude. The additional time aspect will allow identifying certain patterns in the interference.
# Measurement Procedure

## Hardware and Protocol
Measurements in this dataset are conducted with the Energy and Power  Efficient  Synchronous  SensorNetwork (EPhESOS) protocol [1]. EPhESOS is a Time Division Multiple Access (TDMA) network protocol for industrial applications, where every node within the network gets a dedicated timeslot where it is allowed to transmit data. The beacon of the network and the possible timeslots are collected in a so-called superframe that is repeated continuously.  The following figure depicts the superframe format of the EPhESOS protocol.
<p align="center">
<img src="Images/ephesos_frame.png" height="50%" width="50%" >
</p>



As hardware platform, the Nordic™ NRF52840 controller with integrated transceiver was used. For the communication in the WSN the EPhESOS protocol is combined with the Bluetooth Low Energy (BLE) physical (PHY) layer. 
<p align="center">
<img src="Images/hardware.png" height="25%" width="25%" >
</p>


The measurements themselves are conducted by sniffer nodes,  which report the average signal level of each timeslot to the network coordinator, where all data is collected. The average signal level of the timeslots is measured using energy detection, a feature in 802.15.4, and available in many commercial transceiver controllers like the  NRF52840.  It allows an automatic averaging of the signal level of the current channel for a duration of 128 μs, which is used to measure the signal level within all timeslots of the superframes.



## Schematic Interference Detection

Sensor nodes that belong to the same TDMA-WSN have a dedicated timeslot, where they are allowed to transmit data to the network coordinator. Therefore these nodes will try to transmit with the same period as the superframe, though of course they are not required to transmit in every superframe. Interference from other devices and other network protocols can appear at any timeslot, however, if the communication of this device is somehow periodic, a certain pattern can be observed if multiple superframes are considered.
The figure in the following depicts the measurement of a sniffer node for four superframes. The interferer sends periodically, but with a slightly higher period compared to the superframe. As a result, the interference will occur in each superframe a little bit later. The resulting pattern can be seen on the right.

<p align="center">
<img src="Images/meas_idea.gif" height="100%" width="100%" >
</p>



# Example Measurement
The following figure shows one example measurement of this dataset. The x-Axis represents the timeslot number (in our case 100 timeslots per superframe) and the y-Axis represents the superframes, i.e. the subsequent measurements. If in a timeslot the measured signal level is above a −90 dBm threshold, it is marked black, otherwise it is left empty.  In the dataset also the corresponding RSSI values are available, though not depicted here for easier understanding. 

In this measurement two interferer are placed nearby which transmit at a period of 102.4 ms and 92.4 ms,respectively. The following figure  depicts  the measurement,  showing  the interference  of  the  timeslots  over  100  superframes.

<p align="center">
<img src="Images/example_meas_raw.png" height="70%" width="70%" >
</p>

The  first  interference  with  the  102.4 ms  period  is larger compared to the 100 ms superframe duration, therefore the  interference  is  observed  in  each  subsequent  superframe  shifted to the right, resulting in the lines moving to the right in the Figure. The second interference with 92.4 ms has a lower period, i.e., the resulting interference is every superframe several timeslots earlier. This pattern is  hard  to  distinguish  from  the  additional  noise  and  random  access of the real measurement.

# Dataset

## Structure of Dataset
Each subfolder in the [dataset](Dataset) folder represents one measurement set for a certain scenario. Each of these sets contains a [description.json](Dataset/test_set/description.json) with the important parameter of the measurement, the corresponding manufacturer ID of the sniffer nodes, and the timeslot they are operating. Additionally, there is a "measurement_setup" field that contains a description of the setup and peculiarity of this measurement set.

The actual measurement of the sniffer nodes can be found in the [snifferX.csv](Dataset/test_set/sniffer1.csv) that contains the RSSI values of each TDMA-timeslot for each measured superframe. If for certain superframes and/or timeslots measurements are not available the specific fields are left empty.

## Open the Dataset
The dataset real measurement data is provided as a CSV file which allows opening the data in various programming languages and programs. For Python we shall give a small code example to open the sniffer measurement with Pandas and convert the superframe number and the measurements itself to NumPy arrays for further evaluation:


```python
#import needed packages
import pandas as pd
import numpy as np

#load dataframe (make sure to use ',' as separator and "SF" as index)
df = pd.read_csv("test_set/sniffer1.csv", sep=',' , index_col = "SF")

#get 1D-array of superframe numbers
superframe_number = df.index.to_numpy()
#get 2D-array of sniffer values (RSSI for each superframe and timeslot)
sniffer_measurement = df.to_numpy()    
```

# Contact
If you have any comments, questions or feedback please contact
- Julian Karoliny: julian.karoliny@silicon-austria.com

# License 
This dataset is distributed under the [Creative Commons Attributions License 4.0 (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/).


# Acknowledgement
This work is funded by the InSecTT project (https://www.insectt.eu/). InSecTT has received funding from the ECSEL Joint Undertaking (JU) under grant agreement No 876038. The JU receives support from the European Union’s Horizon 2020 research and innovation programme and Austria, Sweden, Spain, Italy, France, Portugal, Ireland, Finland, Slovenia, Poland, Netherlands, Turkey. The document reflects only the author’s view and the Commission is not responsible for any use that may be made of the information it contains.

# Literature

[1] H.  Bernhard,  A.  Springer,  A.  Berger,  and  P.  Priller,    “Life  cycle  of wireless  sensor  nodes  in  industrial  environments,”  in2017  IEEE  13th International  Workshop  on  Factory  Communication  Systems  (WFCS), 2017, pp. 1–9.