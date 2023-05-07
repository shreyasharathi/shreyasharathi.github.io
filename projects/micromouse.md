---
layout: project
type: project
image: img/micromouse/micromouse-square.jpg
title: "Auto Irrigation System "
date: 2021
published: true
labels:
  - Embedded Systems
  - Arduino
  - C++
summary: "My team designed and developed a system to eliminate the need to perform the redundant task of controlling the motor irrigation system.."
---

<div class="text-center p-4">
  <img width="200px" src="../img/micromouse/micromouse-robot.png" class="img-thumbnail" >
  <img width="200px" src="../img/micromouse/micromouse-robot-2.jpg" class="img-thumbnail" >
</div>

For this project, I was the lead programmer who was responsible for programming the various capabilities of the **timer based auto irrigation system**.  I started by programming the basics, such as sensor polling and motor actuation using interrupts. I also designed and tested the PCB for the embedded system. The components used were Arduino Mega, DC motor, Relays, I2C, Keypad Matrix and a GSM module.

- This system is particularly useful when it is inaccessible at night, when the situation poses a risk to the person due to low visibility in the farmlands, insects/wild animals, and other factors. 
- The system allows the user to run the motor or any other appliance without manual supervision, without any difficulties. 
- GSM was used to allow remote access to the system that improves the overall accessibility.

We have deployed this sytem in 22 farms across Thanjavur, India.


Here is some code that illustrates how we read values from the line sensors:

```cpp
byte ADCRead(byte ch)
{
    word value;
    ADC1SC1 = ch;
    while (ADC1SC1_COCO != 1)
    {   // wait until ADC conversion is completed   
    }
    return ADC1RL;  // lower 8-bit value out of 10-bit data from the ADC
}
```
