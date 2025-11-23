# Robot Movements Report
---
## Robot Configuration
The robot is driven by four `DC` motors arranged in a mecanum-wheel configuration, allowing omnidirectional movement. 

Each motor is controlled by two pins: 
- `PWM` pin to set the speed (values between 0-255)
- `DIR` pin to set the rotation direction. 

Additionally, each motor has a boolean variable indicating whether a logical `HIGH` or `LOW` corresponds to forward rotation.

Pin mapping and polarity configuration for each motor:

| Motor              | PWM Pin | DIR Pin | Forward Polarity |
|:------------------:|:-------:|:-------:|:-----------------:|
| Front Left (FL)    |    6    |    5    |       false       |
| Front Right (FR)   |   11    |   12    |       true        |
| Back Left (BL)     |   A4    |   A5    |       false       |
| Back Right (BR)    |    9    |   10    |       true        |

A helper function is used to set each motor:
```cpp
void setMotor(int pwm, int dir, int speed, bool forward) {
  digitalWrite(dir, forward ? HIGH : LOW);
  analogWrite(pwm, speed);
}
```
The global variable `motorSpeed` determines the `PWM` duty cycle (default 80). 

Movements are implemented by applying appropriate direction patterns to each motor.

---
## Vertical Movements
Vertical movements correspond to forward (north) and backward (south) directions of the robot.

These movements involve all four mecanum wheels moving in the same direction.
### North (Forward)
To move the robot north, all four wheels rotate forward.

This movement sets the `movingNorth` flag to `true` for logic tracking, and then calls `setMotor` for each wheel.
```cpp
void moveNorth() {
  movingNorth = true;
  FL_speed = motorSpeed;
  FR_speed = motorSpeed;
  BL_speed = motorSpeed;
  BR_speed = motorSpeed;
  setMotor(FL_PWM, FL_DIR, motorSpeed,  FL_fw);
  setMotor(FR_PWM, FR_DIR, motorSpeed,  FR_fw);
  setMotor(BL_PWM, BL_DIR, motorSpeed,  BL_fw);
  setMotor(BR_PWM, BR_DIR, motorSpeed,  BR_fw);
}
```

### South (Backward)
To move the robot south, all four wheels rotate backward.
```cpp
void moveSouth() {
  FL_speed = -motorSpeed;
  FR_speed = -motorSpeed;
  BL_speed = -motorSpeed;
  BR_speed = -motorSpeed;
  setMotor(FL_PWM, FL_DIR, motorSpeed, !FL_fw);
  setMotor(FR_PWM, FR_DIR, motorSpeed, !FR_fw);
  setMotor(BL_PWM, BL_DIR, motorSpeed, !BL_fw);
  setMotor(BR_PWM, BR_DIR, motorSpeed, !BR_fw);
}
```
