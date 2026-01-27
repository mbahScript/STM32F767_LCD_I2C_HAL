# STM32F767_LCD_I2C_HAL

This repository contains an embedded systems project developed using the **STM32F767ZI Nucleo board** and **STM32CubeIDE**.  
The project demonstrates how to interface a **16x2 character LCD** with STM32 using **I²C communication** via an **I²C LCD backpack (PCF8574 / PCF8574A)**.

---

## Project Overview

### I2C_LCD_Display
A beginner-friendly LCD interface project that displays text on a **16x2 LCD** using **STM32 HAL drivers** and **I²C communication**.

**Key Features:**
- I²C-based LCD communication  
- STM32CubeMX configuration  
- HAL-based LCD driver  
- Reduced GPIO usage (SDA & SCL only)  
- Simple and modular project structure  

---

## Hardware Used
- **Board:** STM32F767ZI Nucleo  
- **LCD:** 16x2 Character LCD  
- **Interface:** I²C LCD Backpack (PCF8574 / PCF8574A)  
- **IDE:** STM32CubeIDE  

### I2C Pin Mapping

| LCD I2C Backpack | STM32F767ZI Pin |
|-----------------|----------------|
| SDA             | PB9 (I2C1_SDA) |
| SCL             | PB8 (I2C1_SCL) |
| VCC             | 5V             |
| GND             | GND            |

> ⚠️ **Note:** Most I²C LCD backpacks require **5V** for proper contrast. Using **3.3V** may result in a blank display.

---

## LCD I2C Address
- `0x27` → PCF8574  
- `0x3F` → PCF8574A  

> STM32 HAL uses **8-bit addressing**, so the address is shifted internally.  
> **Example:**  
> ```c
> 0x27 << 1 = 0x4E
> ```

---

## Software Configuration (STM32CubeMX)
- **Enable:** I2C1  
- **Mode:** I²C  
- **Clock Speed:** 100 kHz  

**Pin Configuration:**
- PB8 → SCL  
- PB9 → SDA  

> No manual GPIO configuration is required for the LCD.

---

## Common Issues & Fixes

### Issue 1: LCD is blank
- **Cause:** Powered with 3.3V  
- **Fix:** Use **5V** and adjust the contrast potentiometer

### Issue 2: `implicit declaration of function` warning
- **Cause:** Missing function prototypes  
- **Fix:** Ensure all LCD functions are declared in `lcd_i2c.h` and included in `main.c`

### Issue 3: No I²C communication
- **Cause:** Incorrect pin mapping or I²C address  
- **Fix:** Verify PB8/PB9 configuration and confirm LCD address (`0x27` or `0x3F`)

---

## How to Run the Project
1. Open **STM32CubeIDE**  
2. Import the project  
3. Build the project  
4. Flash to the **STM32F767ZI**  
5. Adjust LCD contrast  
6. Observe text displayed on the LCD

---

## Reference
This project was implemented using concepts explained on the **ControllersTech** YouTube channel:  
[https://www.youtube.com/@ControllersTech](https://www.youtube.com/@ControllersTech)  

*(Used as a learning reference for STM32 I²C LCD interfacing and HAL usage.)*

---

## Future Improvements
- Display STM32 internal **RTC time** on LCD  
- Convert LCD code into a **reusable driver library**  
- Support **20x4 LCD modules**  
- Add **I²C error handling and debugging output**  

---

## Author
Developed as part of hands-on learning in **Embedded Systems and STM32 Microcontroller Programming**.
