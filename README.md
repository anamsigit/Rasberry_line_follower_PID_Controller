# Rasberry_line_follower_PID_Controller
an line follower robot from rasberry, camera, 2 motor, motor driver L298N , ESP32 and externall battery with PID Controller adjuster computate

# How it work: general
rasberry receives a frame from the camera, then with the python program the frame is processed to detect the color of the black color set, from the black color you are looking for then the code will determine the midpoint.

The resulting center point is recorded for its x coordinate, then processed by the PID to provide a more optimal movement. the PID value is then mapped so that it can provide a value ranging from 80 to -80 (meaning when the value is 0, the robot goes straight). the mapping results are then sent to the esp32 microcontroller and entered in a variable to set the speed of the two tires

The green line indicates PID output then the yellow line indicates camera detection of the black line location actually. As a result, PID Controler prevents robot from making unnecessary turns due to black line detection errors.

<img width="350" height="350" src="https://github.com/anamsigit/Rasberry_line_follower_PID_Controller/blob/main/black-straigh-line.jpeg">
<img width="350" height="350" src="https://github.com/anamsigit/Rasberry_line_follower_PID_Controller/blob/main/detect-on_black-straigh-line.png">

# how it work: rasberry
the cx variable plays an important role in controlling the movement of the robot's turns

when it detects the black path, then cx will look for the midpoint followed by the PID, but when it does not detect the black path, I put cx in the middle it means the coordinate value is the length of the screen(frame.shape[1]) divided by two and in the end it will also be followed by PID to optimize its movement

# how it work: esp32
the microcontroller receives data from only one sourve, my purpose is to separate the values based on positive and negative signs(from python), when the number is positive, the reduced speed is the right wheel, and when the received sign is negative, the reduced wheel speed is the right wheel The difference in torque on one of the wheels will cause the robot to turn right or left

Attention:
before you can run esp32 code, you need to install the library provided by robojax here : http://robojax.com/learn/arduino/robojax_ESP-L298N-DC-Motor_library.zip. I thank and appreciate robojax for the code

calibration PID, you can visit this amazing website: https://www.rentanadviser.com/pid-fuzzy-logic/pid-fuzzy-logic.aspx

video demo: https://youtu.be/Nl7agIYDsWA
