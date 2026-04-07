# RC---Transmitter-Code-Receiver-Code
---

# 6-Channel LoRa RC Transmitter & Receiver

Yeh ek high-range Remote Control (RC) system hai jo **Arduino Nano** aur **LoRa SX1278 (Ra-02)** modules par adharit hai. Yeh system purane nRF24L01 modules ke muqable behtar range (1km+) aur deewaron ke paar bhi solid connectivity pradan karta hai.

## ⚠️ Important: Antenna Warning
**LoRa module ko bina antenna ke kabhi bhi power-on na karein.** Aisa karne se module ki chip turant kharab (burn) ho sakti hai. 433MHz ke liye exactly **17.3 cm** lambi copper wire ka upyog karein.

---

## ✨ Features
* **Channels:** 6 Independent Channels (4 Joysticks, 1 Toggle Switch, 1 Potentiometer).
* **Range:** 1km se 3km tak (Khule maidan mein).
* **Frequency:** 433 MHz (LoRa Spread Spectrum).
* **Fail-safe:** Signal loss hone par motors apne aap band ho jayenge.
* **Low Power Consumption:** Chote DC motors aur Brushless motors dono ke liye upyogi.

---

## 🔧 Hardware Connections (Transmitter & Receiver)

Dono side par LoRa module ke connections **bilkul same** rahenge:

| LoRa Ra-02 Pin | Arduino Nano Pin | Function |
| :--- | :--- | :--- |
| **VCC** | **3.3V** | Power (DO NOT USE 5V) |
| **GND** | **GND** | Ground |
| **NSS** | **D10** | SPI Chip Select |
| **MOSI** | **D11** | SPI Data Out |
| **MISO** | **D12** | SPI Data In |
| **SCK** | **D13** | SPI Clock |
| **RST** | **D9** | Reset |
| **DIO0** | **D2** | Interrupt |

### Transmitter Controls
* **Throttle:** Analog A0
* **Yaw:** Analog A1
* **Pitch:** Analog A2
* **Roll:** Analog A3
* **AUX 1 (Switch):** Digital D2 (Input Pullup)
* **AUX 2 (Pot):** Analog A7

### Receiver Outputs
* **CH1 to CH6:** Digital Pins 9, 2, 3, 4, 5, 6 (Servos/ESC ke liye)

---

## 💻 Software Setup

1.  Arduino IDE kholein.
2.  **Library Manager** mein jayein (`Ctrl+Shift+I`).
3.  **"LoRa"** search karein aur `LoRa by Sandeep Mistry` install karein.
4.  Transmitter aur Receiver code ko alag-alag Arduino Nano par upload karein.
5.  Serial Monitor ko **9600 Baud** par set karke status check karein.

---

## 🚀 Troubleshooting
* **Range Issue:** Check karein ki antenna 17.3 cm ka hai ya nahi. Module ko Arduino se thoda door rakhein.
* **No Connection:** Dono modules mein `LoRa.begin(433E6)` aur `SpreadingFactor` same hona chahiye.
* **Servo Jitter:** Ensure karein ki battery (7.4V Li-po) stable power de rahi hai.

---

## 🛠️ Components Used
* 2x Arduino Nano
* 2x LoRa Ra-02 (SX1278) Modules
* 2x Joysticks
* 1x Potentiometer & 1x Toggle Switch
* 1x 7.4V Li-po Battery

---

# 6-Channel nRF24L01 RC Transmitter & Receiver

Yeh project ek high-performance Remote Control (RC) system hai jo **Arduino Nano** aur **nRF24L01+PA+LNA** modules ka upyog karta hai. Iska upyog RC Planes, Drones, aur Cars ko control karne ke liye kiya ja sakta hai.

## ⚠️ Important: Power & Range Tips
* **Capacitor:** nRF module ke VCC aur GND ke beech **100uF se 1000uF** ka capacitor zaroori hai.
* **Adapter:** Hamesha **3.3V Adapter Board** ka upyog karein taaki nRF ko stable power mile.
* **Antenna:** PA+LNA module ko bina antenna ke power-on na karein.

---

## ✨ Features
* **Channels:** 6 Channels (4 Analog Joysticks, 1 Digital Switch, 1 Potentiometer).
* **Range:** Optimized for maximum range using `250KBPS` data rate.
* **Fail-safe:** Signal loss hone par throttle apne aap safe position (12) par aa jata hai.
* **Frequency:** 2.4 GHz (Channel 108/115 to avoid WiFi interference).

---

## 🔧 Hardware Connections

Dono (Transmitter aur Receiver) mein nRF module ke connections **same** rahenge:

| nRF24L01 Pin | Arduino Nano Pin | Function |
| :--- | :--- | :--- |
| **VCC** | **5V (Adapter se)** | Input to 3.3V Adapter |
| **GND** | **GND** | Common Ground |
| **CE** | **D7** | Chip Enable |
| **CSN** | **D8** | Chip Select Not |
| **SCK** | **D13** | SPI Clock |
| **MOSI (MO)** | **D11** | SPI Data Out |
| **MISO (MI)** | **D12** | SPI Data In |

### Transmitter Controls
* **Throttle / Yaw / Pitch / Roll:** Analog A0, A1, A2, A3
* **AUX 1 (Switch):** Digital D2 (INPUT_PULLUP)
* **AUX 2 (Knob):** Analog A7

### Receiver Outputs
* **CH1 - CH6:** Digital Pins 9, 2, 3, 4, 5, 6 (Servos aur ESC ke liye)

---

## 💻 Software Setup

1.  Arduino IDE mein **RF24** library install karein (by TMRh20).
2.  Transmitter aur Receiver codes ko upload karein.
3.  **Baud Rate:** Serial Monitor ko **250000** par set karein data dekhne ke liye.

### Range Optimization Settings (Code mein):
```cpp
radio.setPALevel(RF24_PA_MAX);      // Max Power
radio.setDataRate(RF24_250KBPS);   // Low Speed = High Range
radio.setChannel(108);             // Custom Channel
```

---

## 🛠️ Troubleshooting
1.  **6 Meter Range Issue:** Agar range kam hai, toh `setDataRate(RF24_250KBPS)` check karein aur capacitor ko check karein.
2.  **No Connection:** Check karein ki `pipe address` aur `channel` dono side par bilkul same hain.
3.  **LED Check:** Receiver mein Pin 13 ki LED jalni chahiye jab transmitter on ho.

---

## 📦 Components List
* 2x Arduino Nano
* 2x nRF24L01+PA+LNA Modules (with Antenna)
* 2x nRF24L01 Voltage Adapter Boards
* 2x Joysticks (Dual Axis)
* 1x 7.4V Li-po Battery (2S)

---
