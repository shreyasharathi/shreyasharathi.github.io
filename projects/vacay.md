---
layout: project
type: project
image: img/vacay/paper1.jpg  
title: "Embedded System Based Solution for Ailment of Irrigation in Agriculture"
date: 2021
published: true
labels:
  - Embedded Systems
  - Smart Agriculture
  - Irrigation
  - Automation
summary: "Published in: 2021 Innovations in Power and Advanced Computing Technologies (i-PACT)"
---

<div class="text-center p-4">
  <img width="200px" src="../img/vacay/paper1.jpg" class="img-thumbnail" >
  <img width="200px" src="../img/vacay/paper2.jpg" class="img-thumbnail" >
  <img width="200px" src="../img/vacay/paper3.png" class="img-thumbnail" >
</div>

Smart agriculture using embedded system-based automated irrigation management is the most prominent approach and will be pivotal in revolutionizing the agricultural domain. The excess as well as inadequate irrigation damages the crops and inflicts great loss to the farmers. This paper proposes a small-scaled embedded system for the application of an irrigation system to provide a sustainable environment for the crops by implementing automation.
<h3>Specifications</h3>
<ul>
  <li> Arduino Uno and ESP-01 </li>
  <li> Soil Moisture Sensor Array  </li>
  <li> Relay driven motor </li>
  <li> MQTT Server (ThingSpeak) </li>
</ul>

<h3> Algorithm-Process Flow </h3>
Step 1: Input
- The sensor array unit senses the conductivity and sends the same in analog format to the sensor interface. <br>

Step 2: Forwarding the input
- The interface uses a comparator to get the digital equivalent of the obtained analog data.<br>
- The digital data is sent to the processing unit.<br>

Step 3: Comparison and decision making
- The processing unit or control unit uses the received data and produces the average moisture level in the soil. <br>
- The average value is compared with the threshold value, thus deciding if the available moisture is sufficient. <br>
- If insufficient, then a signal is passed to the relay to drive the pump till the water content rises above the set threshold.<br>

Step 4: Output
- The output panel, in this case, the Arduino IDE serial monitor, displays the status of each sensor in the array as well as the motor in real-time. <br>
- This allows for overall supervision of the system when needed and also the overall  performance  of the system over a time period.<br>
- From ThingSpeak, the IFTTT API send an email notification to the user in case the water level is below/above the set threshold.<br>

Co-Authored with : Kaushik Lakshmiramanan, Ramya Vijay, Nithya Chidambaram.

Published in: 2021 Innovations in Power and Advanced Computing Technologies (i-PACT). 

Refer : <a href = "https://ieeexplore.ieee.org/document/9696512"> ieeexplore.ieee.org/document/9696512 </a>
