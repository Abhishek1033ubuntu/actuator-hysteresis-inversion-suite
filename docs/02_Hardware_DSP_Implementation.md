# Hardware & DSP Integration Guidelines

Translating the Python simulation into real-time industrial hardware requires strict adherence to digital signal processing (DSP) constraints.

## 1. Microcontroller / DSP Requirements
* **Architecture:** 32-bit Floating-Point Unit (FPU) required (e.g., ARM Cortex-M7 or TI C2000 series).
* **Clock Speed:** $\ge 200$ MHz to ensure the RD-PI array math executes in $\le 3.8 \ \mu\text{s}$.
* **Control Loop Rate:** Minimum 100 kHz update frequency ($\Delta t = 10 \ \mu\text{s}$).

## 2. Analog-to-Digital (ADC) / Digital-to-Analog (DAC)
To support 0.32% tracking precision on a sub-micron scale:
* **DAC Resolution:** Minimum 16-bit to provide smooth pre-distortion voltage mapping without quantization step-chatter.
* **ADC Resolution:** 16-bit simultaneous sampling for the capacitive position feedback sensor.

## 3. High-Voltage Amplifier Interface
* The pre-distorted logical signal ($0 - 3.3\text{V}$) must be stepped up to the operational voltage of the PIN-PMN-PT actuator ($0 - 150\text{V}$). 
* The amplifier must have a large-signal bandwidth of $\ge 10$ kHz to prevent low-pass filtering of the high-frequency SMO switching signal.
