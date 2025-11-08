# M-Array Frequency Shift Keying (MFSK): Comprehensive Analytical Presentation

---

## Slide 1: Title Slide
**M-Array Frequency Shift Keying (MFSK)**
- Subtitle: Mathematical Analysis, Signal Representation, Performance Standards & Applications
- Standard References: IEEE 802.11, ITU-R Recommendations
- Date: November 2025

---

## Slide 2: Introduction & Definition

**MFSK Definition:**
M-Array Frequency Shift Keying (MFSK) is a digital modulation scheme where M distinct frequencies represent M different symbols, each carrying log₂(M) bits of information per symbol transmission.

**Key Characteristics:**
- Modulation Order: M (where M = 2^k, k = number of bits per symbol)
- Multiplicity: M orthogonal frequencies
- Bits per Symbol: k = log₂(M)
- Symbol Rate: Rs = R_b / k (where R_b is bit rate)
- Detection: Non-coherent or coherent demodulation

**Comparison with FSK:**
- Binary FSK (2-FSK): Uses 2 frequencies, 1 bit per symbol
- MFSK: Uses M ≥ 2 frequencies, log₂(M) bits per symbol
- Advantage: Higher spectral data rate

---

## Slide 3: Mathematical Representation - MFSK Signal Model

**General MFSK Signal Expression:**

The transmitted MFSK signal for symbol s_m (where m = 0, 1, ..., M-1) is:

\( s_m(t) = \sqrt{\frac{2E_s}{T_s}} \cos(2\pi f_m t + \phi_0) \)

where:
- E_s = Symbol energy (Joules)
- T_s = Symbol duration (seconds)
- f_m = m-th center frequency (Hz)
- φ₀ = Initial phase offset (radians)
- m = 0, 1, 2, ..., M-1

**Time Domain Definition:**

\( s_m(t) = \begin{cases}
\sqrt{\frac{2E_s}{T_s}} \cos(2\pi f_m t + \phi_0) & \text{for } 0 \leq t \leq T_s \\
0 & \text{otherwise}
\end{cases} \)

**Energy Per Bit:**
\( E_b = \frac{E_s}{\log_2(M)} = \frac{E_s}{k} \)

---

## Slide 4: Frequency Assignment & Orthogonality

**Frequency Spacing Criterion:**

For orthogonal MFSK, the frequencies must be spaced such that:

\( \Delta f = \frac{1}{T_s} \)

This ensures minimum frequency spacing between adjacent channels.

**Orthogonality Condition:**

Two signals s_i(t) and s_j(t) are orthogonal if:

\( \int_0^{T_s} s_i(t) s_j(t) dt = \begin{cases}
E_s & \text{if } i = j \\
0 & \text{if } i \neq j
\end{cases} \)

**Frequency Set Definition:**

\( f_m = f_0 + m \cdot \Delta f = f_0 + \frac{m}{T_s} \)

where:
- f₀ = Minimum (carrier) frequency (Hz)
- m = 0, 1, 2, ..., M-1
- Δf = 1/T_s = Frequency spacing (Hz)

**Cross-Correlation Matrix:**

For orthogonal signals: ρ_ij = ⟨s_i, s_j⟩/E_s = δ_ij (Kronecker delta)

---

## Slide 5: Bandwidth Requirements & Spectral Analysis

