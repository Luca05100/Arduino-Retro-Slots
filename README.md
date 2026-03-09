# 🎰 Arduino Retro-Slots

![C++](https://img.shields.io/badge/Language-C++-00599C?style=for-the-badge&logo=c%2B%2B)
![Arduino](https://img.shields.io/badge/Platform-Arduino-00979D?style=for-the-badge&logo=arduino)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

A fully functional, retro-style slot machine simulator built using **Arduino Uno**. This project brings the classic casino experience to a breadboard, featuring an OLED display for animations, physical buttons for interaction, and a buzzer for authentic sound effects.

---

## ✨ Key Features

* **Interactive Gameplay:** Real-time slot spinning animations on a 0.96" OLED screen.
* **Audio Feedback:** Authentic retro sound effects for spinning, winning, and losing.
* **Credit System:** Built-in logic to manage player credits and winnings.
* **Physical Controls:** Tactile buttons for "Spin", "Bet", and "Reset".
* **Visual Indicators:** LED alerts for winning combinations.

---

## 📸 Project Preview

<img width="463" height="459" alt="Screenshot 2026-03-09 at 21 31 26" src="https://github.com/user-attachments/assets/d263b9a9-4346-4008-8b58-573215393eec" />



---

## 🛠️ Hardware Requirements

To replicate this project, you will need the following components:

* **Microcontroller:** Arduino Uno (or compatible)
* **Display:** 0.96" OLED Display (SSD1306 I2C)
* **Input:** 3x Push Buttons (with 10kΩ pull-down resistors)
* **Sound:** 1x Passive Buzzer
* **Indicator:** 1x LED (with 220Ω resistor)
* **Prototyping:** Breadboard and Jumper Wires

---

## 🧠 Technical Challenges Overcome

Building a game on a microcontroller with limited resources came with several engineering hurdles:

### 💾 1. Memory Management (SRAM Optimization)
The **SSD1306 OLED** driver requires a 1KB buffer to manage the display pixels. Since the **Arduino Uno (ATmega328P)** has only 2KB of SRAM in total, this left very little room for game logic and variables.
* **Solution:** I optimized the code by using the `F()` macro for all static strings (storing them in Flash memory instead of SRAM) and minimized the use of global variables to prevent stack overflow.

### ⚡ 2. Button Debouncing
Mechanical buttons create "noise" (multiple rapid signals) when pressed, which would cause the slots to spin multiple times or glitch.
* **Solution:** I implemented a **software-based debouncing logic** using timing intervals. This ensures that only the first clean signal is registered, providing a smooth and responsive user experience.



### 🎲 3. True Randomization
Computers are deterministic, meaning `random()` functions often produce the same sequence of numbers every time the device starts.
* **Solution:** I used `randomSeed()` combined with `analogRead()` on an **unconnected (floating) analog pin**. The background electromagnetic noise provides a truly unique seed every time the Arduino boots, ensuring the slot results are never predictable.


---

## 🔌 Pin Mapping

| Component | Arduino Pin | Description |
| :--- | :--- | :--- |
| **OLED SDA** | `A4` | I2C Data Line |
| **OLED SCL** | `A5` | I2C Clock Line |
| **Button 1** | `D2` | Spin / Start |
| **Button 2** | `D3` | Bet Amount |
| **Button 3** | `D4` | Reset / Menu |
| **Buzzer** | `D5` | Sound Output |
| **LED** | `D6` | Win Indicator |



---

## 📂 Project Structure

```text
📦 Arduino-Retro-Slots
 ┣ 📂 Arduino_Retro_Slots   # Main sketch folder
 ┃ ┗ 📜 Retroslots.ino      # Source code
 ┣ 📂 docs                  # Documentation & Schematics
 ┃ ┗ 📜 assembly_photo.jpg  # Real build photo
 ┣ 📜 .gitignore            # Clean repo files
 ┗ 📜 README.md             # Project documentation
 ```

 ---

## 🚀 How to Run Locally

Follow these steps to get your **Retro-Slots** machine up and running on your local Arduino:

### 1️⃣ Clone the Repository
Open your terminal and run the following commands:
```bash
# Clone the project
git clone [https://github.com/Luca05100/Arduino-Retro-Slots.git](https://github.com/Luca05100/Arduino-Retro-Slots.git)

# Enter the project directory
cd Arduino-Retro-Slots
```

## 🔧 Prerequisites & Libraries

Before uploading the code, ensure you have the following software and libraries installed:

### 1. Software
* **Arduino IDE:** Download and install the latest version from the [official Arduino website](https://www.arduino.cc/en/software).

### 2. Required Libraries
You need to install these libraries via the **Arduino Library Manager** to handle the OLED display and graphics:

* **Adafruit SSD1306:** The main driver for the 128x64/128x32 OLED displays.
* **Adafruit GFX Library:** The core graphics library for drawing shapes, text, and animations.
* **Adafruit BusIO:** A dependency required by most Adafruit libraries for I2C/SPI communication.

### 📥 How to Install Libraries
1. Open **Arduino IDE**.
2. Go to **Sketch** > **Include Library** > **Manage Libraries...** *(Or press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd> on Windows/Linux or <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd> on Mac).*
3. Search for **"Adafruit SSD1306"** and click **Install**.
4. Search for **"Adafruit GFX"** and click **Install**.
5. If prompted to install "Dependencies" (like Adafruit BusIO), click **Install All**.

