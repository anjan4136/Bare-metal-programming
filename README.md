# Bare-metal-programming
Bare-metal programming of stm32f407 discovery board. Here no Hardware abstraction layer are used and code is written from scratch.
# 1. LED Toggle Example for STM32F4 (ARM Cortex-M4)

This example demonstrates how to toggle an LED using an STM32F4 microcontroller (specifically, the ARM Cortex-M4 core). The code configures a GPIO pin as an output and toggles the state of the LED connected to that pin.

## Prerequisites

- STM32F4 development board (e.g., STM32F407 Discovery)
- STM32CubeIDE or other compatible development environment
- Basic knowledge of STM32 peripherals and registers

## Hardware Setup

1. Connect an LED to GPIO pin PD12 (or any other available GPIO pin).
2. Ensure that the development board is properly powered and connected.

## Code Explanation

1. Clock Configuration
   - The code enables the clock for GPIO D peripheral by setting the 3rd bit in the AHB1ENR register.
2. GPIO Configuration
   - The GPIO pin PD12 is configured as an output by setting the 24th bit in the MODER register.
3. LED Toggle Loop
   - The code enters an infinite loop where it toggles the state of the LED
     - Sets the 12th bit of the output data register to turn ON the LED.
     - Introduces a delay (for human observation).
     - Clears the 12th bit to turn OFF the LED.
     - Introduces another delay.

## Usage

1. Compile and flash the code to your STM32F4 board.
2. Observe the LED connected to PD12 toggling ON and OFF.
