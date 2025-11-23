# Robot Movements Report
---
## Robot Configuration
The robot is driven by four DC motors arranged in a mecanum-wheel configuration, allowing omnidirectional movement. 

Each motor is controlled by two pins: a PWM pin to set the speed (values between 0-255) and a DIR pin to set the rotation direction. 

Additionally, each motor has a boolean variable indicating whether a logical HIGH or LOW corresponds to forward rotation.
