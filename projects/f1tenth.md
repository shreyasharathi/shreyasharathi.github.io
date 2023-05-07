---
layout: project
type: project
image: img/micromouse/timer2.png
title: " Wall Following for F1TENTH Autonomous Race Car"
date: 2023
published: true
labels:
  - Embedded Systems
  - Nvdia Jetson
  - ROS
summary: "AS the titile suggests, my team and I implemented Wall Following System for F1TENTH Race Car"
---
<ul>
<li> The wall follow node implements a simple PID controller for the car to autonomously drive forward while staying centered. </li>
<li> In the context of our car, the desired distance to the wall should be our set point for our controller, which means our error is the difference between the desired and actual distance to the wall. </li>
<li> Obtain two laser scans, 'a' and 'b' </li>
<li> Use the distances 'a' and 'b' to calculate the angle 'alpha'. 'Alpha' is the difference in inclination between the front wheels and back wheels. </li>
<li> Use 'alpha' to find the current distance to the car, and then and to find the estimated future distance to the wall. </li>
<li> Run through the PID algorithm described above to get a steering angle. </li>
<ul>
<li> If the steering angle is between 0 degrees and 10 degrees, the car should drive at 1.5 meters per second. </li>
<li> If the steering angle is between 10 degrees and 20 degrees, the speed should be 1.0 meters per second. </li>
<li> Otherwise, the speed should be 0.5 meters per second. </li>
</ul>
</ul>




