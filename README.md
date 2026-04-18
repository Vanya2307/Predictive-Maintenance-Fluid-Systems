# Cross-Dataset Predictive Maintenance of Fluid-Power Systems

## Research Question
Can similar pre-failure sensor patterns be identified in two different fluid-power systems: a metro train air compressor and a hydraulic test rig?

## Overview
This project investigates predictive maintenance in two different fluid-power mechanical systems through data analysis. The main goal is to explore whether similar warning patterns can be identified before failure across two independent systems.

## Data Sources
- **Dataset 1:** MetroPT-3 - sensor data from a metro train air compressor 
  in Porto, Portugal  
  https://archive.ics.uci.edu/dataset/791/metropt-3+dataset

- **Dataset 2:** Condition Monitoring of Hydraulic Systems - multi-sensor 
  data from a hydraulic test rig  
  https://archive.ics.uci.edu/dataset/447/condition+monitoring+of+hydraulic+systems

## Setup
- Download both datasets from the links above
- Place MetroPT-3 CSV in `data/raw/MetroPT-3 Train Dataset/`
- Place Hydraulic System files in `data/raw/Predictive Maintenance Of Hydraulics System/`
- Run notebooks in order starting from `01_data_loading_and_cleaning.ipynb`

## Planned Work
- Data loading, cleaning and validation
- Harmonization of two independent data sources
- Exploratory Data Analysis (EDA) and visualization
- Hypothesis testing
- Interpretation of results

## Project Structure
...

TODO: save final figures to ../figures/ after notebook structure and plots are finalized.