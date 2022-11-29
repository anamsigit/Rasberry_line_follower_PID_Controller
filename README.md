# Rasberry_line_follower_PID_Controller
an line follower robot from rasberry, camera, 2 motor, motor driver ln298, ESP32 and externall battery with PID Controller adjuster computate

# How it work : general
rasberry receives a frame from the camera, then with the python program the frame is processed to detect the color of the black color set, from the black color you are looking for then the code will determine the midpoint.

The resulting center point is recorded for its x coordinate, then processed by the PID to provide a more optimal movement

the PID value is then mapped so that it can provide a value ranging from 80 to -80 (meaning when the value is 0, the robot goes straight)

the mapping results are then sent to the esp32 microcontroller and entered in a variable to set the speed of the two tires

# how it work : rasberry
the cx variable plays an important role in controlling the movement of the robot's turns

when it detects the black path, then cx will look for the midpoint followed by the PID, but when it does not detect the black path, I put cx in the middle it means the coordinate value is the length of the screen(frame.shape[1]) divided by two and in the end it will also be followed by PID to optimize its movement

# how it work : esp32
the microcontroller receives data from only one sourve, my purpose is to separate the values based on positive and negative signs(from python), when the number is positive, the reduced speed is the right wheel, and when the received sign is negative, the reduced wheel speed is the right wheel The difference in torque on one of the wheels will cause the robot to turn right or left
