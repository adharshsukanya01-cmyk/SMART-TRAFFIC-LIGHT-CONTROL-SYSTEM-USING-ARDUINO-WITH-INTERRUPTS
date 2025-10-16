# DEVARAJAN.N(212223060044)
# **SMART TRAFFIC LIGHT CONTROL SYSTEM USING ARDUINO WITH INTERRUPTS**

## Tinkercad IMAGE:
![WhatsApp Image 2025-10-16 at 12 55 28_24421ecd](https://github.com/user-attachments/assets/d89244cc-25e0-4527-9a8c-fcc0fb68da36)



## **Objective of the Project**  
The objective of the Smart Traffic Light Control System is to manage traffic flow efficiently at a four-way intersection using Arduino, while allowing emergency vehicles to override normal signal cycles through interrupts. The system provides a realistic traffic control model using LEDs and push buttons, simulating traffic light operations and emergency responses.

---

## **Components Used**  
- **Arduino UNO** – Acts as the main controller for traffic light operation.  
- **LEDs (Red, Yellow, Green)** – Represent traffic lights for four different directions.  
- **Resistors** – Protect LEDs from high current.  
- **Push Buttons** – Used to trigger interrupts, simulating emergency vehicle arrival.  
- **Jumper Wires** – For connections between Arduino and breadboards.  
- **Breadboards** – For easy wiring of LEDs and buttons.

---

## **Working Principle**  
The system uses 12 LEDs arranged in four sets (each with red, yellow, and green) to simulate traffic lights at a four-way intersection. Normally, the lights cycle through each direction in sequence using the Arduino, turning on the green light for 5 seconds, then yellow for 3 seconds before moving to the next direction.

Two push buttons are connected to Arduino’s interrupt pins (2 and 3). When an emergency is simulated by pressing a button, an **Interrupt Service Routine (ISR)** is triggered. This ISR immediately changes the light sequence to prioritize the emergency route (e.g., green lights for certain directions), temporarily overriding the normal traffic cycle.

The system resumes normal operation after the emergency state is handled, ensuring both regular and emergency traffic are managed smoothly.

---

## **IoT Application and Benefits**  
Integrating this system with IoT platforms allows real-time traffic monitoring, remote signal control, and dynamic adjustments based on traffic density or emergency events. Authorities can monitor intersections, trigger overrides remotely, and analyze traffic flow data to improve urban mobility. This leads to:

- Faster emergency response times  
- Reduced congestion  
- Improved traffic management efficiency  
- Enhanced public safety

---

## **Block Diagram**  

![WhatsApp Image 2025-10-16 at 12 55 30_819f0956](https://github.com/user-attachments/assets/96033dfe-fc8c-46d0-852b-df89dd016c23)

### **Description of Main Blocks**  
- **Push Buttons (Pin 2 & 3):** Trigger interrupts when pressed, simulating emergency signals.  
- **Arduino UNO:** Core controller that runs normal traffic cycles and responds to interrupts.  
- **Traffic Lights 1–4:** Each has Red, Yellow, and Green LEDs connected to digital pins (0–13).  
- **ISR (Interrupt Service Routine):** Overrides normal traffic cycle during emergencies.  
- **Main Loop:** Handles regular traffic light sequencing in a timed manner.

---

## **Program**

```cpp
int red1 = 0;
int yellow1 = 1;
int green1 = 4;
int red2 = 5;
int yellow2 = 6;
int green2 = 7;
int red3 = 8;
int yellow3 = 9;
int green3 = 10;
int red4 = 11;
int yellow4 = 12;
int green4 = 13;

const byte interruptPin1 = 2;
const byte interruptPin2 = 3;

volatile bool state = false;

void setup() {
  pinMode(interruptPin1, INPUT_PULLUP);
  pinMode(interruptPin2, INPUT_PULLUP);

  attachInterrupt(digitalPinToInterrupt(interruptPin1), ISR_changeTrafficLight, CHANGE);
  attachInterrupt(digitalPinToInterrupt(interruptPin2), ISR_changeTrafficLight, CHANGE);

  pinMode(red1, OUTPUT);
  pinMode(yellow1, OUTPUT);
  pinMode(green1, OUTPUT);
  pinMode(red2, OUTPUT);
  pinMode(yellow2, OUTPUT);
  pinMode(green2, OUTPUT);
  pinMode(red3, OUTPUT);
  pinMode(yellow3, OUTPUT);
  pinMode(green3, OUTPUT);
  pinMode(red4, OUTPUT);
  pinMode(yellow4, OUTPUT);
  pinMode(green4, OUTPUT);
}

void loop() {
  if (!state) {
    direction(red1, yellow1, green1, red2, yellow2, green2, red3, yellow3, green3, red4, yellow4, green4);
    direction(red2, yellow2, green2, red1, yellow1, green1, red3, yellow3, green3, red4, yellow4, green4);
    direction(red3, yellow3, green3, red1, yellow1, green1, red2, yellow2, green2, red4, yellow4, green4);
    direction(red4, yellow4, green4, red1, yellow1, green1, red2, yellow2, green2, red3, yellow3, green3);
  }
}

void direction(int a, int b, int c, int d, int e, int f, int g, int h, int i, int j, int k, int l) {
  digitalWrite(a, LOW);
  digitalWrite(b, LOW);
  digitalWrite(c, HIGH);

  digitalWrite(d, HIGH);
  digitalWrite(e, LOW);
  digitalWrite(f, LOW);

  digitalWrite(g, HIGH);
  digitalWrite(h, LOW);
  digitalWrite(i, LOW);

  digitalWrite(j, HIGH);
  digitalWrite(k, LOW);
  digitalWrite(l, LOW);

  delay(5000);

  digitalWrite(c, LOW);
  digitalWrite(b, HIGH);
  delay(3000);
}

void ISR_changeTrafficLight() {
  state = true;

  digitalWrite(red1, LOW);
  digitalWrite(yellow1, LOW);
  digitalWrite(green1, HIGH);

  digitalWrite(red2, HIGH);
  digitalWrite(yellow2, LOW);
  digitalWrite(green2, LOW);

  digitalWrite(red3, LOW);
  digitalWrite(yellow3, LOW);
  digitalWrite(green3, HIGH);

  digitalWrite(red4, LOW);
  digitalWrite(yellow4, LOW);
  digitalWrite(green4, HIGH);
}
```
## Output

The system runs a regular traffic signal cycle. When either push button is pressed, the interrupt is triggered, and the emergency route lights turn green immediately. Once the emergency is cleared, the system returns to the normal cycle.
