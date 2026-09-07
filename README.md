# FMCW Radar Interference Characterization

This repository contains the **MATLAB implementation, experimental measurements, analysis results, and project report** from a pre-thesis research project conducted as part of the **M.Eng. Embedded Systems Engineering** program at **FH Dortmund – University of Applied Sciences and Arts**.

The project investigates **mutual interference (MI) in FMCW mmWave radar systems** using two Texas Instruments **IWR6843AOP EVM** radar sensors. The work focuses on experimentally characterizing how interference affects radar detections, signal quality, clustering behaviour, and Doppler/velocity coherence.

This research project subsequently provided the experimental and analytical foundation for my Master's thesis on **FMCW radar interference characterization and localization**.

---

## Project Overview

As the number of FMCW radar sensors operating in shared frequency bands increases, overlapping radar transmissions can lead to **mutual interference**. Depending on the radar configurations and timing, interference can alter detection statistics, increase apparent noise, generate anomalous detections, and reduce the coherence of estimated target velocities.

This project experimentally investigates these effects using a dual-radar setup consisting of an independently operating **observer radar** and **interferer radar**.

A MATLAB-based analysis framework was developed to compare baseline and interference-present measurements through:

- Range, SNR, velocity, and noise analysis
- Statistical comparison of baseline and interference datasets
- DBSCAN-based clustering
- Data-driven threshold optimization
- False Positive Rate (FPR) and False Discovery Rate (FDR) evaluation
- Frame-wise velocity profile analysis
- Investigation of interference-induced velocity decoherence

The experiments investigate how **chirp-slope mismatch and overlapping radar operation** produce measurable changes in radar detections and velocity behaviour.

---

## Experimental Setup

The experimental platform consisted of:

- **Radar hardware:** 2 × Texas Instruments IWR6843AOP EVM
- **Operating frequency:** 60 GHz
- **Environment:** Controlled indoor measurements
- **Radar roles:** Observer radar and independently operating interferer radar
- **Target:** Moving human subject
- **Data interface:** UART serial communication
- **Processing environment:** MATLAB

Unlike the later Master's thesis, which operated directly on captured raw ADC measurements, this project analysed **processed radar outputs transmitted through the TI TLV interface**.

The primary data used were:

- **TLV 1:** Detected-point information including 3D position and radial velocity
- **TLV 7:** Side information including SNR and noise-level estimates

The radar output was acquired, parsed, and stored using a customized MATLAB-based parser adapted for the TI mmWave radar platform.

---

## Methodology

The experimental analysis was developed progressively through several stages.

### 1. Data Acquisition

Baseline and interference-present radar measurements were collected under controlled experimental conditions.

The measurement campaign varied parameters including:

- Chirp slope
- Total frame count
- Static clutter removal settings

A total of **nine experimental configurations** were investigated.

---

### 2. Baseline and Interference Analysis

An initial MATLAB analyzer was developed to compare baseline and interference-present measurements using:

- Total number of detections
- Static and moving detections
- Range distributions
- SNR distributions
- Noise characteristics
- Clustering statistics

The initial analysis showed that interference could increase the number of radar detections and alter their statistical characteristics. However, fixed clustering parameters alone were not sufficient to consistently distinguish interference-related detections.

---

### 3. Threshold Optimization

A MATLAB-based threshold-estimation procedure was introduced to improve the separation between normal target detections and interference-related anomalies.

Candidate thresholds were evaluated using detection statistics including **False Positive Rate (FPR)** and **False Discovery Rate (FDR)**.

The resulting threshold was incorporated into an updated analysis framework for subsequent interference characterization.

---

### 4. DBSCAN-Based Clustering

**DBSCAN** was applied to investigate the spatial structure of radar detections without requiring a predefined number of clusters.

After incorporating the optimized thresholding approach, the updated analyzer was able to reveal interference-related clustering behaviour that was not clearly distinguishable using the initial analysis configuration.

This demonstrated the value of combining statistical filtering with density-based clustering rather than relying on clustering alone.

