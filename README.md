# PLL-Project
An on-chip clock mulitplier PLL designed using open source tools and sky130nm pdk

## Introduction
A clock multiplier Phase-Locked Loop (PLL) is a negative feedback control system that generates a high-frequency output clock whose phase is related to the low frequency input clock. The need for PLLs is widespread as they find application in analog, digital, RF and communication systems. <br>The low-frequency clock can be generated using a crystal with frequencies up to 200 MHz. Generating a high-frequency clock with high spectral purity is not possible with a crystal and this is where PLLs come into play. <br>

A simple PLL consists of a Phase and Frequency Detector (PFD), Charge Pump (CP), Loop Filter (LF), Voltage Controlled Oscillator (VCO) and a frequency divider in the feeback path <br>

This PLL design multiplies clock frequency by 8 times. 

## Significance of a PLL 
<img width="1137" height="731" alt="src" src="https://github.com/user-attachments/assets/ca4d1e74-db2e-43b9-a10b-9e4990002d36" />

</p>The processors used in our smartphones have various modules inside serving different purposes. These modules may include CPU, GPU, RAM, WiFi module, Audio module, and so on. 

</p> The interesting thing is that each of these modules may not run at a particular clock frequency. For example, the CPU would need a high clock frequency for performing calculations faster, while the Display module may not.
</p> This is where a Phase-Locked Loop circuit comes into the picture. As shown in Figure above, a PLL is installed at the clock entry point of each above module to produce the desired frequency at which the module would operate.
</p>

<br>

## Specifications

### Pre layout simulations

| Parameter | Description | min | val | max | Unit | Conditions |
| --- | --- | --- | --- | --- | --- | --- |
| VDD | Digital Supply | - | 1.8 | - | V | T = 27C |
| F<sub>CLKREF</sub> | Reference | 5 | 9 | 12.5 | MHz | T = 27C |
| F<sub>CLKOUT</sub> | Output Clock | 40.98 | 71.42 | 100 | MHz | PLL Mode, T = 27C |
| V<sub>ctrl</sub> | Control Voltage | 0.77 | 0.817 | 0.844 | MHz | PLL Mode, T = 27C |
| DC | Duty Cycle | 60.24 | 61.26 | 61.38 | % | T = 27C | 
| T<sub>SET</sub> | Settling Time | ~12 | ~11.5 | ~9 | us | T = 27C |


### Post layout simulations

| Parameter | Description | min | val | max | Unit | Conditions |
| --- | --- | --- | --- | --- | --- | --- |
| VDD | Digital Supply | - | 1.8 | - | V | T = 27C |
| F<sub>CLKREF</sub> | Reference | 5 | 9 | 12.5 | MHz | T = 27C |
| F<sub>CLKOUT</sub> | Output Clock | 40.76 | 73.26 | 100 | MHz | PLL Mode, T = 27C |
| V<sub>ctrl</sub> | Control Voltage | 0.732 | 0.780 | 0.789 | MHz | PLL Mode, T = 27C |
| DC | Duty Cycle | 56.82 | 58.82 | 60.27 | % | T = 27C | 
| T<sub>SET</sub> | Settling Time | ~8.6 | ~5.1 | ~6.4 | us | T = 27C |

## Block Diagram

<img width="1282" height="364" alt="block diagram" src="https://github.com/user-attachments/assets/c13958f7-c131-4f72-8fe8-307d2c41d3c6" />
<br>

## EDA tools used

1. xschem
2. ngspice
3. magic vlsi

## Pre layout simulations

 ### 1. Phase frequency detector (PFD)  </p>
A phase frequency detector or a phase comparator outputs an UP or a DOWN signal depending upon the timed phase difference between the input signal and reference signal. If the input signal leads the reference signal an UP signal is produced whereas if the input lags the reference signal a down signal is produced. </p>
 
