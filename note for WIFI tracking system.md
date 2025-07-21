# A Novel Device-Free Tracking System Using WiFi

This document summarizes the paper’s main findings, key points, implementation details, experimental setup, abstract analysis, and mathematical formulations.

---
## 1. Abstract Analysis

* **Challenge**: CSI phase errors cause ambiguous Doppler sign.
* **Insight**: Exploit large-scale fading for direction.
* **Modeling**: Ray tracing → two power profiles (toward/away).
* **Processing**: STFT → Doppler power; DDTW → direction matching.
* **Result**: 0.84 m median tracking error on Intel 5300 hardware. fileciteturn5file0

## 2. Main Findings

* **Fading-Based Direction Estimation**: Leverages large-scale fading (path-loss variations) to resolve Doppler sign ambiguity in CSI, turning a traditional “foe” of communications into a “friend” for device-free tracking.
* **Ray-Tracing Profiling**: Introduces a simplified ray-tracing model to characterize received-power profiles for targets moving toward vs. away from the Tx–Rx link.
* **STFT + DDTW Pipeline**: Applies Short-Time Fourier Transform to CSI to extract Doppler power, then uses Derivative Dynamic Time Warping to match against the two fading profiles and infer movement direction.
* **Implementation & Accuracy**: Realized on commodity Intel 5300 Wi-Fi cards; achieves a median tracking error of **0.84 m**, outperforming prior work (\~1.1 m) fileciteturn0file0.

---

## 3. Key Point from Each Paragraph

1. **Abstract**: Proposes turning Wi‑Fi fading into a tool for direction estimation, coupling STFT-based Doppler power extraction with DDTW, yielding 0.84 m median error. fileciteturn0file0
2. **Introduction 1**: Argues the necessity of device‑free tracking for applications where targets cannot carry devices. fileciteturn0file0
3. **Introduction 2**: Positions Wi‑Fi device‑free localization like radar‑style detection—using multipath RSS fluctuations—for low cost and easy deployment. fileciteturn0file0
4. **Introduction 3**: Reviews RSS fingerprinting: labor-intensive calibration and only meter-level accuracy due to coarse RSS measurements. fileciteturn0file0
5. **Introduction 4**: Notes CSI provides fine-grained features; prior CSI-fingerprint methods need arrays/calibration, and Doppler-based methods suffer from direction ambiguity. fileciteturn0file0
6. **Introduction 5**: Presents the paper’s approach: exploit fading for direction, model profiles via ray tracing, match via DDTW on STFT-derived Doppler power, then PDR tracking. fileciteturn0file0
7. **System II Opening**: Highlights the challenge: phase errors (CFO/STO) obscure Doppler sign in CSI; proposes using large-scale fading instead. fileciteturn0file0
8. **II.A Moving Speed Estimation**: Derives CSI power expression separating static vs. dynamic paths and shows STFT can extract absolute Doppler magnitude (speed) despite phase errors. fileciteturn0file0
9. **II.B.1 Ray Tracing Analysis**: Uses a ray-tracing path-loss model to show received power decreases when moving toward the link and increases when moving away, creating two distinct power profiles. fileciteturn0file0
10. **II.B.2 Feature Power Extraction**: Defines “feature power” as the sum of STFT-extracted Doppler power over the full Doppler range, isolating dynamic-path contributions. fileciteturn0file0
11. **II.B.3 Doppler Sign Identification**: Computes the first-order derivative of the feature-power sequence and uses its sign to infer movement direction. fileciteturn0file0
12. **II.C Motion Detection**: Proposes a motion-detector based on Doppler-power variance exceeding a threshold learned under static conditions. fileciteturn0file0
13. **II.D Target Tracking**: Integrates speed and direction estimates into a Pedestrian Dead-Reckoning (PDR) update for location. fileciteturn0file0
14. **III.A Implementation**: Describes the indoor testbed: 4 × 4.8 m² area, one 5 GHz transmitter, two receivers (Intel 5300 cards at 1 kHz sampling). fileciteturn0file0
15. **III.B.1 Overall Performance**: Shows 0.84 m median localization error vs. \~1.1 m prior; tight alignment between estimated and actual trajectories. fileciteturn0file0
16. **III.B.2 Motion Detection Performance**: Fusing three antennas and two receivers at κ=2 yields 98.15% correct detection (vs. 89% amplitude-based). fileciteturn0file0
17. **Conclusion**: Reiterates novelty—fading-based direction estimation via ray tracing, STFT, DDTW—and validates 0.84 m median error on commodity hardware. fileciteturn0file0

