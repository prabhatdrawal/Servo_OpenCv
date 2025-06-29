# Servo_OpenCv
Here's a ready-to-use theory section you can include in a GitHub README or documentation file for a project titled something like **"Controlling Servo Motor Using OpenCV and Python"**:

---

##  Theory: Controlling a Servo Motor Using OpenCV and Python

Controlling a servo motor using OpenCV and Python involves combining computer vision with physical actuation. The goal is to use visual data (typically from a webcam or video stream) to control the position of a servo motor based on certain visual cues, such as object position or face tracking. This forms the basis of many real-world applications such as automated tracking systems, face-following cameras, and robotic arms.

###  What is a Servo Motor?

A **servo motor** is a type of actuator that allows precise control of angular or linear position, velocity, and acceleration. It operates on Pulse Width Modulation (PWM) signals:

* A typical servo expects a pulse every 20 ms.
* The width of the pulse (usually between 0.5 ms to 2.5 ms) determines the angle (e.g., 0° to 180°).

### Purpose

The main objective is to use visual information—captured and processed using **OpenCV**—to determine how a servo should move. For example, if tracking a face or an object, the servo can rotate the camera so the object remains centered in the frame.

###  Role of OpenCV

**OpenCV** (Open Source Computer Vision Library) is used to:

* Capture live video frames using a webcam.
* Detect and track features like color, shapes, or faces.
* Extract the x-coordinate (or y-coordinate) of the tracked object in the frame.
* Map that coordinate to a corresponding angle for the servo.

###  Mapping Coordinates to Angles

Once the position of an object is detected in a video frame (say x in a 640x480 frame), we map that coordinate to a servo angle:

```python
def map_range(value, left_min, left_max, right_min, right_max):
    # Maps value from one range to another
    left_span = left_max - left_min
    right_span = right_max - right_min
    value_scaled = float(value - left_min) / float(left_span)
    return right_min + (value_scaled * right_span)
```

This allows us to convert a horizontal position (e.g., 0–640 pixels) into a servo angle (e.g., 0–180 degrees).

###  Controlling the Servo with Python

To control the servo, we typically use:

* **Raspberry Pi GPIO PWM** (for hardware PWM control).
* **PySerial** (if the servo is controlled via Arduino).
* **RPi.GPIO** or **gpiozero** (for Raspberry Pi).

Example using `gpiozero` on Raspberry Pi:

```python
from gpiozero import AngularServo
servo = AngularServo(17, min_angle=0, max_angle=180)
servo.angle = 90  # Set to midpoint
```

Or if using **Arduino via Serial**:

```python
import serial
arduino = serial.Serial('COM3', 9600)
angle = 90
arduino.write(f'{angle}\n'.encode())
```

###  Applications

* Face or object tracking turrets
* Vision-guided robotic arms
* Autonomous camera systems
* Real-time gesture-controlled devices

---

Let me know if you'd like the complete README template, with setup instructions, hardware requirements, or a code example.
