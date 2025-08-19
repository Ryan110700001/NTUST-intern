# 5G UE power on and Cell Search Procedure
<img width="688" height="973" alt="image" src="https://github.com/user-attachments/assets/e09fdede-a34e-43d8-9477-3bc349bd814c" />

This document summarizes the UE (User Equipment) power-on process and the initial cell selection steps in 5G SA (Standalone) architecture.

## Step 1: UE Power ON and PLMN Selection
- UE powers on and initializes hardware/software (e.g., baseband, RF, GNSS, sensors).
- Reads USIM for IMSI, preferred PLMN list, access class, allowed networks.
- Initializes protocol stack (L1 to L3, including NAS and RRC).
- PLMN selection:
  - **Automatic**: From priority list or strongest signal.
  - **Manual**: User selects from UI.
- Uses SIB1 for broadcasted PLMN info and validates with USIM info.
- Ensures no PLMN barring or roaming restriction before proceeding.

## Step 2: Frequency Band Scanning
- UE scans supported NR frequency bands based on operator list, previously connected bands, and UE capabilities.
- Searches for Synchronization Signal Blocks (SSBs).

## Step 3: Cell Search and Synchronization
- UE detects SSBs, which include:
  - **PSS (Primary Synchronization Signal)**
  - **SSS (Secondary Synchronization Signal)** → used to calculate PCI.
  - **PBCH (Physical Broadcast Channel)** → carries MIB.
- SSBs are transmitted as beams with indexes.
- PCI (Physical Cell ID) = `3 × NID1 + NID2`
<img width="953" height="437" alt="image" src="https://github.com/user-attachments/assets/96267d68-8fed-4af7-be30-c3f76de6e715" />

## Step 4: PBCH Decoding and MIB Extraction
- UE decodes PBCH to extract MIB fields:
  - `systemFrameNumber`
  - `subCarrierSpacingCommon`
  - `ssb-SubcarrierOffset`
  - `dmrs-TypeA-Position`
  - `cellBarred`, `intraFreqReselection`, etc.

## Step 5: DCI Decoding and Initial BWP Configuration
- UE decodes DCI Format 1_0 (from CORESET0) for SIB1 scheduling.
- Uses MIB-provided configs to decode PDCCH and PDSCH.
- Extracts **Initial BWP** (Bandwidth Part) settings from SIB1.
  
## Step 6: SIB1 Decoding
- SIB1 includes:
 <img width="941" height="371" alt="image" src="https://github.com/user-attachments/assets/3cfa4952-5ae5-4af3-af67-82c9d293f1af" />


## Step 7: Cell Selection
- UE computes:
  ```math
  Qrxlevmeas = RSRP – q-RxLevMinOffset
<img width="956" height="625" alt="image" src="https://github.com/user-attachments/assets/db0d6361-3dda-4931-b4ac-a3788f693eb4" />


---



