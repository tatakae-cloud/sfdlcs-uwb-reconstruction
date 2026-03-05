# SFDLCS — UWB Signal Reconstruction

PyTorch replication of **Select-First-Decide-Later Compressive Sensing (SFDLCS)** for UWB signal reconstruction.

> **Paper:** Luo et al., *"Deep Learning Based Compressive Sensing for UWB Signal Reconstruction"*, IEEE Transactions on Geoscience and Remote Sensing, 2022.
> [https://doi.org/10.1109/TGRS.2022.3181891](https://doi.org/10.1109/TGRS.2022.3181891)

## Overview

SFDLCS uses two networks to reconstruct sparse UWB signals from compressed measurements:
- **Search Network (LSTM)** — learns correlation between nonzero index positions
- **Decision Network** — learns the distribution of nonzero elements

Together they form a "select first, decide later" structure that outperforms traditional CS algorithms.

## Results

| Algorithm | NMSE | CRR |
|-----------|------|-----|
| **SFDLCS** | **0.628** | **72.1%** |
| GPSR | 0.821 | 69.5% |
| BCS | 0.964 | 69.9% |
| OMP | 1.556 | 64.3% |

SFDLCS achieves **59.6% NMSE reduction vs OMP**, **34.8% vs BCS**, **23.5% vs GPSR**.



## Notes

- Uses synthetic UWB-like signals (Gaussian pulses) instead of real P440 sensor data
- Signal length N=480, sparse zone [0, 80), K=15 pulses per signal
- Trained at sample rate 40% (M=64 measurements)
