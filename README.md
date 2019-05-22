# Raspberry Pi Solar Weather Station

# Description
The objective of this project is to build a weather station that could be placed in a remote polar environment and will be able to function for several years without any need for maintenance or data retrieval. The solar panel will charge a series of large car batteries that will be used to power a Raspberry Pi that will retrieve and transmit data collected from various climate sensors.

Calculating how much power will be consumed by our system is a very important task so that we can provide the system with enough power to last through the dark winter of the polar environment. This task consumed most of our time and therefore the following page will outline the power consumption of a Raspberry Pi under different conditions.



# Parts list

Item | Link
-|-


# Power Consumption
  ## Methods
  
 *Measuring the instantaneous current that the Raspberry Pi draws was a very difficult task and we started in very basic places and progressively built up our method.*
 
 *  **Filming the DMM** - For our first method we connected two DMM’s to our Raspberry Pi, one in parallel and one in series, to measure the current and watch the voltage. We situated the two instruments next to each other alongside a stopwatch. With this setup we used a smartphone to film these three screens in one frame. We then turned on the power to our Raspberry Pi at the same time that we started the stop watch. After the Raspberry Pi powered up, we transmitted data from the temperature sensors a few times and then proceeded to shut off the Raspberry Pi. 
We were able to analyze this video to get some decent data on the power consumption of the Raspberry Pi by slowing the video down to get the current and voltage as a function of time on the stopwatch. 
* **Watching current on DC function generator** - Due to the lack of sophistication of the previous method, we ran the trial again however this time including the ammeter that is present of our DC function generator to confirm the readings that we were getting.  
* **USB Ammeter** - The last irritation that we used was a USB Ammeter to read our results.

  Item | Link
  -----|------
  DMM|https://www.fluke-direct.com/product/fluke-115-digital-multimeter-with-true-rms?gclid=EAIaIQobChMI4pDFkues4gIVg4CfCh3lTgCsEAAYASAAEgJIRPD_BwE 
  DC Function Generator |https://www.circuitspecialists.com/csi3005sm.html 
  USB Ammeter| https://www.amazon.com/Digital-Multimeter-Ammeter-Voltmeter-Capacity/dp/B00YRSV3J8 
  Stop Watch and Camera | Cell Phone
  
 **Summary** - These are all great ways to easily measure the power consumption of a Raspberry Pi or something similar as the procedure only includes equipment that are commonly found in electronics labs. The method requires minimal technical skills and can be replicated in the most basic electronics lab. Although this method is very easy to do and provides some good data for the power consumption, it relies on actually going back through a video to retrieve the data. Since we wanted to test the power consumption of the Raspberry Pi under various conditions we wanted to create a method that would allow us to repeat the process quickly as well as get more accurate data. For this reason, we decided to explore using a digital multimeter chip that fits into our circuit which would give us something close to the instantaneous power consumption. 
 
 
  ## Optimal Methods
  *The method that we used to collect the most accurate data on the power consumption of a Rapsberry revolved around using an INA 219 chip. Below we will outline how we went about utilizing this piece of technology to gather the power consumption of a Raspberry Pi under several differnt conditions.*
  
  ### Set Up
  ![Screen Shot 2019-05-22 at 10 11 48 AM](https://user-images.githubusercontent.com/50841778/58184376-fb93c600-7c7e-11e9-85fa-e6e8cc17b5d7.jpeg)
  <img width="539" alt="Screen Shot 2019-05-22 at 10 50 13 AM" src="https://user-images.githubusercontent.com/50841778/58184860-ea978480-7c7f-11e9-8b8f-3712f8f106e8.png">
  
  
  
  The INA219 is a high side DC current, voltage and power sensor that is rated to be accurate within 1%. We set up the INA219 sensor by appropriately connecting the sensor to a raspberry pi (see link below) and using a DC function generator.
  
  The Raspberry Pi that you are testing must be powered through the GPIO pins. The Raspberry Pi that you are using to collect data can be powered through the micro USB power port. 
  
  ### Procedure
  * Using Python scripts, we were able to record data every second regarding voltage, power and current. 
  * Once we collected the data, we used Excel macros to plot the power consumption of the device over time. 
  * We also used Excel to find the average power consumption of the Raspberry Pi while under multiple scenarios. Using these scenarios, we approximated the power consumption of the individual parts of the Raspberry Pi below. 
  
  
  The python script that we used on the Raspberry Pi were we collected the data was:
```
import os
import socket
import datetime
import time
from ina219 import INA219
from time import sleep

# READ VOLTAGE, CURRENT, AND POWER
ina = INA219(shunt_ohms= 0.1,
                          max_expected_amps =0.6,
                          address=0x40)

ina.configure(voltage_range=ina.RANGE_16V,
                            gain=ina.GAIN_AUTO,
                            bus_adc=ina.ADC_128SAMP,
                            shunt_adc=ina.ADC_128SAMP)

#print ('voltage:', v)
#print ('current:', i)
#print ('power:', p)

print ("voltage (V), current (mA), power (mW)")

while True:
    # GET DATE AND TIME
    now = datetime.datetime.now()
    time = now.strftime("%Y-%m-%d %H:%M:%S")
    time = str.replace(time,' ','%20')
    
    v = ina.voltage()
    i = ina.current()
    p = ina.power()

    print (time, v, i, p)
    sleep(1)

```
  
  
  ## Data
  
  
Test | Sensors | Transmitting | Bluetooth | WIFI | HDMI | Monitor | Average Power Consumption
-----|---------------------|---------------|-----------|------|------|----------|--------------------------
1 | YES | NO | YES | YES | YES | NO | 558.60 mW
2 | YES | YES | YES | YES | YES | NO | 601.30 mW
3 | YES | NO | NO | YES | YES | NO | 551.50 mW
4 | YES | YES | NO | YES | YES | NO | 574.61 mW
5 | NO | NO| NO | YES | YES | NO | 597.43 mW
6 | NO | NO | NO | YES | NO | NO | 525.02 mW
6 | NO | NO | NO | NO | YES | YES | 852.95 mW
Charge Controller | NO | NO | NO | YES | NO | NO | 934.47 mW


Item | Measurement
-----|------------
WIFI Transmission (frequency = 1 per minute) | ~33 mW
Idle Pi | Unknown
Bluetooth | ~17 mW
HDMI | ~72 mW
WIFI | Unknown
4 Sensors | 46~ mW
Efficiency of Charge Controller | System with the charge controller consumes 78% more energy than the system alone. Note: the 78% will likely change with power input to the charge controller (my hunch is if you put more power into the charge controller, you will get less power loss)

*FOR MORE DETAILED DATA AND PROJECT DESCRIPTION SEE ATTACHED PDF'S*


# Sensors

Here are just a few sensors that we used in our project that we thought worked really well and were super reliable


Sensor Name | Purpose | Link
------------|---------|-----
DS18B20 | Ground temperature sensors that can have different lengths for different depths | https://www.adafruit.com/product/381
BME680 | Gas, Humidity, Pressure, Temperature Sensor I²C, SPI Output | https://www.digikey.com/product-detail/en/bosch-sensortec/BME680/828-1077-1-ND/7401321?utm_adgroup=Sensors%20&%20Transducers
MCP9808 | Extremely accurate temperature sensor | https://www.digikey.com/en/product-highlight/m/microchip-technology/mcp9808-silicon-temp-sensor?utm_adgroup=Integrated%20Circuits&slid=&gclid=EAIaIQobChMIr7ej-aCt4gIVEUgNCh25HgnxEAAYASAAEgJKzvD_BwE



# Solar panel 
This part of the project is very unique each stations needs due to where they would be implemented. The things we needed to consider when selecting our solar panel were:
* Lack of sunlight for 10 weeks - The solar power must be able to collect enough power from the sun when it is available in order to fully recharge the battery for when there is no sunlight again. We believed off of our own intuition that any solar panel that had could produce 50 Watts or greater would be good enough. 
* Extreme wind - with extreme wind we would need to make sure that we minimize the surface area that the solar panel has so that it does not act as a sail and eventually destroy the whole station. This again is something worth tailoring towards a specific project and should be calculated considering the conditions of the location where the station is going. 
* Remote area - since we plan to put our solar panel in a remote area which is not only hard to get to but also very expensive we want to ensure that our entire system can work without ever having to revisit the site. This impacted our solar panel decision because we want to ensure that the panel will be functional for several years without having to go and replace the battery. 

We researched many different options and finally settled on ordering a 100 W and 12V solar panel made by Solartech. (https://www.mrsolar.com/solartech-spm100p-ts-f-100w-12v-solar-panel-w-large-j-box/) However, when this solar panel arrived we realized that it was too large and would act as sail. We have not yet figured out the replacement yet but we are leaning towards getting a panel that only provides around 50 Watts of power. The reason why is because when we have light, we will have light all day. In other words, when the light comes out we will have no problem charging the battery. 



# Charge controller
The charge controller is a very important part of the entire system as it drops down the voltage from the 12V battery to the 5V current that the Raspberry Pi runs off of. The charge controller also makes sure that the solar panel does not back drain the battery at night when there is no sunlight being absorbed by the panel. 

An inherent flaw of all charge controllers is that there is some energy loss in the process of dropping the voltage from 12V to 5V. However, there are two different types of charge controllers, PWM and MPPT. MPPT is known to be substantially better at conserving energy than PWM but MPPT is also substantially more expensive. We also could not find any charge controllers that would be suitable for a remote weather station as they are all designed for industrial grade solar panels (over 200 Watts). 

We decided to get the following PWM charge controller and it was the best option based on both price and efficiency. 

Charge Controller: https://www.amazon.com/PowMr-60a-Charge-Controller-Adjustable/dp/B07KW4DHX6/ref=sr_1_2?keywords=powmr+60a+charge+controller&qid=1556820017&s=electronics&sr=8-2 







