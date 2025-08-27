MSP430G2553 – Lab 6 (Assembly) — README

Short Summary
------------
This repository contains assembly code for the MSP430G2553 microcontroller.
The program runs directly on the MCU and demonstrates a small embedded application built with
interrupts, timers, an event‑driven state machine (FSM), and an LCD interface.

What the Project Does
---------------------
- Mode 1 – Signal Classification:
  After pressing PB0, the system enters an ADC sampling mode. The input analog signal (from a signal generator)
  is sampled through the ADC10 and processed in real-time. The program analyzes the samples to identify the waveform
  type (sine, triangle, or PWM) and displays the result on the LCD. Refreshes every ~1 second

- Mode 2 – Average Voltage Measurement:  
  After pressing PB1, the system again samples the analog input via ADC10, but instead of classification, it computes
  the average voltage (Vavg).

- Idle Mode:  
  When no mode is active, the MCU remains idle/low-power until the next button press.

Repository Files
----------------
• prelab6_main.s43  — main program, ISRs, and the FSM control flow (IAR assembly).
• prelab6_api.s43   — simple API used by the application (LCD print, mode changes, etc.).
• prelab6_hal.s43   — hardware abstraction (ADC, timers, GPIO, LCD low‑level).
• prelab6_bsp.s43   — board support (device/clock/ports setup).
• prelab6_bsp.h     — pin/port definitions and small macros used by the BSP/HAL.
(If your wiring differs, update the pin definitions in prelab6_bsp.h accordingly.)

Target Hardware
---------------
• MCU: MSP430G2553 
• Buttons / LCD: connected to the ports as defined in prelab6_bsp.h.
• Function generator (optional), within 0–VCC input range, if you want to feed an analog signal
  for the ADC demonstration.

How to Build & Flash (IDE Only)
-------------------------------
IAR Embedded Workbench for MSP430 
1) Create Workspace, then create a new MSP430 assembler project and select device: MSP430G2553.
2) Add main.s43, api.s43, hal.s43, bsp.s43, and bsp.h to the project.
3) Press build. Then go to Project and then Download and Debug (Ctrl+D).
   IAR will erase, program, and start a debug session on the MCU.
4) Press Run to start execution. To reprogram, stop the session and download again.


How to Use (Runtime)
--------------------
• After flashing, the program starts in an idle or default mode.
• Use the board buttons to switch modes (for example: measure/average/display). Exact button-to‑mode
  mapping is defined in prelab6_bsp.h and in comments near the ISR in prelab6_main.s43.
• The LCD shows the current mode and/or the measured/processed value.

Notes
-----
• This code is intended to be FLASHED to the MSP430G2553 MCU.
• If you port to another MSP430 family, update BSP/HAL (e.g., ADC10 → ADC12 on x4xx devices).
• Keep wiring consistent with the pin macros in prelab6_bsp.h.
• For other MSP430 devices, update BSP/HAL layers.

License
-------
MIT
