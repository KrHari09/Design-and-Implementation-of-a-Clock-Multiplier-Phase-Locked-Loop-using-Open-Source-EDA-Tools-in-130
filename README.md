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

---
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

  **Expected output:-** </p>
<img width="1176" height="517" alt="Output_expected" src="https://github.com/user-attachments/assets/c8b0192d-fd47-4aad-a198-e86e8d9e94e5" />


**Simulated output:-** </p>

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

<img width="1701" height="872" alt="40MHz output" src="https://github.com/user-attachments/assets/723bf586-9443-4efd-b5f6-ee5e078f8c7b" />

</p>

**100Mhz output**
</p>

<img width="1695" height="865" alt="100MHz output" src="https://github.com/user-attachments/assets/40bec40c-ef44-4f40-87fc-b2ef853444e9" />


</p>

**Close up for 100Mhz** </p>
<img width="1697" height="871" alt="Close_up_100Mhz Output" src="https://github.com/user-attachments/assets/137c5401-9979-45d8-954d-decc6db1f442" />

**Red signal constantly overlaps blue signal indicating locked state.** </p>

**Pre-layout summary** </p>

| Input Frequency | Output Frequency |
| :---:  | :-: |
|5MHz|40.98MHz|
|9MHz|71.42MHz|
|10MHz|80.97MHz|
|12.5MHz|100MHz|

## Post layout circuits

### a. Phase Frequency Detector
<img width="937" height="735" alt="PFD" src="https://github.com/user-attachments/assets/b331c087-5847-4048-9c6e-065479801a5b" />

</p>
Fig: Layout of Phase Frequency Detector (PFD)
</p>

### b. Voltage controlled oscillator

<img width="1383" height="350" alt="VCO" src="https://github.com/user-attachments/assets/fa13f125-511e-401b-b8d2-dbeaeb14d8fd" />


</p>
Fig: Layout of Voltage controlled oscillator (VCO)
</p>

### c. Charge pump & loop filter

<img width="780" height="596" alt="CPL Filter" src="https://github.com/user-attachments/assets/3b4bd05c-2863-4f84-a314-75a3c8eca4d1" />

</p>
Fig. - Combined layout of charge pump and loop filter (large boxes are the capacitors of the loop filter)
</p>

### Charge pump close up

<img width="1078" height="717" alt="CP Close_up" src="https://github.com/user-attachments/assets/125facb7-0820-49b1-b3b1-6ff30e7ec63c" />

### d. Frequency divider 

<img width="1293" height="721" alt="Freq_divider" src="https://github.com/user-attachments/assets/cd80d098-9a88-4a2d-81ef-006eb60a96e5" />

</p>
Fig: Layout of Frequency divider by 8 circuit
</p>

The frequency divider by 8 is made from cascading three frequency divider by 2 circuits. The fd/2 ckt layout is shown below <br>

<img width="1386" height="750" alt="fd2 ckt layout" src="https://github.com/user-attachments/assets/f8e65269-aca2-4216-b84d-84dbd5060981" />

### d. Integrated PLL layout  

<img width="923" height="721" alt="integradted pll ayout" src="https://github.com/user-attachments/assets/65213573-eec9-4d5f-b2fa-cb6c8e7a669e" />

<br>

circuit area = 0.2641 mm2

</p> PLL Layout closeup </p>

<img width="1366" height="402" alt="PLL Close_up" src="https://github.com/user-attachments/assets/e61ccfc0-b259-4e26-a305-39e3bbd6824b" />

## Post layout simulations

| Parameter | Description | min | val | max | Unit | Conditions |
| --- | --- | --- | --- | --- | --- | --- |
| VDD | Digital Supply | - | 1.8 | - | V | T = 27C |
| F<sub>CLKREF</sub> | Reference | 5 | 9 | 12.5 | MHz | T = 27C |
| F<sub>CLKOUT</sub> | Output Clock | 40.76 | 73.26 | 100 | MHz | PLL Mode, T = 27C |
| V<sub>ctrl</sub> | Control Voltage | 0.732 | 0.780 | 0.789 | MHz | PLL Mode, T = 27C |
| DC | Duty Cycle | 56.82 | 58.82 | 60.27 | % | T = 27C | 
| T<sub>SET</sub> | Settling Time | ~8.6 | ~5.1 | ~6.4 | us | T = 27C |


### 1. 5 Mhz input 

<img width="1706" height="867" alt="5M Hz" src="https://github.com/user-attachments/assets/83e613f2-f017-4321-946b-034ba03ea0c5" />


</p>

**Fig - PLL simulation for 5Mhz input frequency**
</p>

Red - input signal <br>
Blue (on red signal) - feedback signal <br>
Yellow - up signal <br>
Green - down signal <br>
Pink - control voltage <br>
Brown - output signal <br>

 <br>

 <img width="1341" height="430" alt="5MHz io" src="https://github.com/user-attachments/assets/467df42d-37ea-42b9-ac8b-eb816d31b2e3" />

</p>

**Fig - input - output for 5 Mhz operation**
</p>

 <br>

 <img width="1707" height="872" alt="5MHz close up" src="https://github.com/user-attachments/assets/da4c2225-e5a6-483a-8bf8-494915247462" />

</p>

**Fig - settled output for 5 Mhz operation**
</p>
 <br>

 ### 2. 9 Mhz input 

<img width="1692" height="865" alt="9Mhz" src="https://github.com/user-attachments/assets/b3a6caf4-2abe-4fb0-985d-e7a8abef50b0" />

