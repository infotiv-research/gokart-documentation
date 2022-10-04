### Issue List

- ❌ Wifi only connects to INFOTIV internal wifi AP
- ✅ Left & Right wheels are not synced: Possible Solution: Using the backup GoKart may possibly solve this.
- ✅ Not possible to turn the wheel to the Left: Found a working solution in the repository
- ✅ CAN message cannot be used to control the wheel/speed: Replaying the CAN can move the steering wheel.
- ❌ System beeping for no reason with Red flashing light

    1- Possible Solution: Use remote control (or ROS) to do propulsion operation (steering & speeed) and it changes the beeping patern and light color to orange

    2- Possible Solution: internal gyro notices that the device is tilted?

- ❌ The NVIDIA Jetson TX2 Developer Kit comes with 19v & 4.7A (90W max) power supply. However the external power & possible the battries cannot provide enough power and causes the Jetson to shutdown when wheel and steering are engaged. 
- ✅ Kill switch: Fixed in the code.
- ❌ Extra power supply & battery 
- ❌ Segway supports external batteries (BMS need to be studied throughly)
- ✅ OpenPilot POC
- ❌ OpenPilot 

	1- Delay

- ✅ Documentation

	1- ✅ PDF

	2- ✅ Webpage

- ✅ Thesis project to upgrade part, documentation, CI and machine learning
- ❌ pull request recent changes on VCU
- ❌ Disable and enable RC in VCU
- ❌ Find other areas for testing (preferebly with electricity and road line)
	
	1- AstaZero: Far away

	2- Other locations?

- ❌ Open source the project. 

	1- ✅ Document as an opensource project for VALU3S
	
	2- PCB boards & codes

	3- 3D models

- ❌ 3D print module for body electronics module
- ✅  Kill switch or RC
- ❌ Implement missing ROS APIs
- ❌ reenable RC steering, not sending neutral steering but just L&R  (see throttle for inspiration)
- ❌ Fix carla streering value range
- ❌ Make a command to stop wheel before killing the openpilot docker process
- ❌ Fix hostname (dobby.local) translation inside docker (pass hostname as an environemnt variable)
- ❌ Generic spec like: https://www.benderrobotics.com/breach.html


Patches for fixing the issue with remote control
```
void RcView::updateSpeedPulse() 
{
	speedData_ = RC_SPEED_INPUT.get();
	if(speedData_ == 1 && previousSpeedData_ != 1)
	{
		speedStartTime_ = get_system_time_ns();
	}
	else if(speedData_ == 0 && previousSpeedData_ == 1)
	{
		speedEndTime_ = get_system_time_ns();
        if(speedEndTime_ - speedStartTime_ > minSpeedPulse_ && speedEndTime_ - speedStartTime_ < maxSpeedPulse_) //Remove all misscalculations when timer overflows.
        {
            speedPulse_ = speedEndTime_ - speedStartTime_;
			float speedReq = linearConversion(speedPulse_, minSpeedPulse_, maxSpeedPulse_, 0, 1);

        	if (speedReq > 1) speedReq = 1;
        	else if (speedReq < 0) speedReq = 0;

        	if(speedReq > 0.55) //Acceleration signal
        	{
				speedReq = (speedReq - 0.55) / (0.45);
				gokartModel_->setSpeedRequest(speedReq);
        	}
			else if(speedReq < 0.45) //brake signal
			{
				float brake_req = (speedReq / 0.45); 
				gokartModel_->setBrakeRequest(brake_req);
			}
			else
			{
				gokartModel_->setSpeedRequest(0);
				gokartModel_->setBrakeRequest(0);
			}
			
        }
	}
	previousSpeedData_ = speedData_;
}

```


The left steering is not implemented correctly or NOT at all

1. gokart_controller / gokart_controller.py
```
     def set_power_enable(self):
        raise NotImplementedError

    def set_speed(self, speed):
        raise NotImplementedError

    def set_turn_rate(self, degrees):
        raise NotImplementedError
```

2. last commit on gokart/Gokart_VCU
```
src/controllers/GokartController.cpp  

- #define minTurnPWM_ 0.069
- #define maxTurnPWM_ 0.051
+ #define minTurnPWM_ 0.074
+ #define maxTurnPWM_ 0.047

src/views/RcView.h 

-  static const int minTurnPulse_ = 1130000;
-  static const int maxTurnPulse_ = 1930000;
+  static const int minTurnPulse_ = 1050000;
+  static const int maxTurnPulse_ = 1850000;
```
To check `GoKartController.cpp`:

```
/**
 * Sets the vehicle speed. 
 * 
 * Motor want analog signals between 0,8v and 4,2v
 * 
 * Output pwm-signal between 0,24(4,2v analog) and 1(0,8v analog)(voltage inverted because of low pass filter) on pin A1
 *
 * @param speed_req Value between 0 and 1
 */
void GokartController::setSpeed(float speedReq)
{
    float speedPulse = linearConversion(speedReq, 0, 1, 1, 0.24); //speed_req * (0.24 - 1) + 1;
    TIM_pulse.set_pwm_duty(2, speedPulse); 
    TIM_pulse.set_pwm_duty(3, 0.75);
    
    gokartModel_->setWheelTorque(speedPulse);

}
```