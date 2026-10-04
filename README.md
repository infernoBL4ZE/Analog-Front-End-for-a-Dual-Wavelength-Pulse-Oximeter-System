# Analog-Front-End-for-a-Dual-Wavelength-Pulse-Oximeter-System

This is only a showcase for my project of EEE 208(S) course.

Technical and mathematical details are noted down in https://docs.google.com/document/d/1iTzqDZH3-dw8jsMqOaMcd4MN_Oo6L-XcHi8vIYs_f2k/edit?usp=sharing

The project begins by modelling Photodiode signal as a current source using a PWL file for the project. A simple unity gain transimpedance amplifier is used for current to voltage conversion.



A significant part of my project was filter comparison. For this, I compared only first order Bandpass Filter, Second order (or Fourth Order depending on how you define) Butterworth, Bessel and Chebyshev filters. Comparing even higher order filters was in my plans, but time limitation didn't allow the implementation. The filters were compared based on a few parameters, namely Filtered Waveform Comparison, Magnitude response, Phase response and Group Delay. All filters were normalized to unity gain and cutoff frequencies at 0.5 and 5 Hz for a direct and fair comparison. Comparing all the parameters gave Bessel Filter a better choice for the project.

The DC Low Pass Filter was designed to have 0.2 Hz cutoff frequency. This design choice was done based on trial and error as I had to find a proper compromise between keeping the DC baseline centered and also to not bleed into the AC frequencies while tracking the DC shift properly.

The AGC segment after the AC filter utilizes a pre amp stage followed by a JFET which acts as a voltage controlled variable resistor. A significant challenge in implementing the circuit is to configure the JFET in a way that keeps it operational in its linear region for most of our use case. The feedback loop consists of an active peak detector and error integrator circuit to drive the JFET gate voltage accordingly and get the output from the Drain.



This AGC stage was crucial for the next stage which is heart rate measurement. This ensures that the Schmitt trigger circuit used for this stage has a good headroom to operate and can work well with a good range of input voltage. The entire system uses +15 and -15V supply rails for the op amps, although simple design modifications can use lower ones



Two identical channels are used for Red and IR wavelengths of light.



Note that this is not the complete model for the Pulse Oximeter as it doesn't include the digital processing part. But as the bulk of workload is done using the AFE, the digital processing becomes relatively simple to implement.