---

## 3. Implementation Details

* **Testbed Layout**: 4 m × 4.8 m indoor area; three mini‑PCs at 1.2 m height (one Tx, two Rx) fileciteturn2file0L80-L85.
* **Hardware**: Intel 5300 NICs with three antennas; Ubuntu 10.0.2 on mini‑PCs. fileciteturn2file0L85-L88
* **Radio Config**: 5 GHz band; 1 kHz packet rate for high-resolution CSI. fileciteturn2file0L88-L90

---

## 4. Experimental Setup: Step-by-Step

1. **Gather Hardware**: 3 mini‑PCs, Intel 5300 cards, omnidirectional antennas.
2. **Software Environment**: Ubuntu 10.0.2; patch and install Linux 802.11n CSI tool; dependencies (`build-essential`, `git`, headers). fileciteturn3file0L85-L88
3. **Testbed Geometry**: Mark 4 × 4.8 m area; mount PCs at 1.2 m; place Rx1 at 4 m, Rx2 at 4.8 m from Tx. fileciteturn3file0L80-L85
4. **Radio Settings**: Set 5 GHz channel; Tx at 1 kHz; verify CSI logging. fileciteturn3file0L88-L90
5. **Calibration**: Record static CSI to compute baseline mean Ĩ and σI; choose κ (e.g., 2) fileciteturn3file2L148-L153
6. **Trials**: Define paths; walk at \~1.2 m/s; log CSI. fileciteturn3file0L91-L97
7. **Post-Processing**:

   * Compute |Ĥ(f,t)|²; STFT → Doppler power; sum over f → feature power sequence.
   * Use ray-traced toward/away profiles; DDTW for direction; speed = |fD|·λ/(2f). fileciteturn3file8L7-L12
8. **PDR Fusion**: Update Lₜ₊₁ = Lₜ + v(t)·T·sgn(D); optionally fuse Rx estimates. fileciteturn3file12L69-L74
9. **Evaluation**: CDF of position error (median\~0.84 m); motion detection metrics. fileciteturn4file1L31-L37

---


---

## 5. Mathematical Formulation

### CSI Signal Model

```math
H(f,t) = \sum_{i\in P_s} a_i(f)e^{-j2\pi f\tau_i} + \sum_{k\in P_d} a_k(f,t)e^{-j2\pi(f\tau_k + f_{D_k}t)}
```

Handles static and dynamic multipaths; phase errors ĥω obscure Doppler sign. fileciteturn6file9L21-L27

### Power-Based Extraction

```math
|Ĥ(f,t)|^2 ≈ 2|Ĥ_s(f)| \sum_{k\in P_d}a_k(f,t)\cos(2\pi f_{D_k}t)
```

STFT on |Ĥ| recovers |f\_{D\_k}|. fileciteturn6file1L63-L71

### Ray-Tracing Path-Loss

```math
P_r = P_t(\frac{λ}{4π})^2G_tG_r|\frac{1}{d_0} + \sum_{i=1}^{N-1}(\frac{1}{d_i}\prod_{k=1}^{n_i}R_{k,i}e^{-j2πd_i/λ})|^2
```

Profiles vary as target moves. fileciteturn6file7L29-L37

### Feature Power & DDTW

```math
\bar I_t = \sum_{k=f_{min}}^{f_{max}} I_k
```

Match \bar I\_t to reference toward/away using DDTW.

### Motion Detection

```math
\tilde I = \frac{1}{n}\sum_{i=1}^n \bar I_i,
σ_I = \sqrt{\frac{1}{n}\sum_{i=1}^n(\bar I_i-\tilde I)^2}
```

Motion if \bar I\_t > \tilde I + κσ\_I. fileciteturn6file4L89-L94

### PDR Update

```math
L_{t+1} = L_t + v_t T \quad\text{with } v_t = \frac{λ}{2f}|f_D|\;\text{and sign by DDTW}
```

Recursive 2D location update. fileciteturn6file5L69-L74

---

*End of summary.*
