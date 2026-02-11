# Digital Parameter Config Unit

Project: OLED display demo for Arduino Uno R4 using PlatformIO and CLion.

---

## Quick checklist
- Using CLion: yes (instructions below)
- Recommended IDE version: CLion 2023.3 or newer (see notes)
- Code overview: `src/main.cpp` — initializes SSD1306 OLED via I2C and prints text.
- Libraries: Adafruit_SSD1306, Adafruit_GFX, Wire, Arduino core (PlatformIO handles install)
- Dependencies: PlatformIO (platformio.ini), Arduino core for the target board
- Components: SSD1306 128x64 I2C OLED, Arduino Uno R4 (or compatible)
- Author: Replace the placeholder below with your name
- Software & hardware requirements: listed in a dedicated section

---

## Using CLion
This repository is set up for PlatformIO. You can use CLion in two common ways:

Option A — CLion with PlatformIO plugin (recommended):
1. Install CLion (recommended 2023.3 or newer).
2. Install the PlatformIO plugin for CLion via Settings -> Plugins -> Marketplace -> "PlatformIO".
3. Restart CLion and open this project directory (`digital-parameter-config-unit`).
4. PlatformIO should detect the project (reads `platformio.ini`) and provide Build / Upload / Monitor actions in the IDE.

Option B — CLion + PlatformIO Core (CLI):
1. Install PlatformIO Core (pip install platformio) or use the standalone installer.
2. Open the folder in CLion as a project.
3. Use PlatformIO CLI from the terminal inside CLion (or an external terminal):

   pio run              # build
   pio run -t upload    # build and upload to the board (make sure correct environment in platformio.ini)
   pio device monitor   # open serial monitor

Note: If you prefer to work without the PlatformIO plugin, the CLI option is stable and recommended.

---

## Recommended IDE Version
- CLion 2023.3 or newer is recommended because of improved PlatformIO integration and general toolchain support.
- If you must use an older CLion, prefer at least 2022.x. If you rely only on PlatformIO CLI, any CLion version that can open a folder will work.

(If you want, I can detect your installed CLion version and add it here — tell me to check the system.)

---

## Code overview
- File: `src/main.cpp`
- Purpose: Initialize an SSD1306 128x64 OLED display over I2C and print a few lines:
  - Sets up serial at 9600 baud.
  - Initializes the Adafruit_SSD1306 display with I2C address 0x3C.
  - Prints "Arduino Uno R4", "OLED with I2C", and "Hello World" to the OLED.
  - `loop()` is empty and available for extending with dynamic content.

Design notes:
- The project uses Adafruit libraries which require the Wire (I2C) library and the appropriate Arduino core.
- Display constructor: `Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);` — uses default reset pin disabled (-1). If your OLED module has a reset pin wired, change this parameter.

---

## Libraries
The code expects the following libraries (PlatformIO will install them when configured in `platformio.ini`):
- `Adafruit_SSD1306` — SSD1306 driver for OLED displays.
- `Adafruit_GFX` — graphics primitives used by Adafruit_SSD1306.
- `Wire` — Arduino I2C library (part of Arduino core).

If you open the PlatformIO project and it does not auto-install, add these to `platformio.ini` under `lib_deps` (example):

[env:uno_r4]
platform = atmelmegaavr
board = uno_r4
framework = arduino
lib_deps =
  adafruit/Adafruit SSD1306@^2.5.7
  adafruit/Adafruit GFX Library@^1.11.5

(Adjust versions and the environment name to match your `platformio.ini`.)

---

## Dependencies
- PlatformIO Core (CLI) or PlatformIO plugin for CLion
- Arduino core for your board (installed by PlatformIO)
- The Adafruit libraries listed above
- A working USB driver so your OS can access the Uno R4 serial/bootloader port

---

## Components (hardware used with the OLED)
- Arduino Uno R4 (or compatible board with I2C and 5V tolerant I/O)
- SSD1306-based OLED module, 128x64 pixels, I2C interface (commonly available at address 0x3C)
- I2C connections:
  - OLED VCC -> 3.3V or 5V (check module specs; many are 3.3V tolerant or have onboard regulator)
  - OLED GND -> GND
  - OLED SDA -> SDA pin on Uno R4 (usually A4 on classic UNO; check Uno R4 pinout)
  - OLED SCL -> SCL pin on Uno R4 (usually A5 on classic UNO; check Uno R4 pinout)
  - Optional: RESET pin -> if present and used, wire to appropriate MCU pin and update constructor

Notes:
- Verify the I2C address. Many SSD1306 modules use 0x3C but some use 0x3D.
- If the display doesn't initialize, check wiring, voltage, and the address.

---

## Software & Hardware Requirements
Software:
- CLion (recommended 2023.3+)
- PlatformIO (plugin or PlatformIO Core)
- Python 3.8+ (if installing PlatformIO Core via pip)
- Git (recommended)

Hardware:
- Arduino Uno R4 (or compatible board)
- SSD1306 128x64 OLED module with I2C pins
- USB cable for programming and serial
- Jumper wires and optional breadboard

---

## How to build and upload (CLI)
1. Install PlatformIO Core: `pip install platformio` or follow official installation docs.
2. From project root run:

   pio run
   pio run -t upload
   pio device monitor --baud 9600

Replace environment/board if your `platformio.ini` uses a different name.

---

## Troubleshooting
- "OLED not found" message on Serial: check wiring, power, and I2C address. Use an I2C scanner sketch or `pio device monitor` to confirm serial output.
- Compilation errors about missing libraries: add appropriate `lib_deps` to `platformio.ini` or install via PlatformIO library manager.
- If upload fails: ensure correct board is selected in `platformio.ini`, correct USB drivers are installed, and the board is in programming mode if required.

---

## Author
Project Author: <Your Name Here>
- Email: your.email@example.com (replace)
- Repository: (add repo URL if applicable)

---

## License
This repository does not include a license. Add a LICENSE file if you plan to publish or share the code.

---

If you'd like, I can:
- Detect your local CLion version and insert it into this README.
- Add a sample `platformio.ini` snippet tailored to your board if you provide the exact PlatformIO board ID.
- Extend `src/main.cpp` to show dynamic content (time, sensor readings, menu system).

