# BogDAC - A no frills DAC board for ES9039Q2M

## Introduction
I like to keep things simple. Reading about people "improving" their DACs with femtosecond-precision clocks, re-clockers, hundreds of farads of capacitance and potting soil (yes, potting soil), I decided I wanted to create a bog standard
DAC board based on the ES9039Q2M chip. I wanted a small board that would just accept an I2S stream and I2C commands and output single-ended audio. 

## Design Overview
This is following my Bog Standard concept: Keep things simple, follow best practices and avoid audiophile fads. The chip is locked into software mode and asynchronous I2S (a.k.a. PCM) operations using a local 49.152MHz oscillator. This 
allows for a design with a very simple and short clock signal path and should (at least in my opinion) perform better than external clocks connected through wires. The output section is pretty much just the one suggested in the data sheet and
based on OPA1612. The +/- 12V power for the analog section is provided by a TPS7A39 regulator. The 3.3V power for the analog reference voltages and the digital power is fed by a LT3046 regulator. The L3046 can be fed either from a separate 5V
power input or from the 12V rail by installing a jumper. Please note that nothing should be plugged into the 5V inlet if the jumper is installed.

## Schematic
![Digital schematic](images/digital-schematic.png)
![Analog schematic](images/analog-schematic.png)

## Test results
I tested this using a QA403. While this is a superb piece of gear, it has its limitations compared to test equipment that costs 100 times more. Because of this, the lower bound of the THD I can measure is about 0.0001% and the lowest noise 
floor is just above -150dBV. In fact, the harmonic profile of a loopback measurement looks very similar to the results I'm getting, so my hypothesis is that almost all noise and distortion you see comes from the measurement setup and 
not the circuit.

A 1kHz tone at full volume yields this spectrum. The THD is about 0.00013# and the SNR sits at about 113dB. I think the actual numbers are a lot better. Anyone who wants to lend me a $50,000 audio analyzer? :)
<img width="2029" height="1195" alt="image" src="https://github.com/user-attachments/assets/56b832c0-4f5a-437d-980b-7304836360bf" />

Another interesting measurement is looking at the idle noise. This is the DAC fully enabled, but without an input signal. I'm running the board on a cheap lab supply. As you can see, there's virtually no hum and very low noise.
You can thank those fancy regulators for that! 
<img width="2024" height="1190" alt="image" src="https://github.com/user-attachments/assets/ccf800aa-48ae-4baa-9dec-7bb86ec4c20a" />



