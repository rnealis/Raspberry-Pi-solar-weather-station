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







