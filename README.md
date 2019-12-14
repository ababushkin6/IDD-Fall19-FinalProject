# IDD Final Project

**Fabio Daiber** (*github: fpdaiber; discord: Fabio*)

**Ziyu(Ross) Liu** (*github: dlydb; dsicord: ross_lzy*)

**Alan Babushkin** (*github: ababushkin6; discord: alan.babushkin*)


## Ai.re - Monitor body heat emission in rooms and use it as natural heating

### Description

The idea behind the project is to monitor the temperature inside a room using multiple temperature sensors across the room and see how it changes based on body heat emission by tracking of the number of people going in and out of the room.

We use two ultrasonic sensors at the entrance of an room to detect movement. Based on which sensor is triggered first, we know if people are walking in our out of the room. We have two high-accuracy temperature and humidity sensors spread across the room to track the average room temperature. Both the temperature sensors as well as the ultrasonic sensors are each connected to a Raspberry Pi that sends the signal wirelessy to our server. 

Our website allows users to input the room size, human activity level in the room and desired temperature. Based on this information, the average temperature and the number of people in the room, we estimate the heat emission caused by the human bodies in the room and calculate the time it takes for the room to heat up to the desired temperature solely based on this emission.

### Interaction plan

We have two interactions: 

1) Walking past the ultrasonic sensors changes the count on the website of the people in the room in real-time. 
2) Our website also allows users to input the room size, human activity level in the room and desired temperature, based on that the required time to heat up the room changes.

### Initial Design and Paper Prototypes

Our design was to have three temperature sensors, each connected to an Arduino and the Arduino connected to a Raspberry Pi. We also used an Arduino to read the ultrasonic sensors and sends it to another Raspberry Pi that we used as central server for all other Pis. 

This is our design schematic: 

![Design Schematic](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/DDID%20Final%20Project%20Prototype%20Schematic.png)


These are our paper prototype cases for the temperature sensors:

![Paper cases](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2827.jpg)


### Progress 

Unfortunately one of our temperature sensors broke in early tests, so we ran with just two. After the initial setup, we found that we can connect the temperature sensors directly to the Raspberry, which made it much easier to out into a box and distribute across the room. We also connected the ultrasonic sensors directly to a Pi and had all three Pis connected to a flask server that we established on one of our laptops. 

Getting the sensors connected to the Pis and send the signals to a server was relatively easy and worked fast. Getting the ultrasonic sensors to count correctly was a bit harder. We had to tried it various times and noticed that the signals of both sensors impacted each other, that is why we built a wooden board to put a larger distance between each of the sensors.


Alan building the board for the ultrasonic sensors:

![board](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2832.jpg)

We then had to create an algorithm to show our insights from our sensor measurements. Our initial plan was to calculate the optimal room temperature based on the number of people. However, after long research we came to the conclusion that this is not feasible with the information we had. We attempted to use Fanger's comfort equation, the basis for most HVAC systems, but to accurately estimate an optimal temperature point requires data on the room composition, materials, insulation levels that we did not have. Hence, we changed our algorithm to estimate the heat generated by humans and used this information to show how long it takes to heat up a room based on the number of people in the room. 


Ultrasonic print output in the console:

![Ultrasonic print](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2839.jpg)

As our last step, we printed small cases for our Raspberry Pis to fit in and put double-sided tape on the back of them. That way we could paste them onto the wall close to an outlet and put the temperature sensors about 2" above it, so they are not affected by the heat of the Pis.

Our 3D printed Pi cases:

!Pi case](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2815.jpg)


### Devices Used 

The devices that we used to contain our server, run our sensors, and output the data to a website are Raspberry Pi boards as well as an Arduino Uno during the testing phase. The sensors are a pair of DHT 22s and two ultrasonic distance sensors. The devices and where they can be obtained are shown below:

* 3 Raspberry Pi 3 Model B+ [Link to board](https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/)
* Arduino Uno Rev3 [Link to board](https://store.arduino.cc/usa/arduino-uno-rev3)
* 2 Adafruit DHT 22 Temperature and Humidity Sensors [Link to sensors](https://www.adafruit.com/product/393)
* 2 Adafruit Ultrasonic Distance Sensors [Link to sensors](https://www.adafruit.com/product/4007)

### Codes Used

[Sensor Information & Coding](https://github.com/ababushkin6/IDD-Fall19-FinalProject/tree/master/Sensors)

[Server Coding](https://github.com/ababushkin6/IDD-Fall19-FinalProject/tree/master/Server)


### Calculate body heat emission

For simplicity, our temperature algorithm on our server  assumes that the room is a closed body of air with perfect insulation. We calculate the temperature difference in Kelvin using the average temperature and the user's desired temperature input. Based on the room size, we calculate the volume and weight of the air in the room and using the specific heat for air, we estimate the required energy need to heat up the room to the desired temperature. Finally, we use the metabolic rate of the selected activity in the room and an average body surface for humans (1.75 square meters) to estimate the body heat production in W and multiply it by the number of people in the room. We adjust for temperature diffusion and calculate the time it takes to heat up the room in hours and mins.

Calculations are based on: [Cornell Unviersity Ergonomics Web](http://ergo.human.cornell.edu/studentdownloads/DEA3500notes/Thermal/thcondnotes.html)


### Key Learnings

* Determining optimal room temperature is a highly complex process impacted by various factors from personal preferences to materials used in the room
* Ultrasonic sensors work the determine people walking in and out, but require people to walk relatviely slow. PIR motion sensors might work better
* Humans emit a lot of heat (that can be used to heat up a room naturally)


### Final product

Here is a picture of our final products:

![Devices final](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/IMG_2825%202.jpg)

![Website](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2829.jpg)


Here's a video of the interaction:
[Video of the website](https://drive.google.com/open?id=1w4Owynh2kB8nk3H762CxsLngoVftQoUo)


Our product in action during our project fair: 

The ultrasonic sensor were mounted on a table near the entrance and the temperature sensors were mounted above a plug with large distance from each other.



![Ultrasonic](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2836.jpg)

![Temperature](https://github.com/ababushkin6/IDD-Fall19-FinalProject/blob/master/images/IMG_2837.jpg)
