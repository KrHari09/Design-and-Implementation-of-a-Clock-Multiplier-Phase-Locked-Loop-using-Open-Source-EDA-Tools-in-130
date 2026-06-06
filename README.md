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