</p>

**Fig - PLL simulation for 9Mhz input frequency**
</p>
 <br>

 <img width="1197" height="428" alt="9MHz io" src="https://github.com/user-attachments/assets/0fc9a15d-26fe-4903-851f-6def9bca3757" />


</p>

**Fig - input-output for 9mhz operation**
</p>
 <br>

<img width="1717" height="511" alt="9MHz close up" src="https://github.com/user-attachments/assets/261d143e-a70e-4e35-908b-187fdde34fae" />

</p>

**Fig - settled output for 9mhz operation**
</p>
 <br>
 
### 2. 12.5 Mhz input 

<img width="1697" height="885" alt="12 5 MHz" src="https://github.com/user-attachments/assets/84f08b18-6bd5-4268-a4b3-0e48fdc5ae0b" />


**Fig - PLL simulation for 12.5Mhz input frequency**
</p>
 <br>
 
<img width="1567" height="526" alt="12 5MHz io" src="https://github.com/user-attachments/assets/ee090ad8-b633-4b35-af0e-dfb5f8fc7109" />

</p>

**Fig - input-output for 12.5mhz operation**
</p>
 <br>

<img width="1717" height="511" alt="12 5MHz close up" src="https://github.com/user-attachments/assets/0a7cdaef-c3f3-4b35-8f04-ab37cb108c79" />

</p>

**Fig - settled output for 12.5 Mhz operation**
</p>
 <br>

## To use this repository

1.	Clone the github repository in your ubuntu system
2.	Go to the mag folder in the postlayout directory and open terminal in the folder
3.	Type ‘ngspice pll_tb.spice’
4.	Paste the following command after simulation is complete

 ```bash
  plot V(f_clk_in)+8 V(x1.pfd_lay_0/f_vco)+8 V(x1.cp_0/up)+6 V(x1.cp_0/down)+4 V(x1.cp_0/vctrl)+2 V(f_clk_out)
```

 This will show the plots mentioned in the post layout section of this github repository <br>

**To see the layout**

1. Type in folder terminal window <br>


   ```bash
	magic pll.mag 
   ```


2. The layout will be hollow when the magic tool is opened for the first time. To see the layout clearly. Open the magic terminal (opens with the magic tool) and type

    ```bash
     % select top cell
     % expand
    ```

**NOTE** : all the above steps are valid for a system which has ngspice and magic (sky130nm integrated) installed. The same can be installed from [here](https://www.youtube.com/watch?v=VCuyO7Chvc8&t=2405s&ab_channel=whyRD) 


<h3> References </h3>
<b>[1]</b> Paras Gidd, avsdpll_3v3 github repository <br> <br> 
<b>[2]</b> Sun, Qingbo et al. “On-chip Phase Locked Loop (PLL) design for clock multiplier in CMOS Monolithic Active Pixel Sensors (MAPS).” (2009). <br> <br> 
<b>[3]</b> Vincent Von Kaenel, “A 320 MHz, 1.5 mW @ 1.35 V CMOS PLL for Microprocessor Clock Generation” (1996) <br> <br> 
<b>[4]</b> J. Dhurga Devi “Jitter Reduced Self Biased PLLs—A Systematic Simulation Study”
<b>[5]</b> Jitter and Phase Noise in Ring Oscillators, Ali Hajimiri, Sotirios Limotyrakis, and Thomas H. Lee <br> <br> 
<b>[6]</b> Mo Zhang, A Programmable Frequency Divider Having a Wide Division Ratio, and Close-to-50% Output Duty-Cycle  <br> <br> 
<b>[7]</b> George Tom Varghese, MS thesis on “Phase Locked Loop Design as a Frequency Multiplier” NIT Rourkela (2009) <br> <br> 
<b>[8]</b> Yang Liu, “Phase Noise in CMOS Phase-Locked Loop Circuits” (2011) <br> <br> 
<b>[9]</b>	Rushabh Mehta, Design and implementation of a phase locked loop for high-speed serial links <br> <br> 
<b>[10]</b> Shruti Suman, An Improved Performance Ring VCO: Analysis and Design (2018)  <br> <br> 
<b>[11]</b> Scott Buchanan, Phase Locked Loop Integrated Circuit (2015)  <br> <br> 


<h3> Acknowledgements </h3>

- I thank Mr. Kunal Ghosh, co-founder [VSD](https://www.vlsisystemdesign.com/), for helping me through out the project, I would like to thank my college professors Dr. Chandradeep Singh and Dr. Kunal Singh for encouraging me initiate this project and helping me with conceptual doubts.
- I thank Stephan Scrippers, David Mitchell Bailey, Luis Henrique Rodovalho, Tim Edwards and Lucas Daudt Franck from the [sky130 Slack channel](https://join.slack.com/t/open-source-silicon/shared_invite/zt-2eg56th1v-2SkdbmD6cGr9EbAFCJgIXw) for helping me with the doubts in xschem and skywater pdk.
- Rajdeep Mazumder, who's [VLSI Project help video](https://www.youtube.com/watch?v=VCuyO7Chvc8&t=2405s&ab_channel=whyRD) helped me install the open source tools
- I would also thank Paras Gidd, who's PLL repository was a reference for this project.


<h3> Contact Information</h3>

Hari Kumar(Author)- B.Tech ECE NIT Jamshedpur - harikumaroct2001@gmail.com

