# Project proposal

### Introduction:
To increase the knowledge and expertise within the evolving automotive industry Infotiv AB developed the Infotiv's Educational Autonomous Platform. The goal of this platform is to have a autonomous GO-Kart, be it in a controlled test environment, that furthers development and research in the autonomous vehicle industry.
The technical scope of this project will be ever-changing depending on the market need and introducing new technology within the automotive industry. It will include, but not limited to, development in areas such as: electrical hardware (PCB design, battery) and embedded systems, mechanical hardware, software and protocol design, sensing, perception and decision making using machine learning,  telematics and electromobility , app and UX design. 

### Current GoKart
Currently the system is designed in three modules, Automotive platform that implements the core driving functionality (steering, throttle and brake) through CAN bus . Body electronics which includes lights, sensors, horn and monitor displaying the platform power mode and a simulated key.
Finally Autonomous Drive module that runs the perception and sensing for decision making using AI/ML algorithms capable of Adaptive Cruise Control (ACC), Automated Lane Centering (ALC) and other basic driving assistant functionalities.

### Future plan
We are now in the point that we want to extend the functionalities and introduce the second generation of the autonomous platform capable of running cutting edge algorithms. This requires upgrading the electronic control units (ECU), improving the verification and validation of each units and a separate diagnostic module, Extending the machine learning based autonomous drive system with advanced new functionality such as Driver Awareness and Monitoring Systems (DMS), improving environment perception by road sign and traffic light detection system, path planning.

In parallel, Infotiv is interested in developing a digital twins of the Autonomous Platform inside a simulated environment for rapid testing Advanced Driver Assistance Systems (ADAS for short) components. This includes but limited to Brake Assist (BA) and Autonomous Emergency Braking (AEB) and for testing perception and decision making components in situations when the test may raises safety concerns. We are also intersted to explore the possible to train and test these ML models inside a simulator before exposing and training them in a real world.

Finally adding a secure telematic and infotainment system capable of remotely and continuously updating the software for each ECU, secure real time remote control of the vehicle and finally secure and reliable transmission of sensor data (e.g. Camera, LIDAR, …) to the back office.


### Conclusion and goals
The goal is to release and open the software code and HW design for this generation for public for self driving enthusiastic and as an educational platform for improving collaboration between academia and industry. This framework will be a valuable educational and safe environment for experiment using machine learning for autonomous drive experiments.

Performing development in a smaller scale models (GoKart) and using simulator and digital twins reduces the cost and time of design, implementation and verification of autonomous system and therefore  speeds up the time to market which benefits Infotiv and its customers.