**Occupied Bandwidth (Carson's Rule Approximation):**

\( B_w \approx (M-1) \cdot \Delta f + 2 \cdot B_m \)

For FSK with rectangular pulses:

\( B_w = M \cdot \Delta f = \frac{M}{T_s} = M \cdot R_s \)

where R_s = 1/T_s = Symbol rate (baud/s)

**Spectral Efficiency (bits/s/Hz):**

\( \eta = \frac{R_b}{B_w} = \frac{\log_2(M)}{M \cdot R_s} \cdot \frac{R_s}{1} = \frac{\log_2(M)}{M} \text{ bits/s/Hz} \)

**Spectral Efficiency Examples:**

| M | k (bits/symbol) | η (bits/s/Hz) |
|---|---|---|
| 2 (2-FSK) | 1 | 0.500 |
| 4 (4-FSK) | 2 | 0.500 |
| 8 (8-FSK) | 3 | 0.375 |
| 16 (16-FSK) | 4 | 0.250 |
| 32 (32-FSK) | 5 | 0.156 |
| 64 (64-FSK) | 6 | 0.094 |

**Key Observation:** Spectral efficiency decreases as M increases, making MFSK less bandwidth efficient for large M values.

---

## Slide 6: Modulation Index & Deviation Ratio

**Frequency Deviation:**

\( \Delta f_d = \frac{f_{max} - f_{min}}{2} = \frac{(M-1) \Delta f}{2} \)

**Modulation Index (h):**

\( h = \frac{\Delta f_d}{R_s} = \frac{\Delta f_d \cdot T_s}{1} \)

For orthogonal MFSK with Δf = 1/T_s:

\( h = \frac{1}{2} \)

**Carson's Bandwidth with Modulation Index:**

\( B_w = 2(\Delta f_d + R_s) = 2 \Delta f_d (1 + \frac{1}{h}) \)

---

## Slide 7: MFSK Signal Constellation

**Example: 4-MFSK (M=4) Constellation**

Bit Patterns and Frequency Mapping:
| Bits | Symbol | Frequency | f_m (Hz) |
|---|---|---|---|
| 00 | 0 | f₀ | f₀ + 0/T_s |
| 01 | 1 | f₀ + Δf | f₀ + 1/T_s |
| 10 | 2 | f₀ + 2Δf | f₀ + 2/T_s |
| 11 | 3 | f₀ + 3Δf | f₀ + 3/T_s |

**Constellation Representation:**

In the frequency domain, MFSK symbols are represented as impulses at frequencies f_m with magnitude √(2E_s/T_s).

---

## Slide 8: Modulation Process (Transmitter)

**Steps:**

1. **Bit Grouping:** Group incoming bits into k-bit symbols
   - k = log₂(M)

2. **Symbol Mapping:** Map each k-bit group to a symbol index (0 to M-1)

3. **Frequency Assignment:** Assign frequency f_m = f₀ + m/T_s to symbol m

4. **Signal Generation:** Generate sinusoidal waveform at selected frequency

5. **Transmission:** Transmit signal for duration T_s, then repeat

**Mathematical Expression of Transmitter Output:**

\( x(t) = \sum_{i} s_{m_i}(t - i \cdot T_s) \)

where m_i is the symbol index at the i-th interval.

---

## Slide 9: Demodulation & Reception (Receiver)

**Coherent Demodulation (Optimal - Maximum Likelihood):**

1. **Matched Filtering:** Correlate received signal with each reference signal

\( r_m = \int_0^{T_s} r(t) \cdot s_m(t) dt \)

2. **Energy Calculation:** Compute energy in each frequency bin

\( E_m = |r_m|^2 \)

3. **Maximum Likelihood Decision:** Select symbol with maximum energy

\( \hat{m} = \arg \max_m |r_m|^2 \)

**Non-Coherent Demodulation (Practical):**

Uses envelope detection with frequency shift keying without requiring phase synchronization:

\( \hat{m} = \arg \max_m \left| \int_0^{T_s} r(t) e^{-j 2\pi f_m t} dt \right| \)

---

## Slide 10: Performance Analysis - Probability of Error

**Symbol Error Probability (SEP) in AWGN Channel:**

For orthogonal MFSK with coherent non-coherent detection:

\( P_e = (M-1) Q\left(\sqrt{\frac{2E_s}{N_0}}\right) \)

where Q(x) is the Gaussian Q-function: \( Q(x) = \frac{1}{\sqrt{2\pi}} \int_x^{\infty} e^{-t^2/2} dt \)

**Bit Error Probability (BEP):**

Assuming Gray coding:

\( P_b \approx \frac{1}{\log_2(M)} \cdot P_e \)

**Asymptotic Performance (High SNR):**

\( P_e \approx (M-1) e^{-E_s/N_0} \)

**SNR Required for BER = 10⁻⁵:**

| M | E_b/N_0 (dB) |
|---|---|
| 2 | 9.6 |
| 4 | 9.7 |
| 8 | 10.0 |
| 16 | 10.6 |
| 32 | 11.5 |

---

## Slide 11: Performance in Fading Channels

**Rayleigh Fading Channel Model:**

The received signal in Rayleigh fading:

\( r(t) = h(t) \cdot s_m(t) + n(t) \)

where h(t) is the random channel gain: |h|² ~ χ²₂

**Symbol Error Probability in Rayleigh Fading:**

\( P_e = (M-1) \int_0^{\infty} Q\left(\sqrt{2|h|^2 \cdot E_s/N_0}\right) p(|h|^2) d|h|^2 \)

Simplified form:

\( P_e = (M-1) \left( 1 - \sqrt{\frac{\gamma_s}{2 + \gamma_s}} \right) \)

where γ_s = average symbol SNR = E_s/(2σ²) and σ² is noise variance

**Comparison: AWGN vs Rayleigh Fading**

At BER = 10⁻³:
- AWGN: SNR ≈ 6-7 dB
- Rayleigh Fading: SNR ≈ 18-25 dB (depending on M)

**Diversity Techniques:**

Maximal Ratio Combining (MRC) with L antennas:

\( P_e = (M-1) \prod_{i=0}^{L-1} \left(1 - \sqrt{\frac{\gamma_i}{2+\gamma_i}}\right) \)

---

## Slide 12: Noise and Interference Performance

**Signal-to-Noise Ratio (SNR) Definition:**

\( \text{SNR} = \frac{E_s}{N_0} = \frac{\text{Signal Power}}{\text{Noise Power}} \)

**Eb/N0 Relationship:**

\( E_b/N_0 = \frac{E_s}{\log_2(M) \cdot N_0} \)

**Noise Figure (NF):**

\( \text{NF} = 10 \log_{10}\left(\frac{\text{SNR}_{in}}{\text{SNR}_{out}}\right) \text{ (dB)} \)

**SINR (Signal-to-Interference-plus-Noise Ratio):**

In multi-user scenarios:

\( \text{SINR} = \frac{P_s}{P_i + P_n} \)

where P_s = signal power, P_i = interference power, P_n = noise power

---

## Slide 13: Bandwidth Efficiency Tradeoff

**Fundamental Tradeoff:**

\( B_w = \frac{M \cdot R_b}{\log_2(M)} \)

**Analysis:**

- As M increases: Bits per symbol increases, but required bandwidth increases faster
- Optimal M depends on available bandwidth and noise immunity requirements
- Spectral efficiency η = log₂(M)/M has maximum at M = e ≈ 2.718

**Power Efficiency vs Bandwidth Efficiency:**

| Parameter | Small M | Large M |
|---|---|---|
| Bandwidth Efficiency | Low | Lower |
| Power Efficiency | Good | Better |
| Complexity | Low | High |
| Robustness to Noise | Better | Worse |

---

## Slide 14: Modulation Standards & Specifications

**IEEE Standards Employing MFSK:**

| Standard | Application | M | Bit Rate |
|---|---|---|---|
| IEEE 802.11 (WiFi) | Wireless LAN | 2-4 | 1-2 Mbps |
| IEEE 802.15.4 | Zigbee | 16 | 250 kbps |
| ISM Band | Amateur Radio | 2-16 | 1.2-9.6 kbps |

**ITU-R Recommendations:**

- ITU-R F.1495: Testing digital radio systems for fading channels
- ITU-R M.1531: Field-strength measurements for wireless systems
- ITU-R RS.1546: Propagation prediction methods

**Frequency Band Allocations:**

- VHF: 30-300 MHz (typical for MFSK applications)
- UHF: 300 MHz - 3 GHz
- ISM Bands: 2.4 GHz (unlicensed), 915 MHz (US), 868 MHz (Europe)

---

## Slide 15: Practical Implementation Considerations

**Transmitter Design:**

1. Digital signal processor (DSP) generates baseband signals
2. Numerically controlled oscillator (NCO) generates carrier frequencies
3. Power amplifier boosts signal to transmission level
4. Antenna radiates signal

**Critical Parameters:**

- Frequency accuracy: ±ppm tolerance
- Phase synchronization: Critical for coherent detection
- Symbol timing: Recovered using clock recovery circuits
- Frequency stability: Temperature and aging compensation

**Receiver Design:**

1. Antenna reception
2. Low-noise amplifier (LNA) for signal enhancement
3. Frequency conversion (mixing) to baseband
4. Analog-to-digital converter (ADC) at Nyquist rate
5. Digital matched filter bank (one filter per frequency)
6. Maximum likelihood detector

**Nyquist Sampling Rate:**

\( f_s \geq 2 \cdot (f_0 + \frac{M}{2T_s}) \)

---

## Slide 16: Advantages of MFSK

1. **High Data Rate:** Can transmit log₂(M) bits per symbol
2. **Noise Immunity:** Orthogonal frequencies provide excellent SNR performance
3. **Non-Coherent Detection:** Simplified receiver in non-coherent mode
4. **Frequency Diversity:** Different frequencies reduce fading effects
5. **Robust to Phase Noise:** Less sensitive than PSK to phase instability
6. **Low Crest Factor:** Single-tone transmission (lower than OFDM)
7. **Inherent Averaging:** Multiple frequencies provide inherent averaging

---

## Slide 17: Disadvantages of MFSK

1. **Bandwidth Expansion:** Requires M times the bandwidth of binary FSK
2. **Low Spectral Efficiency:** η = log₂(M)/M → decreases with M
3. **Increased Complexity:** Receiver requires M matched filters
4. **Frequency Synchronization:** Requires precise frequency alignment
5. **Larger Constellation:** More symbols increase error susceptibility in high-noise conditions
6. **Poor Bandwidth-Power Tradeoff:** Cannot achieve Shannon limit as efficiently as QAM
7. **Not Optimal for Large M:** Spectral efficiency degrades significantly

---

## Slide 18: Comparison with Other Modulation Schemes

| Characteristic | MFSK | PSK | QAM | OFDM |
|---|---|---|---|---|
| Spectral Efficiency | Low-Moderate | High | Very High | High |
| Bandwidth Requirement | Wide | Narrow | Narrow | Moderate |
| Power Efficiency | Good | Moderate | Poor | Moderate |
| Noise Immunity | Excellent | Good | Moderate | Moderate |
| Complexity | Moderate | Moderate | High | Very High |
| Frequency Sync Required | Yes | Moderate | Yes | Yes |
| Phase Synchronization | No (non-coherent) | Yes | Yes | Yes |
| Crest Factor | Low (1.0) | Moderate (1.4) | High (3.0+) | Very High (10+) |

---

## Slide 19: Applications of MFSK

**1. Amateur Radio & Packet Radio:**
- AFSK (Audio Frequency Shift Keying) over VHF/UHF
- Popular for packet radio networks
- Typical: 1200 bps or 9600 bps

**2. Underwater Acoustic Communication:**
- Water absorbs RF signals; acoustics essential
- MFSK robust to multipath in underwater channels
- Extended range communication

**3. Military Communication:**
- Frequency hopping spread spectrum (FHSS) often uses MFSK
- Jam-resistant properties
- Secure communication channels

**4. Wireless Sensor Networks:**
- Zigbee (IEEE 802.15.4): 16-ary FSK at 2.4 GHz
- Low power consumption suitable for IoT
- Reliable in industrial environments

**5. Satellite Communication:**
- Non-coherent MFSK for satellite downlinks
- Phase tracking difficult at long distances
- Frequency diversity compensation

**6. Narrowband Digital Radio:**
- Licensed and unlicensed ISM bands
- Data modem applications
- 1.2-9.6 kbps typical rates

**7. Radio Astronomy:**
- Detection of weak signals from space
- Multiple frequencies for signal verification
- Non-coherent detection reduces tracking complexity

---

## Slide 20: MFSK vs Binary FSK Detailed Comparison

**Capacity & Data Rate:**

Binary FSK (2-FSK):
- Bits per symbol: 1
- Bandwidth: B_w = 2 · Δf
- Data rate: R_b = R_s (symbol rate = bit rate)

MFSK (M-ary):
- Bits per symbol: k = log₂(M)
- Bandwidth: B_w = M · Δf
- Data rate: R_b = k · R_s

**Spectral Efficiency Improvement:**

Factor improvement: \( \frac{\eta_{MFSK}}{\eta_{2-FSK}} = \frac{\log_2(M)/M}{1/2} = \frac{2 \log_2(M)}{M} \)

Example: For 8-FSK vs 2-FSK:
\( \text{Ratio} = \frac{2 \times 3}{8} = 0.75 \) (75% of binary FSK efficiency)

---

## Slide 21: Design Example: 16-MFSK System

**System Parameters:**

| Parameter | Value | Unit |
|---|---|---|
| Modulation Order (M) | 16 | symbols |
| Bits per Symbol (k) | 4 | bits/symbol |
| Bit Rate (R_b) | 9600 | bps |
| Symbol Rate (R_s) | 2400 | baud |
| Symbol Duration (T_s) | 416.7 | μs |
| Carrier Frequency (f_0) | 1700 | Hz |
| Frequency Spacing (Δf) | 2400 | Hz |
| Bandwidth | 38.4 | kHz |
| Spectral Efficiency | 0.250 | bits/s/Hz |

**Frequency Assignment:**

\( f_m = 1700 + 2400 \cdot m \text{ Hz, where } m = 0, 1, ..., 15 \)

Frequencies range: 1700 Hz to 37,700 Hz

**Symbol Energy Calculation:**

For SNR = 10 dB (E_s/N_0 = 10):
- E_b/N_0 = 10 - 10log₁₀(4) = 10 - 6.02 = 3.98 dB
- E_s/N_0 = 10 dB
- N_0 = 1 (normalized)
- E_s = 10 Joules/symbol

**Error Probability:**

P_e ≈ 15 · Q(√(2 × 10)) ≈ 15 · Q(4.47) ≈ 15 × 3.8×10⁻⁶ ≈ 5.7×10⁻⁵

---

## Slide 22: Implementation Example: Software Defined Radio (SDR)

**Typical MFSK SDR Architecture:**

```
Input Bits → Symbol Mapper → NCO Bank → Multiplexer → DAC → RF Frontend → Antenna
                     ↓
            Digital Signal Processor
```

**DSP Operations:**

1. **Bit Grouping:** Convert serial input to parallel k-bit symbols
2. **Symbol Mapping:** Create lookup table for frequency indices
3. **NCO Generation:** Generate sinusoids at f_m frequencies
4. **Windowing:** Apply Hann window to reduce spectral splatter
5. **Interpolation:** Upsample to DAC sampling rate

**Python-Like Pseudocode:**

```python
# Symbol modulation
M = 16
bits_per_symbol = 4
symbols = [] # Array of M-bit groups
frequencies = [] # M frequencies

# MFSK Signal Generation
for symbol in symbols:
    freq_index = int(symbol, 2)  # Convert bits to frequency index
    carrier_freq = f0 + freq_index * delta_f
    mfsk_signal = sqrt(2*Es/Ts) * cos(2*pi*carrier_freq*t)
    transmit(mfsk_signal)
```

---

## Slide 23: Standards Compliance & Testing

**Standard Testing Procedures:**

1. **Frequency Accuracy Test:**
   - Verify each frequency within ±ppm tolerance
   - Standards: ±2.5 ppm typical

2. **Bandwidth Measurement:**
   - Measure -3dB and -20dB bandwidth
   - Comply with ITU-R recommendations

3. **Modulation Quality:**
   - Measure phase noise
   - Verify constellation placement

4. **BER Measurement:**
   - Test at specified SNR levels
   - Compare against standard limits

5. **Interference Rejection:**
   - Test with adjacent channel interference
   - Verify selectivity > 30 dB

**Example Test Specification (Zigbee):**
- Carrier frequency: 2.4 GHz
- Modulation: 16-MFSK
- Bit rate: 250 kbps
- Frequency deviation: 150 kHz
- Required BER: < 10⁻⁵ at specified SNR

---

## Slide 24: Recent Developments & Future Trends

**Advanced MFSK Techniques:**

1. **Continuous Phase MFSK (CP-MFSK):**
   - Continuous phase between symbol transitions
   - Reduced spectral splatter
   - Better frequency efficiency

2. **Minimum Shift Keying (MSK):**
   - Special case of CPFSK with h = 0.5
   - Orthogonal, low-sidelobe modulation
   - Superior spectral efficiency

3. **Gaussian MSK (GMSK):**
   - Gaussian pulse shaping
   - Reduced bandwidth
   - Used in GSM and other standards

4. **Coded MFSK:**
   - Error-correcting codes (Turbo, LDPC)
   - Improved SNR performance
   - Enhanced reliability

**Integration with Modern Systems:**

- Machine learning for adaptive modulation selection
- Cognitive radio applications for spectrum efficiency
- Integration with 5G and beyond (mmWave MFSK)
- Quantum-enhanced demodulation concepts

---

## Slide 25: Key Equations Summary

**Fundamental Equations:**

| Quantity | Equation | Units |
|---|---|---|
| Symbol Energy | E_s | Joules |
| Bit Energy | E_b = E_s / log₂(M) | Joules |
| Bandwidth | B_w = M / T_s | Hz |
| Symbol Rate | R_s = 1 / T_s | baud |
| Bit Rate | R_b = log₂(M) · R_s | bps |
| Spectral Efficiency | η = log₂(M) / M | bits/s/Hz |
| Frequency Spacing | Δf = 1 / T_s | Hz |
| Error Probability | P_e = (M-1)Q(√(2E_s/N_0)) | dimensionless |

---

## Slide 26: Conclusion & Summary

**Key Takeaways:**

1. **MFSK Fundamentals:**
   - M orthogonal frequencies transmit log₂(M) bits per symbol
   - Excellent noise immunity in fading channels
   - Tradeoff between data rate and bandwidth

2. **Mathematical Framework:**
   - Rigorous signal representation and analysis
   - Well-defined orthogonality conditions
   - Proven error probability formulas

3. **Performance Characteristics:**
   - Spectral efficiency decreases with M
   - Power efficiency improves with M
   - Fading channel performance requires diversity

4. **Practical Applications:**
   - Underwater acoustics, amateur radio
   - Satellite and military communications
   - Modern IoT and sensor networks

5. **Standards Compliance:**
   - IEEE 802.11, 802.15.4 specifications
   - ITU-R recommendations for testing
   - Rigorous measurement procedures

**Future Outlook:**

MFSK remains relevant in niche applications where noise immunity and simplicity are prioritized over bandwidth efficiency. Hybrid approaches combining MFSK with coding and modern signal processing continue to enhance its performance in challenging communication environments.

---

## Slide 27: References & Further Reading

**Textbooks:**
- Proakis, J. G., & Salehi, M. (2007). Digital Communications. 5th Edition, McGraw-Hill.
- Haykin, S. (2013). Communication Systems. 5th Edition, John Wiley & Sons.
- Sklar, B. (2001). Digital Communications: Fundamentals and Applications. 2nd Edition, Prentice Hall.

**Standards Documents:**
- IEEE 802.11-2020: Wireless LAN Standard
- IEEE 802.15.4-2020: Low-Rate Wireless Personal Area Networks
- ITU-R F.1495: Field Strength Measurements

**Research Papers:**
- Chandra, A., et al. (2011). "SEP calculations for coherent M-ary FSK in different fading channels with MRC diversity." Wireless Communications and Mobile Computing.
- Sharma, M., & Ferreira, D. B. (2022). "Resource Allocation for Maximizing Spectral Efficiency in a Multiuser MFSK System." Journal of Communication and Information Systems.

**Online Resources:**
- Engineering Funda YouTube Channel (Digital Communication Course)
- MATLAB Communications Toolbox Documentation
- GNU Radio Project (Open-source SDR toolkit)

---

## Slide 28: Q&A Section

**Common Questions:**

**Q1: Why use MFSK over BFSK?**
A: MFSK allows higher bit rates by encoding multiple bits per symbol, though at the cost of bandwidth expansion.

**Q2: What is the optimal value of M?**
A: Depends on application. Maximum spectral efficiency at M ≈ 2.7, but practical systems use M = 2^k (4, 8, 16, 32, ...).

**Q3: Is coherent or non-coherent detection better?**
A: Coherent detection is optimal (≈3dB better), but non-coherent is simpler and widely used in practice.

**Q4: How does MFSK compare to QAM?**
A: QAM is more bandwidth efficient; MFSK is more power efficient and robust to phase noise.

**Q5: What is the main limitation of MFSK?**
A: Low spectral efficiency for large M values, making it unsuitable for bandwidth-limited applications.

---

END OF PRESENTATION
