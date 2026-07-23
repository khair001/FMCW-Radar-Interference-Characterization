# FMCW Radar Interference Characterization

This repository contains the MATLAB code, experimental data, analysis results, and project report from a pre-thesis research project conducted as part of the M.Sc. Embedded Systems Engineering program at FH Dortmund – University of Applied Sciences and Arts.

The project investigates **mutual interference (MI) in FMCW mmWave radar systems** using two Texas Instruments **IWR6843AOP EVM** radar sensors. The work focuses on experimentally characterizing how interference affects radar detections, signal quality, clustering behavior, and velocity coherence.

The project also served as a foundation for subsequent Master's thesis research on FMCW radar interference characterization and localization.

---

## Project Overview

As the number of FMCW radar sensors operating in shared frequency bands increases, mutual interference can become a significant challenge. Overlapping radar transmissions can introduce additional detections, increase the noise floor, generate spurious responses, and degrade Doppler coherence.

This project experimentally investigates these effects using a dual-radar setup consisting of an **observer radar** and an **interferer radar**.

A MATLAB-based analysis framework was developed to compare baseline and interference-present measurements through:

- Range, SNR, velocity, and noise analysis
- Statistical comparison of baseline and interference datasets
- DBSCAN-based clustering
- Threshold optimization for interference detection
- False Positive Rate (FPR) and False Discovery Rate (FDR) evaluation
- Frame-wise velocity profile analysis
- Investigation of velocity coherence degradation under mutual interference

The experiments demonstrate how slope-mismatch interference can produce measurable changes in radar detections and velocity behavior.

---

## Experimental Setup

The experimental system uses:

- **Radar Hardware:** 2 × Texas Instruments IWR6843AOP EVM
- **Operating Frequency:** 60 GHz band
- **Environment:** Controlled indoor environment
- **Radar Roles:** Observer radar and interferer radar
- **Target:** Moving human subject
- **Data Interface:** UART serial communication
- **Processing Environment:** MATLAB

The radar output was acquired using TLV (Type-Length-Value) packets:

- **TLV 1:** 3D position and radial velocity information
- **TLV 7:** Signal-to-Noise Ratio (SNR) and noise-level information

The acquired data were parsed and stored using a customized MATLAB-based parser adapted for the TI mmWave radar platform.

---

## Methodology

The analysis framework follows several stages.

### 1. Data Acquisition

Radar measurements are collected for baseline and interference-present conditions.

The experimental configurations include variations in:

- Chirp slope
- Total frame count
- Clutter removal settings

A total of nine experimental configurations were investigated during the project.

### 2. Baseline and Interference Analysis

The initial MATLAB analyzer compares baseline and interference datasets using:

- Total radar detections
- Static and moving object detections
- Range distributions
- SNR distributions
- Noise characteristics
- Clustering statistics

The initial analysis showed an increase in raw detections under interference conditions, but fixed clustering parameters were not sufficient to clearly separate interference-related detections.

### 3. Threshold Optimization

A MATLAB-based threshold estimation procedure was introduced to improve the separation between normal object detections and interference-related anomalies.

The optimized threshold was then integrated into an updated analysis framework.

### 4. DBSCAN-Based Clustering

DBSCAN clustering is used to analyze spatial detection patterns.

After threshold optimization, the updated analyzer was able to identify interference-related clusters that were not distinguishable using the initial analysis configuration.

### 5. Velocity Profile Analysis

Frame-wise velocity profiles are analyzed to investigate the effect of mutual interference on Doppler consistency.

Baseline measurements showed comparatively stable velocity patterns, while interference-present measurements exhibited increased fluctuations and irregular velocity behavior.

This analysis was used to investigate interference-induced degradation of velocity coherence.

---

## Representative Experiment

One representative configuration discussed in detail in the project report used:

| Parameter | Value |
|---|---|
| Observer/Baseline Chirp Slope | 3 MHz/µs |
| Interferer Chirp Slope | 7 MHz/µs |
| Total Frames | 500 |
| Static Clutter Removal | Disabled |
| Range Resolution | 0.044 m |
| Maximum Radial Velocity | 1 m/s |
| Doppler Resolution | 0.13 m/s |
| Frame Duration | 100 ms |

The slope mismatch between the observer and interferer radar was used to induce controlled mutual interference.

---

## Key Results

The experimental analysis produced several key observations:

- The number of raw detections increased under interference-present conditions.
- Range-SNR and noise distributions showed changes under mutual interference.
- The initial clustering approach did not clearly distinguish interference-related detections.
- Threshold optimization improved the separation of interference-induced anomalies.
- The updated analyzer identified distinct interference-related clusters in the representative interference dataset.
- Frame-wise velocity analysis showed reduced Doppler consistency under interference conditions.
- The experiments demonstrated that processed radar point-cloud data can provide useful indicators for diagnosing mutual interference even without direct raw ADC access.

These results demonstrate the potential of combining statistical analysis, clustering, threshold optimization, and velocity-domain analysis for FMCW radar interference characterization.

---

## Repository Structure

```text
FMCW-Radar-Interference-Characterization/
│
├── Code/
│   ├── Data_Acquisition_Code.m
│   ├── Initial-Analyser.m
│   ├── Threshold_Calculation.m
│   ├── Updated_Analyser.m
│   ├── Velocity_profile.m
│   ├── data_for_VelocityProfile.m
│   └── README.md
│
├── Data_and_configuration_file/
│   ├── collected_data/
│   └── my_profile.cfg
│
├── Report/
│   └── Interference_Characterization_and_Localization_Framework_for_FMCW_mmWave_Radars.pdf
│
├── Results/
│   ├── Excel file
│   └── Radar_Interference_Experiments...
│
└── README.md
