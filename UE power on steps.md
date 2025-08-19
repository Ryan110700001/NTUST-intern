# 5G NR UE Initial Access and Cell Search Procedure

## Introduction

When a User Equipment (UE) is powered on, it attempts to connect to a 5G cell. The UE has no prior frequency knowledge and performs a **blind search** through:
- **Storage List Search (SLS)**: Check previously stored frequencies.
- **Full Band Search (FBS)**: Scan all supported frequencies if SLS fails

## Initial Steps of Cell Search

### Step 1: RSSI Measurement
UE scans all supported frequencies and measures **RSSI (Received Signal Strength Indicator)** for each.

### Step 2: RSSI Thresholding
UE filters out frequencies with RSSI below a threshold (threshold implementation-specific).

### Step 3: SSB Decoding
UE scans **SSB (Synchronization Signal Block)** using **synchronization raster**.

---

## Synchronization Signal Block (SSB) Search

### Purpose of SSB
- Obtain synchronization information
- Identify **physical cell ID** (PCI)

### SSB in Standalone vs. Non-Standalone
- **Non-Standalone (NSA)**: No blind search; config via RRC
- **Standalone (SA)**: Blind search is required to find SSB

---

## Synchronization Raster and GSCN

### What is GSCN?
- **Global Synchronization Channel Number**
- Like LTE’s channel raster but optimized for 5G's larger bandwidths

### Scanning with GSCN
- UE uses **GSCN positions** to perform sparse, efficient scanning
- GSCN represents SSB center frequency
- Formula:
  - `SSREF = N × 1.2 MHz + M × 15 kHz`
  - `GSCN = 3 × N + (M – 3)/2` (for 0–3 GHz)

### Example Calculation
- Scan #1: GSCN = 5279, M = 1  
  → N = 1760  
  → `Ssref = 2112.05 MHz`  
  → `ARFCN = (2112.05 – 2110)/0.005 + 422000 = 422410`

UE continues scanning GSCN values until SSB is detected.

---

## SSB Mapping and Structure

- **SSB Composition**: PSS, SSS, PBCH
- **Occupies**: 20 RBs in frequency, 4 symbols in time
- **Transmitted via**: Antenna Port 4000

### PBCH (Physical Broadcast Channel)
- Includes MIB (Master Information Block)
- Modulated using QPSK
- Uses DMRs (Demodulation Reference Signals) for decoding

---

## PSS (Primary Synchronization Signal)

- Determines physical-layer identity NID(2)
- Generated via BPSK-modulated m-sequence (length 127)
- Cyclic shift: 0, 43, 86 depending on PCI
- Located in symbol 1 of the SSB

---

## SSS (Secondary Synchronization Signal)

- Determines PCI group number NID(1)
- Mapped in symbol 3 of the SSB
- Uses BPSK-modulated **Gold sequence** (length 127)
- Total: 336 SSS sequences × 3 PSS options = 1008 PCIs

---

## PCI (Physical Cell Identity)

- Total in NR: **1008**
  - LTE had 504
- PCI = Combination of NID(1) + NID(2)

---

## Time-Domain Resource Allocation

### Example: Case A
- Subcarrier Spacing: 15 kHz
- Frequency: ≤ 3 GHz
- Max SSBs per SS burst set = 4
- SSB start symbols: 2, 8, 16, 22

---

## SSB Location Calculation

1. Get carrier bandwidth and subcarrier spacing
2. Use formula:
   - `SSB Subcarrier Offset = (FreqA – FreqSSB) / SubcarrierSpacing`

---


---


