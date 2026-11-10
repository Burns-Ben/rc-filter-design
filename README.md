# RC Filter Design and Experimental Validation

Design, simulation, construction, and experimental characterization of first-order passive RC low-pass and high-pass filters.

This project compares three representations of the same filters:

1. **Theoretical analysis in MATLAB**
2. **AC simulation in LTspice**
3. **Physical measurements using a breadboard and PC audio interface**

The goal was to determine how closely measured frequency responses matched ideal first-order RC filter behavior.

---

## Design

Both filters use nominal component values of:

- **Resistance:** 1.5 kΩ
- **Capacitance:** 0.1 µF (100 nF)

The theoretical cutoff frequency is

```math
f_c=\frac{1}{2\pi RC}
```

which gives

```math
f_c \approx 1.061\ \text{kHz}
```

The low-pass filter measures the output across the capacitor, while the high-pass filter measures the output across the resistor.

---

## Theoretical Analysis

MATLAB was used to calculate the ideal magnitude responses over 20 Hz–10 kHz.

For the low-pass filter,

```math
|H_{LP}(f)|=\frac{1}{\sqrt{1+(2\pi fRC)^2}}
```

For the high-pass filter,

```math
|H_{HP}(f)|=
\frac{2\pi fRC}{\sqrt{1+(2\pi fRC)^2}}
```

Gain was converted to decibels using

```math
G_{dB}=20\log_{10}|H(f)|
```

At the cutoff frequency, both filters ideally have a gain of approximately **−3.01 dB**.

---

## LTspice Simulation

Both circuits were simulated with an AC sweep from **20 Hz to 10 kHz**.

The simulations verified the expected first-order responses:

- The low-pass filter approaches 0 dB at low frequencies and rolls off above the cutoff frequency.
- The high-pass filter is strongly attenuated at low frequencies and approaches 0 dB at high frequencies.
- Both filters reach approximately −3 dB at the cutoff frequency.
- Low-pass phase approaches −90° as frequency increases.
- High-pass phase approaches +90° at low frequencies and approaches 0° as frequency increases.

---

## Experimental Setup

The filters were constructed on a solderless breadboard.

MATLAB generated sinusoidal test signals at:

`100, 250, 500, 1061, 2000, 5000, and 10000 Hz`

The signals were sent through the **motherboard-integrated Realtek audio output of an Alienware Aurora R7**.

The filtered signal was returned through the computer's **Realtek Line In** connection and recorded in MATLAB.

A direct audio loopback measurement was taken to establish a reference amplitude. RMS amplitudes were then used to calculate the experimental gain:

```math
G_{\text{measured}}
=
20\log_{10}
\left(
\frac{V_{\text{out,RMS}}}
{V_{\text{in,RMS}}}
\right)
```

---

## Measured Components

The physical components were measured with a **CEN-TECH CM300 digital multimeter**.

| Component | Nominal | Measured |
|---|---:|---:|
| Resistor | 1500 Ω | 1475 Ω |
| Capacitor | 100 nF | 100.3 nF |

Using the measured component values,

```math
f_c=
\frac{1}
{2\pi R_{\text{measured}}C_{\text{measured}}}
\approx 1.076\ \text{kHz}
```

The small shift from the nominal 1.061 kHz cutoff indicates that component tolerance alone does not explain all of the observed measurement error.

---

## Experimental Results

At the nominal cutoff frequency of **1061 Hz**:

| Filter | Theoretical Gain | Measured Gain |
|---|---:|---:|
| Low-Pass | −3.01 dB | −3.665 dB |
| High-Pass | −3.01 dB | −3.773 dB |

Across the full test range, both experimental curves closely followed the expected first-order filter behavior.

The remaining differences between theory and experiment are likely associated with the complete measurement system, including source and input impedances, motherboard audio-interface characteristics, breadboard connections, and normal measurement uncertainty.

---

## Tools and Equipment

- MATLAB
- LTspice
- Alienware Aurora R7 integrated Realtek audio interface
- CEN-TECH CM300 digital multimeter
- Solderless breadboard
- 1.5 kΩ resistor
- 100 nF ceramic capacitor
- 3.5 mm audio cables
- Solid-core jumper wire

---

## Repository Contents

```text
rc-filter-design/
├── README.md
├── RC_Filter_IEEE_Report.pdf
├── Filter_Project.mlx
├── LTspice/
│   └── HiLoFilt.asc
└── Images/
    ├── low-pass.jpg
    ├── high-pass.jpg
    ├── reference.jpg
    ├── resistor-measurement.jpg
    └── capacitor-measurement.jpg
```

---

## Key Takeaways

This project provided practical experience with:

- First-order passive filter design
- Frequency-response analysis
- MATLAB numerical modeling and automated measurements
- LTspice AC simulation
- Breadboard circuit construction and troubleshooting
- RMS signal measurement
- Theory-versus-experiment comparison
- Component tolerance and measurement-system error analysis

An initial wiring error also provided a useful troubleshooting exercise: the output measurement was first taken from the grounded side of the capacitor, producing only noise. Moving the measurement point to the resistor-capacitor junction restored the expected response near cutoff.

---

## Project Report

A full IEEE-format report containing circuit schematics, LTspice simulations, experimental plots, breadboard photographs, DMM measurements, and error analysis is included in this repository.
