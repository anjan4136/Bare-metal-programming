# STM32F407G Emergency SOS signalling

## Description
This project demonstrates how to read input from GPIOA pin 0 on an STM32F407G Discovery Board and control an LED connected to GPIOD pin 12 based on the input status.

## Table of Contents
- Overview
- Hardware Requirements
- Software Requirements
- Installation
- Usage
- Code
- Contributing
- License
- Contact

## Overview
The project configures GPIOA pin 0 as an input and GPIOD pin 12 as an output. When the input button pin is high (connected to VDD), the LED turns on. When the input button pin is low (connected to GND), the LED turns off.

## Hardware Requirements
- STM32F407G Discovery Board
- LED
- Resistors
- Breadboard and jumper wires

## Software Requirements
- STM32CubeIDE or any other suitable IDE for STM32 development
- STM32CubeMX (optional for pin configuration)

## Installation
1. Clone the repository:
    ```bash
    git clone https://github.com/anjan4136/Bare-metal-programming.git
    cd Bare-metal-programming
    ```

2. Open the project in STM32CubeIDE.

3. Build and flash the project to your STM32F407G Discovery Board.

## Usage
1. Connect the LED to GPIOD pin 12 with a suitable resistor.
2. Connect a button or any input source to GPIOA pin 0.
3. Power on the STM32F407G Discovery Board.
4. The LED will turn on when the input button pin is high and turn off when the input button pin is low.

## Code
Here's the main code for the project:

```c
int main(void)
{
    uint32_t volatile *const pClkCtrlReg = (uint32_t*)0x40023830;
    uint32_t volatile *const pPortDModeReg = (uint32_t*)0x40020C00;
    uint32_t volatile *const pPortDOutReg = (uint32_t*)0x40020C14;

    uint32_t volatile *const pPortAModeReg = (uint32_t*)0x40020000;
    uint32_t const volatile *const pPortAInReg = (uint32_t*)0x40020010;

    // Enable the clock for GPIOD and GPIOA peripherals in the AHB1ENR
    *pClkCtrlReg |= (1 << 3);
    *pClkCtrlReg |= (1 << 0);

    // Configuring PD12 as output
    *pPortDModeReg &= ~(3 << 24);
    // Make 24th bit position as 1 (SET)
    *pPortDModeReg |= (1 << 24);

    // Configure PA0 as input mode (GPIOA MODE REGISTER)
    *pPortAModeReg &= ~(3 << 0);

    while (1)
    {
        // Read the pin status of the pin PA0 (GPIOA INPUT DATA REGISTER)
        uint8_t buttonStatus = (uint8_t)(*pPortAInReg & 0x1); // Zero out all other bits except bit 0

        if (buttonStatus) {
            // Turn on the LED
            *pPortDOutReg |= (1 << 12);
        } else {
            // Turn off the LED
            *pPortDOutReg &= ~(1 << 12);
        }
    }
}
