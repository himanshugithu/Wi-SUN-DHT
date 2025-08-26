# Wi-SUN DHT11 Minimal Example

This project demonstrates how to read temperature and humidity from a DHT11 sensor using a Silicon Labs EFR32 device and print the results over UART.

## Hardware
- Silicon Labs EFR32 board (tested on BRD4271A)
- DHT11 sensor
- DHT11 data pin connected to Port C, Pin 1 (PC01)
- 3.3V and GND to DHT11

## Usage
1. Build and flash the project to your EFR32 board.
2. Open a serial terminal (e.g., Tera Term, PuTTY) at the correct COM port and baud rate (default: 115200).
3. You will see temperature and humidity readings printed every ~2 seconds.

## How to Use DHT11 in Your Own Code
1. Include the header:
   ```c
   #include "dht.h"
   ```
2. Initialize the sensor once (e.g., at startup):
   ```c
   DHT11_Init();
   ```
3. Read data whenever needed:
   ```c
   DHT11_Data_t dht_data;
   if (DHT11_Read(&dht_data)) {
       // Use dht_data.humidity_int, dht_data.temperature_int, etc.
   }
   ```

## Code Overview
- `dht.c`/`dht.h`: DHT11 driver (bit-banged, uses DWT for timing)
- `app.c`: Minimal main loop, reads and prints DHT11 data

## Customization
- To change the data pin, edit `DHT11_PORT` and `DHT11_PIN` in `dht.c`.
- To change the read interval, adjust the delay loop in `app.c`.

## Troubleshooting
- If you see only "DHT11 read failed!", check wiring and power to the sensor.
- If you want debug output, set `#define DHT_DEBUG 1` in `dht.c`.

---

MIT License. See source files for details.
