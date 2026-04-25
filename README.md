# Smart Energy Monitor ⚡

> Non-Intrusive Load Monitoring (NILM) & Energy Disaggregation Dashboard  
> **ICRA Satellite School 2026 — Grant Project**

[![IEEE](https://img.shields.io/badge/IEEE-Senior%20Member-00629B?style=flat-square)](https://ieee.org)
[![RAS](https://img.shields.io/badge/IEEE-RAS%20Member-00629B?style=flat-square)](https://ieee.org)
[![Dataset](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=flat-square)](https://www.kaggle.com/datasets/mexwell/smart-home-energy-consumption)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## Overview

A smart home energy monitoring system that predicts monthly electricity bills using a **single-point measurement approach** — eliminating the need for per-appliance sensors. The system captures current and power signatures at one location, applies a **Naive Bayes classifier** to disaggregate loads, and visualizes real-time consumption through an interactive web dashboard.

**Live Dashboard →** [mzunnurainhussain.github.io/smart-energy-monitor](https://mzunnurainhussain.github.io/smart-energy-monitor)

---

## Dashboard Features

- **Hourly consumption** bar chart with Today / This week / This month toggle
- **Load disaggregation** — per-appliance kWh breakdown via NILM
- **Appliance share** donut chart
- **Temperature & humidity vs. consumption** 30-day trend
- **Live appliance state** panel (ON/OFF + wattage)
- **Interactive bill estimator** with adjustable PKR/kWh rate slider

---

## Technical Stack

### Hardware
| Component | Role |
|-----------|------|
| Raspberry Pi (Raspbian) | Central processing unit |
| Arduino Nano | Sensor data acquisition |
| ACS712 Current Sensor | RMS current measurement |
| Voltage Transformer | Mains voltage sensing |
| LM339 ZCD Circuit | Zero-cross detection |
| 7486 EXOR IC | Phase angle measurement |

### Software
| Component | Role |
|-----------|------|
| Python (77%) | Core NILM algorithms |
| C++ (20%) | Arduino firmware |
| Naive Bayes Classifier | Appliance state detection |
| Flask | Real-time web dashboard |
| Chart.js | Interactive visualizations |
| HTML/AJAX | Frontend dashboard |

---

## Dataset

**Kaggle:** [mexwell/smart-home-energy-consumption](https://www.kaggle.com/datasets/mexwell/smart-home-energy-consumption)

```python
import kagglehub
path = kagglehub.dataset_download("mexwell/smart-home-energy-consumption")
print("Path to dataset files:", path)
```

The dataset contains appliance-level energy readings, timestamps, temperature, and humidity for a smart home environment — used to train and validate the Naive Bayes NILM classifier.

---

## How It Works

### 1. Power Measurement
- Sample mains line to get peak voltage (Vpp)
- Compute RMS: `Vrms = (Vpp/2) × 0.707`
- Convert to current using ACS712 scale factor
- `P = Vrms × Irms`

### 2. Load Disaggregation (NILM)
- Monitor current delta between consecutive samples
- Use real + reactive power as classification features
- Zero Cross Detection (ZCD) determines phase angle → active/reactive power
- Naive Bayes classifies appliance state from (ΔI, P, Q) feature vector

### 3. Bill Estimation
- Track Start/Stop time per appliance state
- `Energy = Power × Active Time`
- `Monthly Bill = Σ(Energy per appliance) × Rate per unit`

---

## Quick Start

```bash
git clone https://github.com/mzunnurainhussain/smart-energy-monitor.git
cd smart-energy-monitor
open index.html
```

No build step required — the dashboard runs as a standalone HTML file.

---

## Project Info

| Field | Details |
|-------|---------|
| Presenter | Muhammad Zunnurain Hussain |
| IEEE Membership ID | 92687282 |
| Membership Grade | Senior Member |
| IEEE Section | IEEE Lahore Section |
| Institution | Bahria University Lahore Campus |
| Event | ICRA Satellite School 2026 |
| Field | Automation / Smart Energy |
| Classifier Accuracy | ~94% (Naive Bayes) |

---

## References

1. [ACS712 Datasheet — SparkFun](https://www.sparkfun.com/datasheets/BreakoutBoards/0712.pdf)
2. [NILM Approaches for Disaggregated Energy Sensing — NCBI](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3571813/)
3. [NILM using Hidden Markov Models](https://www.youtube.com/watch?v=9a8dR9NEe6w)
4. [Neural NILM](https://www.youtube.com/watch?v=PC60fysLScg)
5. [Kaggle Dataset — mexwell/smart-home-energy-consumption](https://www.kaggle.com/datasets/mexwell/smart-home-energy-consumption)

---

## License

MIT © Muhammad Zunnurain Hussain
