# Omnidirectional Vehicle: Design, Implementation, and Application

---

## 1. Project Description

This project documents the **design**, **construction**, and **implementation** of a **Bluetooth-controlled omnidirectional vehicle**.  
The vehicle utilizes **four mecanum wheels**, which allow for exceptional maneuverability, including **forward**, **backward**, **lateral (sideways)**, **diagonal**, and **rotational** movements on a flat surface.

The core of the vehicle is an **Arduino Uno** microcontroller, which processes commands received wirelessly from a **smartphone** via an **HC-05 Bluetooth module**.  
An **L293D Motor Driver Shield** is used to control the four DC geared motors, each connected to a mecanum wheel.  
The system is powered by a **12V battery pack**, making it a **self-contained** and **versatile mobile robotics platform**.

This project serves as a practical demonstration of **omnidirectional kinematics**, **embedded systems programming**, and **wireless communication**.  
It's an excellent platform for **educational purposes** and a solid foundation for more advanced robotics applications like **autonomous navigation** and **Automated Guided Vehicles (AGVs)**.

---

## 2. Features

- **Holonomic Movement:** Capable of moving in any direction without changing orientation.

**Full Range of Motion:**

- Forward / Backward
- Left / Right (Lateral)
- Diagonal (Forward-Left, Forward-Right, Backward-Left, Backward-Right)
- In-place Rotation (Clockwise and Counter-Clockwise)

- **Wireless Control:** Operated remotely using a standard smartphone via a Bluetooth terminal app.
- **Modular Design:** Built with common, off-the-shelf components, making it easy to replicate, modify, and expand.

---

## 3. Components & Cost Analysis

The following table details the components used for this project and their respective costs.

| Component                     | Quantity | Cost (INR) |
|-------------------------------|----------|------------|
| Mecanum Wheels                | 4        | ₹ 725      |
| Coupling                      | 4        | ₹ 825      |
| Cardboard (for Chassis)       | 1        | ₹ 70       |
| Zip Ties                      | Multiple | ₹ 50       |
| TTM BO Motor                  | 4        | ₹ 200      |
| L293D Motor Driver/Servo Shield | 1      | ₹ 110      |
| Arduino Uno R3                | 1        | ₹ 650      |
| Jumper Wires                  | Multiple | ₹ 140      |
| 3.7V Li-ion Batteries         | 3        | ₹ 190      |
| 3-Cell Battery Holder         | 1        | ₹ 40       |
| HC-05 6-pin Bluetooth Module  | 1        | ₹ 230      |
| DC Power Switch               | 1        | ₹ 10       |
| **Total Cost**                |          | **₹ 3240** |

---

## 4. Technical Details

### Communication Protocol

- **Bluetooth SPP:** The vehicle is controlled via an **HC-05 Bluetooth module** configured to use the **Serial Port Profile (SPP)**.  
  This allows it to act as a wireless serial bridge between the controlling device (**smartphone**) and the **Arduino**.

- **UART Interface:** The **HC-05 module** communicates with the **Arduino Uno** using a software serial interface on **digital pins 10 (RX)** and **9 (TX)** at a baud rate of **9600 bps**.

- **Command Structure:** Control is achieved by sending single-character commands from a Bluetooth terminal app on a smartphone.  
  The Arduino code continuously listens for these characters and executes the corresponding movement function.  
  For example:
  - `F`: Move Forward
  - `B`: Move Backward
  - `L`: Move Left (Lateral)
  - `R`: Move Right (Lateral)
  - `X`: Toggle Rotation Mode On/Off

---

### Power Management & Battery System

- **Power Source:** The system is powered by three **3.7V Li-ion batteries** connected in series within a battery holder, providing a nominal voltage of **11.1V** (approximately **12V**).

- **Power Distribution:** The battery pack is connected directly to the power input terminal of the **L293D Motor Driver Shield**.  
  The shield handles power distribution, providing regulated **5V** power to the **Arduino Uno** and the **HC-05 module**, while supplying the higher voltage directly to the DC motors.  
  This isolates the sensitive logic circuits from the noisy motor power supply.

- **Control:** A physical **DC power switch** is integrated between the battery pack and the motor shield, allowing the entire system to be easily powered on or off.

---

## 5. Vehicle Dynamics

- **Vehicle Weight:** 612 g
- **Wheel Dimension:** Diameter = 80 mm, Width = 37 mm
- **Limiting Angle of Friction (Mecanum Wheel & Plastic):** 27°
- **Wheelbase:** 115 mm
- **Chassis Dimensions:** Width = 215 mm, Length = 285 mm
- **Corner Radius:** 40 mm
- **Ground Clearance:** 50 mm
- **Maximum Rotational Speed:** 3.18 rad/s
- **Maximum Speed:** 0.681 m/s


### Motor Control & Kinematics

- **Mecanum Wheel Principle:** The vehicle's omnidirectional capability comes from the four mecanum wheels.  
  Each wheel has rollers mounted at a **45° angle** to its axis. By controlling the direction and speed of each wheel independently, the forces generated can be combined to produce movement in any direction.

- **L293D Motor Shield:** The **Adafruit L293D shield** contains two L293D H-Bridge ICs, allowing it to control the direction and speed of up to four DC motors independently.

- **Speed Control:** Motor speed is managed using **Pulse Width Modulation (PWM)** signals generated by the Arduino.  
  In this implementation, the motors are run at maximum speed (`setSpeed(255)`) for simplicity.

- **Kinematic Control:** The Arduino code implements the logic for omnidirectional movement by activating the motors in specific combinations.  
  For example, to move laterally to the right, the front-right and rear-left motors spin **backward**, while the front-left and rear-right motors spin **forward**.

---

## 6. How to Use

1. Assemble the vehicle according to the **mechanical and electronic configuration diagrams**.
2. Upload the provided **Arduino code** to the Arduino Uno board.
3. Power On the vehicle using the **DC power switch**. The status LED on the **HC-05 module** should start blinking.
4. **Pair Your Smartphone:**
   - Open your smartphone's Bluetooth settings and search for a new device.
   - Connect to the **HC-05 module** (often named *HC-05*).
   - Use the pairing code **"1234"** if prompted. The LED on the module should become solid.
5. **Control the Vehicle:**
   - Open a **Bluetooth serial terminal app** on your smartphone (e.g., *Serial Bluetooth Terminal* on Android).
   - Connect to the paired **HC-05 device** within the app.
   - Use the on-screen buttons to send commands to control the vehicle's movement.

---
