# Infrared Communication Using Frequency Discrimination

**An Analog Electronics Project | Signal Processing | Infrared Communication**

<p align="center">
  <img src="images/project-cover.jpg" alt="Infrared Frequency Discrimination Project" width="850">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Domain-Analog%20Electronics-blue">
  <img src="https://img.shields.io/badge/Signal-Infrared-red">
  <img src="https://img.shields.io/badge/Processing-Frequency%20Discrimination-green">
  <img src="https://img.shields.io/badge/Design-KiCad-314CB6">
</p>

## 1. Project Overview

This project explores a simple infrared communication system based on **frequency discrimination**, using analog electronic circuits rather than digital decoding or microcontrollers.

The objective is to transmit different commands through an infrared optical link by assigning a distinct frequency to each command. At the receiver, the detected signal is processed by active filters to identify its frequency and activate the corresponding output indicator.

The system demonstrates how frequency-selective circuits can be used to distinguish between signals transmitted over the same communication channel.

## 2. Operating Principle

The system is divided into three main stages:

### A. Signal Generation and Transmission

Two independent op-amp-based relaxation oscillators generate signals at different frequencies.

- **Low-frequency channel:** Approximately 298.6 Hz.
- **High-frequency channel:** Approximately 12.08 kHz.

Push buttons are used to activate the corresponding oscillator. An NPN transistor drives the infrared LED, allowing the generated signal to modulate the transmitted infrared light.

### B. Infrared Reception

An infrared-sensitive photodetector receives the transmitted optical signal and converts variations in infrared intensity into an electrical signal.

The resulting electrical signal is conditioned before being sent to the filtering stage.

### C. Frequency Detection and Output

The received signal is processed using two active filters:

- **Low-pass filter (LPF):** Passes the lower-frequency component while attenuating higher-frequency signals.
- **High-pass filter (HPF):** Passes the higher-frequency component while attenuating lower-frequency signals.

Depending on the detected frequency, the corresponding output stage activates an LED indicator.

This allows two different commands to be distinguished using a single infrared transmission channel.

## 3. System Architecture

```text
              TRANSMITTER
        ┌──────────────────────┐
        │  Low-Frequency       │
        │  Oscillator (~299 Hz)│
        └──────────┬───────────┘
                   │
              Push Button
                   │
        ┌──────────┴───────────┐
        │  High-Frequency      │
        │  Oscillator (~12 kHz)│
        └──────────┬───────────┘
                   │
             Transistor Driver
                   │
              IR LED
                   │
           Infrared Optical Link
                   │
              IR Receiver
                   │
        Signal Conditioning Stage
                   │
             ┌─────┴─────┐
             │           │
         Low-Pass     High-Pass
          Filter       Filter
             │           │
         Output 1     Output 2
             │           │
          LED 1        LED 2
```

## 4. Circuit Design

The circuit is designed around the following functional blocks:

| Stage | Main components | Function |
|---|---|---|
| Oscillators | LM358, resistors, capacitors | Generate two distinct frequencies |
| Transmitter driver | NPN transistor, IR LED, base resistor | Drive the infrared emitter |
| Receiver | IR-sensitive photodetector, resistor | Convert received infrared variations into an electrical signal |
| Signal conditioning | LM358 | Buffer and condition the received signal |
| Low-pass filter | Op-amp, resistors, capacitors | Detect the lower-frequency channel |
| High-pass filter | Op-amp, resistors, capacitors | Detect the higher-frequency channel |
| Indicators | LEDs and current-limiting resistors | Display the detected command |

### Oscillator Design

The transmitter uses op-amp-based relaxation oscillators.

Their operating frequency depends on the timing capacitor and feedback resistor network.

The approximate oscillation period is:

\[
T=2RC\ln\left(\frac{1+\beta}{1-\beta}\right)
\]

where:

\[
\beta=\frac{R_2}{R_1+R_2}
\]

and:

\[
f=\frac{1}{T}
\]

The two oscillators were experimentally tested, producing the following measured frequencies:

| Channel | Measured frequency |
|---|---:|
| Channel 1 | 298.6 Hz |
| Channel 2 | 12.08 kHz |

### Active Filter Design

The receiver employs active high-pass and low-pass filtering stages.

The cutoff frequency of a first-order RC filter is:

\[
f_c=\frac{1}{2\pi RC}
\]

The cutoff frequencies must be selected to separate the two operating frequencies while providing sufficient attenuation of unwanted signals.

The use of active filters also provides the possibility of signal amplification and buffering.

