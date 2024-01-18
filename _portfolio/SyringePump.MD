---
title: "Syringe Pump Project: Linear Actuator"
excerpt: "This programmable syringe pump can operate two syringe pump sizes at any input flow rate."
header:
  image: /assets/img/SyringePumpFinalRendering .png
  teaser: /assets/img/RealSPImage.png
gallery:
  - image_path: <img src="/assets/img/RealSPImage.png" width="400" alt="Final Rendering"> 
  - image_path: <img src="/assets/img/SyringePumpWiringDiagram.png" width="400" alt="Wiring Diagram"> 
  - image: <img src="/assets/img/ElectronicsENclosureSP.png" width="400" alt="Electronics Enclosure"> 
---

# Details

* **About This Project** \ 
Syringe pumps are motor-driven precision pumps that deliver precise amounts of fluid, typically in medical environments. They operate using a motor to drive a plate forward, pushing a syringe plunger and expelling the fluid at a specified rate. While commercial syringe pumps can be quite expensive, this prototyped design offers a cost-effective alternative, requiring about $200 in materials. This fully programmable syringe pump design allows for the usage of two different syringe barrel sizes and includes features such as a forward/back and adjustable knob for controlling the fluid flow rate. This syringe pump is capable of 1 µL/min to 10 mL/min.

* **User Operation Instructions** \ 
To operate the syringe pump at a given flow rate, first, input the syringe size and desired flow rate into the Arduino code. Upload the code to the Arduino, then plug the syringe pump into the wall outlet. Ensure the lid of the enclosure is properly secured down, and the syringe is placed properly in the pump. If slight adjustments to the carriage position need to be made, do so with the forward and reverse buttons on the control panel. Once the user is ready to dispense, click the start/stop button once, and the syringe pump will begin operating at your desired flow rate. The LED will turn green when in motion. To slow the constant flow rate of the syringe pump, turn the potentiometer knob counterclockwise. When the user has dispensed the desired amount of fluid, press the start/stop button again to pause the motion of the carriage; the LED should turn yellow when paused. If the pump is allowed to dispense the total volume of the syringe, the pump will automatically stop operating, and the LED will turn red. Use the forward and reverse buttons to readjust your carriage to the desired position, then unplug when finished operating.

## CAD Model \


## Arduino Code \
Here is a link to the [Arduino code](/SyringePumpArduinoCodeGithub.ino) to operate.

# Table 1 
* **Parts Required** \

|Header 1|Header 2|
|--------|--------|
|Content 1|Content 2|

# Table 2 
* **3D Printed Parts Required** \

|Header 1|Header 2|
|--------|--------|
|Content 1|Content 2|

{% include gallery caption="Rendition & Wiring Diagram of the Syringe Pump" %}
