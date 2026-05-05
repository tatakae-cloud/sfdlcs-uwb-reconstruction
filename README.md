# UWB Signal Reconstruction: SFDLCS with Deep Learning Enhancements

This project implements a high-precision reconstruction pipeline for Ultra-Wideband (UWB) soil echo signals using Compressive Sensing (CS) and Deep Learning. It transitions from traditional greedy algorithms to a data-driven "Select-First-Decide-Later" (SFDLCS) framework.

## Project Structure

The project is divided into two major phases:

### Phase 1: Core SFDLCS Framework
- **Sensing Model**: Compressed measurements $y = \Phi s$, where $s$ is the sparse signal.
- **Search Network (LSTM)**: Replaces greedy selection with an LSTM to model sequential dependencies between residuals and sparse indices.
- **Decision Network (FCNN)**: A verification stage that validates indices based on the learned distribution of non-zero elements in UWB signals.
- **Baselines**: Comparative analysis against OMP, BCS, and GPSR.

### Phase 2: Learned Enhancements
- **Transformer Encoder**: Replaces the LSTM Search Network with self-attention mechanisms to capture global dependencies across reconstruction iterations.
- **Adaptive Sensing ($\Phi$)**: Implements a learnable sensing matrix that adapts to the signal structure during training, significantly reducing NMSE.
- **Differentiable Proxy**: Uses a neural decoder during training to enable gradient flow into the sensing matrix.

## Key Results
- **Phase 1**: SFDLCS consistently outperformed OMP, especially at low sampling rates ($M \ll N$).
- **Phase 2 (Transformer)**: Achieved a marginal (~1.2%) improvement in NMSE over LSTM.
- **Phase 2 (Adaptive $\Phi$)**: Provided a major **6.14% NMSE reduction** by optimizing the compression step itself.

## Requirements
- Python 3.x
- PyTorch
- NumPy
- Matplotlib

## How to Run
1. **Data Generation**: Generate synthetic UWB-like signals using the provided utilities.
2. **Train Decision Network**: Train the FCNN to learn the signal's spatial non-zero distribution.
3. **Train Search Network**:
    - For Phase 1: Train the `SearchNetLSTM`.
    - For Phase 2: Train the `SearchNetTransformer`.
4. **Learn Sensing Matrix**: Use the `PhiLearner` and `Decoder` classes to optimize the sensing matrix $\Phi$.
5. **Evaluate**: Run the SFDLCS reconstruction function and compare results with OMP/BCS/GPSR.

## Metrics
- **NMSE**: Normalized Mean Square Error (Lower is better).
- **CRR**: Correct Recovery Rate (Higher is better).