## 5. Hardware Implementation

The circuits were initially assembled and tested on a breadboard.

The experimental setup includes the oscillator circuits, infrared transmitter and receiver, signal-conditioning stages, and output indicators.

The project focuses on understanding the behavior of each functional block and verifying the frequency discrimination principle through practical measurements.

## 6. Experimental Results

The oscillator frequencies were measured using a digital multimeter with frequency measurement capability.

**Measured results:**

- Low-frequency oscillator: 298.6 Hz.
- High-frequency oscillator: 12.08 kHz.

These measurements confirm that the two oscillator circuits generate distinguishable frequency signals.

The next verification stage consists of testing the complete optical transmission and reception path, followed by evaluating the selectivity and reliability of the receiver filters.

## 7. Project Documentation and Media

### 7.1 Project Concept

An overview of the communication concept and its frequency-based operating principle.

![Project concept](images/project-concept.jpg)

### 7.2 Circuit Schematic

The electronic circuit was designed and documented using KiCad.

![KiCad schematic](images/kicad-schematic.png)

**Design files:** [`hardware/`](hardware/)

### 7.3 Active Filter Design

The high-pass and low-pass filter configurations used to separate the received frequency components.

![Active filter design](images/active-filters.png)

### 7.4 Oscillator Implementation and Measurements

Breadboard implementation and experimental frequency measurements.

![Oscillator implementation](images/oscillator-experiment.jpg)

### 7.5 Infrared Transmitter and Receiver

The infrared emitter and photosensitive receiver form the optical communication interface.

![Infrared transmitter and receiver](images/infrared-interface.png)

### 7.6 Demonstration Video

A practical demonstration of the project, including signal generation, infrared transmission, reception, and output response.

[▶ Watch the project demonstration](media/demo.mp4)

## 8. Tools and Components

**Software**
- KiCad – Electronic schematic design.
- Analog circuit simulation tools (where applicable).

**Main hardware components**
- LM358 operational amplifier.
- Infrared LED.
- IR-sensitive photodetector.
- NPN bipolar junction transistor.
- Resistors and capacitors.
- Push buttons.
- Indicator LEDs.
- Breadboard and connecting wires.

## 9. Future Improvements

Several improvements could extend the functionality and performance of this prototype:

1. **Multi-frequency communication:** Introduce additional oscillator frequencies to support more commands.
2. **Band-pass filtering:** Design a dedicated band-pass filter for each communication channel to improve frequency selectivity.
3. **Filter optimization:** Investigate second-order and higher-order active filters for better attenuation outside the passband.
4. **Signal conditioning:** Improve receiver sensitivity and reduce the effects of ambient infrared interference.
5. **Performance evaluation:** Measure the maximum transmission distance, detection reliability, and response time.
6. **PCB implementation:** Develop a dedicated PCB to replace the breadboard prototype and improve circuit integration.

### Proposed Multi-Channel Architecture

The system could be extended by assigning a unique frequency to each command and using a corresponding band-pass filter at the receiver.

![Proposed band-pass filtering improvement](images/future-improvements.jpg)

## 10. Repository Structure

```text
infrared-frequency-discrimination/
│
├── README.md
│
├── images/
│   ├── project-cover.jpg
│   ├── project-concept.jpg
│   ├── kicad-schematic.png
│   ├── active-filters.png
│   ├── oscillator-experiment.jpg
│   ├── infrared-interface.png
│   └── future-improvements.jpg
│
├── hardware/
│   ├── infrared-frequency-discrimination.kicad_pro
│   ├── infrared-frequency-discrimination.kicad_sch
│   └── infrared-frequency-discrimination.kicad_pcb
│
└── media/
    └── demo.mp4
```

*Include the `.kicad_pcb` file only if a PCB layout has been designed. The schematic and project files should be included in their original KiCad formats.*

## 11. Learning Outcomes

Through this project, I explored and applied several concepts in analog electronics and instrumentation:

- Operational amplifier applications.
- Relaxation oscillator design and frequency generation.
- RC active filter design and frequency response.
- Infrared optical transmission and photodetection.
- Transistor-based LED driving.
- Analog signal conditioning.
- Practical circuit assembly, testing, and troubleshooting.

---

**Author:** Abderraouf Brada

**Field:** Micro & Nano Sensors and Instrumentation for Nanotechnology

**Project Category:** Analog Electronics and Signal Processing

---

*This project was developed as an experimental study of frequency-based infrared communication and analog signal discrimination.*