---

### 5. Velocity-Coherence Analysis

Frame-wise velocity profiles were analysed to investigate how mutual interference affects Doppler consistency.

Baseline measurements exhibited comparatively coherent target-velocity behaviour, whereas interference-present measurements showed increased fluctuations and irregular velocity patterns.

This observation motivated the analysis of **interference-induced velocity decoherence** as an additional indicator of mutual radar interference.

---

## Representative Experiment

One representative configuration discussed in detail in the project report used:

| Parameter | Value |
|---|---:|
| Observer/Baseline Chirp Slope | 3 MHz/µs |
| Interferer Chirp Slope | 7 MHz/µs |
| Total Frames | 500 |
| Static Clutter Removal | Disabled |
| Range Resolution | 0.044 m |
| Maximum Radial Velocity | 1 m/s |
| Doppler Resolution | 0.13 m/s |
| Frame Duration | 100 ms |

The chirp-slope mismatch between the observer and interfering radar was used to create a controlled mutual-interference condition and investigate its influence on the observer's processed detections.

---

## Key Results

The experimental investigation produced several key observations:

- Interference-present measurements showed an increase in raw radar detections for the evaluated scenarios.
- Range-SNR and noise characteristics changed under mutual interference.
- Fixed clustering parameters alone were insufficient to reliably isolate interference-related detections.
- Data-driven threshold optimization improved the separation of interference-induced anomalies.
- Combining thresholding with DBSCAN revealed interference-related clustering behaviour in representative measurements.
- Frame-wise velocity analysis showed reduced Doppler/velocity coherence under interference conditions.
- Processed radar point-cloud and side-information data provided useful indicators for diagnosing mutual interference even without direct access to raw ADC samples.

Overall, the project showed that **statistical analysis, adaptive thresholding, density-based clustering, and velocity-domain analysis can provide complementary indicators for FMCW radar interference characterization**.

The findings also motivated the subsequent Master's thesis, in which the investigation was extended to **raw ADC measurements, Range-Doppler processing, interference detection and classification, and exploratory interference-source bearing estimation**.

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
```

---

## Code

The [`Code`](Code/) directory contains the MATLAB scripts developed during the project:

- **`Data_Acquisition_Code.m`** — acquires and stores radar output from the TI mmWave platform
- **`Initial-Analyser.m`** — performs the initial baseline/interference statistical analysis
- **`Threshold_Calculation.m`** — evaluates and derives thresholds for interference-related detection analysis
- **`Updated_Analyser.m`** — applies the updated analysis and clustering approach
- **`Velocity_profile.m`** — analyses frame-wise target velocity behaviour
- **`data_for_VelocityProfile.m`** — prepares measurement data for velocity-profile analysis

Additional implementation information is available in [`Code/README.md`](Code/README.md).

---

## Project Report

The complete project report is available in the [`Report`](Report/) directory.

It contains the theoretical background, experimental configurations, analysis methodology, parameter evaluation, results, and discussion that led to the subsequent Master's thesis research.

---

## Technologies and Methods

`MATLAB` · `FMCW Radar` · `mmWave Radar` · `Radar Signal Processing` · `TI TLV Data Processing` · `DBSCAN` · `Threshold Optimization` · `Statistical Analysis` · `FPR/FDR Evaluation` · `Doppler/Velocity Analysis` · `Experimental Validation` · `TI IWR6843AOP`

---

## Related Work

This project was continued and substantially extended in my Master's thesis:

**Interference Characterisation and Localisation for FMCW mmWave Radars**

The Master's thesis extends the work from processed radar outputs to **raw ADC signal processing**, including Range-Doppler processing, CA-CFAR detection, interference classification, temporal analysis, clustering, and exploratory phase-based bearing estimation.

🔗 [Master's Thesis Repository](https://github.com/khair001/Master_Thesis)

---

## Author

**Md Abul Khair**  
M.Eng. Embedded Systems Engineering  
FH Dortmund – University of Applied Sciences and Arts
