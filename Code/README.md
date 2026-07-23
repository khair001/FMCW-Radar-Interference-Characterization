# MATLAB Code for Mutual Interference Analysis using IWR6843AOP Radar

This repository contains the MATLAB scripts used in the radar interference characterization experiment with the **Texas Instruments IWR6843AOP EVM**.  
The workflow follows a step-by-step data acquisition and analysis process to detect and visualize mutual interference effects, extract clusters, and analyze velocity coherence degradation.

---

## 📂 Folder Structure


---

## ⚙️ Software Requirements

- MATLAB **R2023a** or newer  
- TI mmWave SDK (for TLV packet definitions)  
- Serial interface drivers for **IWR6843AOP**  
- Configuration (`.cfg`) file for your radar setup  

---

## 🧩 Workflow Overview

1. **Data Acquisition**  
   Run `Data_Acquisition_Code.m`  
   - Connect the radar via two COM ports (Config + Data).  
   - Update COM port names and `.cfg` file in the script.  
   - Script logs TLV packets (Type 1: position/velocity, Type 7: SNR/noise) and saves them locally.  

2. **Initial Data Analysis**  
   Run `Initial_Analyser.m`  
   - Parses and visualizes the raw detections.  
   - Identifies signal distortion and noise increase caused by mutual interference.  
   - However, interference clusters may not yet be clearly separable.  

3. **Threshold Optimization**  
   Run `Threshold_Calculation.m`  
   - Calculates adaptive thresholds based on statistical noise distribution.  
   - Determines suitable cutoff values to suppress false detections.  

4. **Refined Clustering Analysis**  
   Run `Updated_Analyser.m`  
   - Integrates optimized threshold from Step 3.  
   - Detects and visualizes interference clusters in 3D plots.  
   - Compares baseline vs interference datasets effectively.  

5. **Velocity Profiling (ADV Analysis)**  
   a. Run `data_for_VelocityProfile.m` to extract per-frame velocity data.  
   b. Then run `Velocity_profile.m` to generate frame-wise velocity plots and compute **Average Directional Variance (ADV)** — a metric that quantifies velocity decoherence due to interference.  

---

## 📊 Outputs

Each step produces specific results:
| Output Type | Description |
|--------------|-------------|
| `*.mat` / `*.bin` | Raw and parsed TLV data files |
| Plots (3D & 2D) | Interference clusters and SNR/noise visualizations |
| `threshold_results.mat` | Optimized threshold values |
| `velocity_profile.png` | Frame-wise velocity distribution |
| `ADV_results.csv` | ADV metric for baseline vs interference |

---

## ⚠️ Important Notes

- Disable **clutter removal** during acquisition to avoid losing static reference reflections.  
- Keep **chirp slope and frame rate identical** between baseline and interference tests.  
- Use the **same test environment** (target distance, angle, and motion path) for consistent comparison.  
- The `collected_data/` folder should store raw and parsed data files before analysis.

---


