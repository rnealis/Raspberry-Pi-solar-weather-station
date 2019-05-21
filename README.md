# Raspberry-Pi-solar-weather-station

# Description
The objective of this project is to build a weather station that could be placed in a remote polar environment and will be able to function for several years without any need for maintenance or data retrieval. The solar panel will charge a series of large car batteries that will be used to power a Raspberry Pi that will retrieve and transmit data collected from various climate sensors.

Calculating how much power will be consumed by our system is a very important task so that we can provide the system with enough power to last through the dark winter of the polar environment. This task consumed most of our time and therefore the following page will outline the power consumption of a Raspberry Pi under different conditions.

# Parts list

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
  
  
  ## Data



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







