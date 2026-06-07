# Design and Implementation of a Clock Multiplier Phase-Locked Loop using Open-Source EDA Tools in 130nm CMOS Technology

<div align="center">

![PDK](https://img.shields.io/badge/PDK-SkyWater%20130nm-blue?style=for-the-badge)
![Tools](https://img.shields.io/badge/EDA-xschem%20%7C%20ngspice%20%7C%20magic-orange?style=for-the-badge)
![Type](https://img.shields.io/badge/Design-Full%20Custom%20Analog-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Pre%20%26%20Post%20Layout%20Verified-brightgreen?style=for-the-badge)
![Multiplier](https://img.shields.io/badge/Clock%20Multiplier-8x-purple?style=for-the-badge)

</div>

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

##  Key Highlights

-  **Full custom analog IC design** — schematic to layout, entirely from scratch
-  **8× clock multiplication** verified across 5 MHz – 12.5 MHz input range
-  **Pre-layout AND post-layout** SPICE simulations both passing spec
-  **Open-source EDA stack**: xschem + ngspice + magic VLSI — no proprietary tools
-  **SkyWater 130nm PDK** — production-grade open-source foundry process
-  **Lock-in time as fast as ~5.1 µs** — fast settling post-layout verified
-  **Circuit area: 0.2641 mm²** — compact layout with full DRC compliance
-  **Loop filter stability** designed with zero-pole analysis (R-C network)


##  Tech Stack

| Tool | Purpose |
|---|---|
| **xschem** | Schematic entry and netlist generation |
| **ngspice** | SPICE simulation (pre & post layout) |
| **magic VLSI** | Physical layout design and DRC |
| **SkyWater 130nm PDK** | Open-source foundry process design kit |

##  PLL Architecture

A classical charge-pump PLL architecture with 5 functional blocks:

<img width="1440" height="680" alt="image" src="https://github.com/user-attachments/assets/e1c9c3ac-c5b3-4fd5-b89b-dff66e2443e7" />


| Block | Function |
|---|---|
| **Phase Frequency Detector (PFD)** | Compares phase/frequency of reference and feedback; outputs UP/DOWN pulses |
| **Charge Pump (CP)** | Converts UP/DOWN pulse width to proportional current injection |
| **Loop Filter (LF)** | R-C low-pass filter; converts current to stable VCO control voltage |
| **Voltage Controlled Oscillator (VCO)** | Differential ring oscillator; output frequency ∝ V<sub>ctrl</sub> |
| **Frequency Divider (÷8)** | Three cascaded ÷2 flip-flop stages; feeds divided output back to PFD |




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


## Pre layout simulations

 ### 1. Phase frequency detector (PFD)  </p>
A phase frequency detector or a phase comparator outputs an UP or a DOWN signal depending upon the timed phase difference between the input signal and reference signal. If the input signal leads the reference signal an UP signal is produced whereas if the input lags the reference signal a down signal is produced. </p>
 
**Circuit of PFD used** </p>
<img width="1157" height="553" alt="PFD_ckt" src="https://github.com/user-attachments/assets/7065871d-9bfc-43de-ae95-9537e7593a00" />
<p>

 - input signal - f_clk_in
  - reference signal - f_vco

  </p>
There is a 1ns difference between the time period of f_vco and f_clk_in. This is done to emulate phase & frequency error.   </p>

  **Expected output** </p>
<img width="1176" height="517" alt="Output_expected" src="https://github.com/user-attachments/assets/c8b0192d-fd47-4aad-a198-e86e8d9e94e5" />
**Simulated output** </p>

 - considering constant phase difference between input signal and reference signal </p>
  
 <img width="1712" height="867" alt="pfd_const_phase_diff" src="https://github.com/user-attachments/assets/404ae1af-5980-4b13-99fa-5410615b2ca0" />
  </p>
   <br>

<img width="1397" height="292" alt="pfd_sim2" src="https://github.com/user-attachments/assets/f03c554b-d313-43c0-8f8a-8678eac62267" />


Fig - Representation as a Phase error detector <br>

   - considering input and reference signal to have different time periods </p>

   <img width="1157" height="553" alt="PFD_ckt" src="https://github.com/user-attachments/assets/4c599643-6e12-4ea6-9eaa-59fdf23957f4" />
</p>
   
In the above simulation result when **f_clk_in** **leads** **f_vco** , **UP** signal is triggered (yellow). While when the **f_clk_in lags f_vco** , **DOWN** signal is triggered. 
These two (up & down) signals are fed into the charge pump which is the next block of our implemented PLL.</p>


### 2. Charge Pump and Loop filter  </p>

### Charge Pump </p>
 These UP and DOWN pulses are fed into the input of the charge pump. The charge pump is a combination of switches connected to the power supply. This system acts as a current source/sink which injects/draws current into/from the loop filter, based on the duty cycle of UP/DOWN signal. </p>

 **Circuit of Charge Pump used** </p>
<img width="1702" height="877" alt="charge_pump_ckt" src="https://github.com/user-attachments/assets/2cba1765-941b-41c8-a40b-9b5402c98f8d" />
</p>
In the above schematic transistors M4 and M3 act as current sources while transistors M18 and M10 are current mirrors. The schematic shown above contains the loop filter. One can see it at the Vctrl output pin. </p>

### Loop filter </p>
This charge pump current is fed into the low pass filter. The low pass filter is a capacitor in series with a resistor. The entire system is connected in shunt with the control loop. The duration of pulses from the charge pump decides the amount of charge injected in the capacitor. </p> 

**Circuit of loop filter used** </p>

<img width="1359" height="789" alt="loop_filter_ckt" src="https://github.com/user-attachments/assets/c5cd525f-f617-4bf1-a331-b79ce1285e5a" />

</p>
This charge on the plates of the capacitor generates a voltage, which is then used as the control signal (Vctrl) to the VCO. </p>

**Design considerations of Loop filter**</p>
The loop filter consists of a resistor in series with a capacitor. This combination is in parallel with another capacitor as shown in figure above Capacitor C3 adds an integrator path and introduces a pole. The resistor adds a proportional path and introduces a zero. Thus, the system is stable with the addition of these two paths. Capacitor C5 is used to suppress the Vctrl ripple. However, the addition of an additional capacitor comprises on the stability of the PLL. This is because C5 adds another pole. So, to mitigate this issue the value of C5 is chosen to be very small than C3 (~C5 = 0.2*C3) </p>

**Expected output (CP+LF)** </p>
<img width="582" height="376" alt="(CP+LP)Expected output" src="https://github.com/user-attachments/assets/785037f4-589d-41b9-abd0-40fb5246c4e0" />

**Simulated output (CP + LF)** </p>

**Charge pump output for UP signal** </p>
<img width="498" height="282" alt="CPO UP signal" src="https://github.com/user-attachments/assets/db3d301e-4803-46ce-b864-6ab94cce7dac" />
</p>

**Charge pump output for DOWN signal** </p>
<img width="861" height="616" alt="CPO DOWN signal" src="https://github.com/user-attachments/assets/2aede4c8-1c81-420e-a308-bfd59b503edf" />

### Voltage controlled oscillator  
</p>

The control voltage is fed to a differential ring oscillator VCO. The VCO produces an output which is oscillating in nature. The frequency of these oscillations is a function of control voltage. </p>

**Schematic of VCO** </p>
<img width="842" height="628" alt="VCO Schematics" src="https://github.com/user-attachments/assets/2af94cba-2fba-41dc-aa46-969014cee8ba" />

<br>

**Simulated output of VCO** </p>
<img width="1166" height="564" alt="PLL_13" src="https://github.com/user-attachments/assets/41bd2717-090b-4b1c-8631-ec126d3e8cea" />

</p>

We can see that the frequency of oscillations increases with increase in control voltage input to VCO. </p>

### Frequency Divider 
</p>
The frequency divider used in this circuit divides the input frequency by 8 times. </p>

**Simulated output** </p>
<img width="843" height="622" alt="Simulated output" src="https://github.com/user-attachments/assets/e466984e-e6e6-40c3-a07c-0cb8ae5c06fd" />
</p>

## Full PLL Simulation  
</p>

**Integrated schematic** </p>
<img width="872" height="587" alt="Integrated Schematic" src="https://github.com/user-attachments/assets/7455d32e-7f62-4e0f-86fb-a22d8c5759ac" />

</p>

### Pre layout Simulation results
</p>

Generates 8x Multiplied Clock

<b> Pre-Layout: </b> <br>

Frequency Obtained for 5Mhz input: &nbsp;&nbsp;&nbsp; 40.98MHz <br>
Frequency Obtained for 12.5Mhz input: &nbsp;&nbsp;&nbsp; 100MHz

Duty Cycle obtained: &nbsp;&nbsp;&nbsp; 60.24% at 40MHz and 61.38% at 100MHz

Lock-in starts at ~12us for 5MHz input and ~9us for 12.5Mhz input


**40Mhz output** 
</p>

