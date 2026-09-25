# ESP32 Matrix OS (5x9 LED Matrix & Web Server)

A custom-built, interactive **5x9 LED Matrix** powered by an **ESP32** and driven by a hybrid hardware multiplexing engine. This project features a self-hosted **Wi-Fi Web Server** and a full-stack dashboard ("Matrix OS") that lets you control scrolling text, sync a browser-based clock, play Snake via an on-screen D-pad joystick, and trigger fluid pixel art animations straight from your smartphone—**no internet connection or external router required!**

---

## 🌟 Features

* **Hybrid Multiplexing Architecture:** Bypasses standard 8-bit shift register limits by using a single `74HC595` for the first 8 columns and a direct ESP32 GPIO pin for the 9th column.
* **Matrix OS Web Dashboard:** Hosts a mobile-responsive HTML/JavaScript interface directly from the ESP32's internal flash memory.
* **Scrolling Text Engine:** Custom 3x5 font with a massive memory buffer, real-time speed slider, and smooth looping.
* **Browser-Synced Software RTC:** Automatically syncs precise local time from your smartphone browser, running independently on an internal software clock even if disconnected.
* **Dynamic Animations:** Flipbook-style pixel art engine featuring organic timing for a Beating Heart and Blinking Face.
* **Wireless Snake Game:** Fully playable retro Snake game controlled wirelessly through an intuitive on-screen D-pad joystick.

---

## 🛠️ Bill of Materials (Hardware)

* **1x** ESP32 Microcontroller Board
* **45x** LEDs (Standard 3mm or 5mm)
* **1x** 74HC595 Shift Register IC
* **5x** BC547 NPN Transistors (Collector-Base-Emitter / C-B-E pinout)
* **9x** 220Ω Resistors (For LED columns)
* **5x** 1kΩ Resistors (For transistor bases)
* Breadboards and jumper wires

---

## ⚡ Circuit & Wiring Guide

### 1. The Matrix Grid Construction
* **Columns (1 to 9):** Solder all **Positive (Anode / Long)** legs together vertically. You will have 9 column wires.
* **Rows (1 to 5):** Solder all **Negative (Cathode / Short)** legs together horizontally. You will have 5 row wires.

### 2. Shift Register (74HC595) to ESP32
* **Pin 16 (VCC) & Pin 10 (MR)** ➔ ESP32 `3.3V`
* **Pin 8 (GND) & Pin 13 (OE)** ➔ ESP32 `GND`
* **Pin 14 (SER / Data)** ➔ ESP32 `GPIO 23`
* **Pin 12 (RCLK / Latch)** ➔ ESP32 `GPIO 22`
* **Pin 11 (SRCLK / Clock)** ➔ ESP32 `GPIO 21`

### 3. Column Connections (Positive Side)
Place a **220Ω resistor** in series with each column wire:
* **Columns 1 through 8:** Connect via 220Ω resistors to `Q0` through `Q7` (Pins 15, 1–7) of the 74HC595.
* **Column 9:** Connect via a 220Ω resistor directly to **ESP32 `GPIO 4`**.

### 4. Row Connections (Negative Side via BC547 Transistors)
*(Hold the BC547 with the flat side facing you: Pins from left to right are **Collector, Base, Emitter**).*
* **Left Pin (Collector):** Connects to the negative row wire of the matrix.
* **Right Pin (Emitter):** Connects directly to ESP32 `GND`.
* **Middle Pin (Base):** Connects through a **1kΩ resistor** to the respective ESP32 GPIO:
  * **Row 1:** GPIO `19`
  * **Row 2:** GPIO `18`
  * **Row 3:** GPIO `5`
  * **Row 4:** GPIO `17`
  * **Row 5:** GPIO `16`

---

## 💻 Software Setup & Installation

1. Install the [Arduino IDE](https://www.arduino.cc/).
2. Ensure you have the **ESP32 Board Package** installed via the Board Manager.
3. Copy the firmware code into your Arduino IDE sketch.
4. Select your ESP32 board and upload the code.

---

## 🚀 How to Use

1. Power up your ESP32.
2. Open your smartphone or laptop Wi-Fi settings and connect to the network:
   * **Network Name:** `ESP32_Matrix`
   * **Password:** *(Leave blank / None)*
3. Open any web browser and navigate to the IP address:
   * **`http://192.168.4.1`**
4. Use the dashboard to stream text, sync your local time, toggle animations, or play Snake!

---

## 📜 License
This project is open-source and available under the [MIT License](LICENSE).
