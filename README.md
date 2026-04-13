# 💡 Smart Light Control System

![Arduino](https://img.shields.io/badge/Arduino-Uno-teal)
![Tinkercad](https://img.shields.io/badge/Tinkercad-Circuit%20Simulation-blue)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> Arduino-based smart lighting system that automatically controls an LED based on room occupancy (PIR sensor) and ambient light levels (LDR). The light only activates when both conditions are met — someone is present AND sunlight is insufficient.

---

## ⚙️ How It Works

| PIR (Occupancy) | LDR (Sunlight) | LED |
|-----------------|---------------|-----|
| No person | Any | OFF |
| Person detected | High sunlight | OFF |
| Person detected | Low sunlight | ON ✅ |

Both conditions must be true simultaneously for the LED to activate — avoiding unnecessary energy use.

---

## 🔄 Flowchart

![image](https://github.com/user-attachments/assets/15faec6b-2d6a-4541-a287-b0559c2e9e87)

**Case 1 — Occupancy check:** PIR sensor detects whether a person is present. If no one is detected, the system stops and the LED stays off.

**Case 2 — Light level check:** If a person is detected, the LDR measures ambient sunlight. If sunlight is sufficient, the LED stays off. If sunlight is low, the LED turns on.

---

## 🔌 Circuit Diagram

![image](https://github.com/user-attachments/assets/b88c2b80-daad-4577-86b8-11f9d4ce3310)

**Components:**
- PIR Sensor — occupancy detection (Digital Pin 2)
- LDR — ambient light measurement (Analog Pin A0)
- Arduino Uno — control logic
- Resistor — current limiting
- LED — output indicator (Digital Pin 13)

---

## 💻 Arduino Code

```cpp
int buttonState = 0;
int value = 0;

void setup() {
  pinMode(2, INPUT);   // PIR sensor
  pinMode(13, OUTPUT); // LED
  pinMode(A0, INPUT);  // LDR
}

void loop() {
  value = analogRead(A0);        // Read LDR value
  buttonState = digitalRead(2);  // Read PIR state

  if (buttonState == HIGH) {     // Person detected
    if (value < 10) {            // Low sunlight
      digitalWrite(13, HIGH);
      Serial.println("Light ON");
    } else {                     // Sufficient sunlight
      digitalWrite(13, LOW);
      Serial.println("Light OFF");
    }
    Serial.println(value);
  } else {                       // No person detected
    digitalWrite(13, LOW);
  }

  delay(2);
}
```

---

## 🎬 Simulation

https://github.com/user-attachments/assets/2dcc9120-6c94-4cc0-8125-f32590869159

---

## 📊 Key Outcomes

- Dual-condition logic ensures the LED only activates when genuinely needed, reducing unnecessary power consumption
- PIR and LDR sensors work in series — both must trigger for the light to turn on
- LDR threshold (`value < 10`) can be tuned to suit different room brightness levels
- Simulation validated correct behaviour across all three switching states

---

## 👤 About

**Moses Rubaraj** — BEng Mechatronics | MSc Robotics & Automation, University of Salford

[![GitHub](https://img.shields.io/badge/GitHub-mosesrubaraj-black?logo=github)](https://github.com/mosesrubaraj)
