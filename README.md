# SITL Benchmark Suite for UAV Communication Security

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![ArduPilot](https://img.shields.io/badge/ArduPilot-v4.5.1-orange)](https://ardupilot.org/)
[![Python](https://img.shields.io/badge/Python-3.10+-green)](https://python.org)

Research artifacts accompanying the paper:

> **UAV Communication Security: A Survey on Threats, Protocols, and Deception-Based Defenses**  
> Prajwal Chowdary M, Sapna V. M., Prasad H. B.  
> *Submitted to ACM Computing Surveys (CSUR), 2026*

## Overview

This repository contains the **SITL (Software-In-The-Loop) benchmark suite** for evaluating MAVLink intrusion detection systems. It provides:

- **Attack simulation scripts** — Replay, injection, fuzzing, and DoS attack generators
- **Detection baselines** — Random Forest, Isolation Forest, and One-Class SVM models
- **Trained model weights** — Pre-trained `.pkl` files for immediate evaluation
- **SITL configuration** — ArduPilot v4.5.1 parameters for reproducible experiments
- **Real-world attack datasets** — Anonymized connection logs from deployed honeypots

## Repository Structure

```
sitl-benchmark/
├── README.md
├── LICENSE
├── requirements.txt
├── attacks/                    # Attack simulation scripts
│   ├── simulate_real_attack.py # Multi-vector attack simulator
│   └── test_data_generator.py  # Synthetic MAVLink traffic generator
├── detection/                  # Detection baselines
│   ├── skill_classifier.py     # Random Forest classifier
│   ├── anomaly_detector.py     # Isolation Forest + One-Class SVM
│   ├── train_model.py          # Model training pipeline
│   └── evaluator.py            # Metrics and evaluation
├── models/                     # Pre-trained model weights
│   ├── skill_model.pkl         # Skill classification model
│   └── trained_model.pkl       # Anomaly detection model
├── datasets/                   # Anonymized attack datasets
│   ├── connections.csv         # Connection metadata
│   └── adaptive_data.csv       # Adaptive honeypot interaction logs
├── honeypot/                   # MAVLink honeypot core
│   └── mavlink_honeypot.py     # Adaptive deception engine
└── config/                     # SITL configuration
    └── ardupilot_params.md     # ArduPilot v4.5.1 parameters
```

## Quick Start

### Prerequisites
- Python 3.10+
- ArduPilot SITL (v4.5.1 recommended)
- pymavlink >= 2.4.40

### Installation

```bash
git clone https://github.com/mavlink-honeypot/sitl-benchmark.git
cd sitl-benchmark
pip install -r requirements.txt
```

### Running Detection Baselines

```bash
# Train models on SITL-generated data
python detection/train_model.py

# Evaluate detection accuracy
python detection/evaluator.py --model models/trained_model.pkl --dataset datasets/connections.csv
```

### Running Attack Simulations

```bash
# Generate synthetic attack traffic
python attacks/test_data_generator.py --output datasets/synthetic_attacks.csv

# Run multi-vector attack simulation
python attacks/simulate_real_attack.py --target localhost:5760
```

## Baseline Results

Results from Table 14 in the paper (ArduPilot v4.5.1 SITL, RPi4 inference):

| Model | Accuracy | FPR | FNR (Replay) | Inference (ms) |
|-------|----------|-----|-------------|----------------|
| Random Forest | 96.8% | 1.2% | 8.7% | 0.3 |
| Isolation Forest | 93.1% | 4.2% | 11.5% | 1.1 |
| One-Class SVM | 91.4% | 5.8% | 14.2% | 1.8 |

## Honeypot Deployment

The honeypot has been deployed on two continents for real-world data collection:
- **US** — Cloud VPS
- **India** — Cloud VPS

Combined statistics (as of May 2026):
- 8,674+ connections from 1,971+ unique IPs
- 118 fingerprinted attacker sessions
- MAVLink-aware probes from 3 distinct threat actors

## Citation

If you use this benchmark in your research, please cite:

```bibtex
@article{chowdary2026uav,
  title={UAV Communication Security: A Survey on Threats, Protocols, and Deception-Based Defenses},
  author={Chowdary M, Prajwal and V. M., Sapna and H. B., Prasad},
  journal={ACM Computing Surveys},
  year={2026},
  note={Under review}
}
```

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

## Acknowledgments

- [ArduPilot](https://ardupilot.org/) — Open-source autopilot platform
- [pymavlink](https://github.com/ArduPilot/pymavlink) — MAVLink Python library
- PES University, Department of Computer Science and Engineering
