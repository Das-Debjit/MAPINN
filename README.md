# MAPINN: Multi-Scale Adaptive Physics-Informed Neural Network
### M.Sc. Thesis | Vellore Institute of Technology, Chennai | April 2026

> *A neural network framework for solving nonlinear PDEs characterized by sharp interfaces and excitable dynamics — achieving 100× error reduction over standard PINNs on the FitzHugh–Nagumo system.*

---

## 📌 Abstract

Physics-Informed Neural Networks (PINNs) struggle with nonlinear PDE systems involving sharp interfaces, multi-scale behavior, or rapidly propagating waves due to spectral bias and inefficient collocation point distribution.

**MAPINN** addresses these limitations by combining three components into a unified physics-informed learning framework:
1. **Fourier feature encoding** — captures high-frequency solution components
2. **Multi-branch architecture** — decomposes solution into low, mid, and high frequency branches
3. **Adaptive residual-based sampling** — focuses training on physically active regions (interfaces, excitation fronts)

---

## 📊 Key Results

| PDE System | Baseline PINN | Fourier PINN | **MAPINN** |
|---|---|---|---|
| Allen–Cahn (Phase-field) | 13.47% | 5.42% | **2.96%** |
| FitzHugh–Nagumo (Excitable) | 92.13% | 90.03% | **0.78%** |

> MAPINN achieves **>100× error reduction** on excitable wave dynamics where standard PINNs completely fail (92.13% → 0.78%).

---

## 🏗️ Architecture

```
Input (x, t)
     │
     ▼
Fourier Feature Encoding
[sin(ω₁x), cos(ω₁x), sin(ω₂x), cos(ω₂x), ...]
     │
     ├──► Low-Frequency NN  (ωL = 1)
     ├──► Mid-Frequency NN  (ωM = 5)
     └──► High-Frequency NN (ωH = 20)
              │
              ▼
     Multi-Scale Feature Fusion (Σ)
              │
              ▼
         Output uθ(x, t)
```

**Training Strategy:**
- Stage 1: Adam optimizer with uniform collocation sampling
- Stage 2: L-BFGS with adaptive residual-based resampling

---

## 📐 Governing Equations

### Allen–Cahn Phase-Field Equation
```
∂u/∂t = ε² ∂²u/∂x² − (u³ − u)
```
Models sharp interface evolution in phase separation and materials science.

### FitzHugh–Nagumo Excitable System
```
∂u/∂t = D ∂²u/∂x² + u − u³/3 − v
∂v/∂t = ε(u + a − bv)
```
Models excitable wave propagation in biological and chemical systems.

---

## 🛠️ Tech Stack

| Component | Tool |
|---|---|
| Deep Learning Framework | PyTorch |
| Automatic Differentiation | torch.autograd |
| Optimizers | Adam + L-BFGS |
| Numerical Ground Truth | Spectral solver (N=512 modes) |
| Visualization | Matplotlib |
| Environment | Google Colab / CUDA GPU |

---

## 📁 Repository Structure

```
MAPINN/
│
├── notebooks/
│   └── MAPINN_COMPLETE_FINAL.ipynb   ← Full implementation
│
├── data/
│   ├── allen_cahn_ground_truth.npz
│   └── fhn_ground_truth.npz
│
├── models/                            ← Pretrained checkpoints
│   ├── mapinn_allen_cahn.pth
│   ├── mapinn_fhn.pth
│   └── (baseline & Fourier variants)
│
├── results/                           ← Plots & metrics
│
├── DEBJIT_THESIS.pdf                  ← M.Sc. dissertation
├── poster final debjit.pdf            ← Research poster
├── README.md
└── requirements.txt
```

---

## 🚀 How to Run

### Option 1 — Google Colab (Recommended)
1. Open `MAPINN_COMPLETE_FINAL.ipynb` in Google Colab
2. Set runtime to **GPU** (Runtime → Change runtime type → T4 GPU)
3. Run all cells

### Option 2 — Local
```bash
git clone https://github.com/Das-Debjit/MAPINN.git
cd MAPINN
pip install -r requirements.txt
jupyter notebook MAPINN_COMPLETE_FINAL.ipynb
```

---

## 📈 Evaluation Metrics

- **Relative L2 Error** — primary global error metric
- **Spectral Error Decomposition** — frequency-wise error analysis
- **Interface Fidelity** — sharpness and location accuracy of phase boundaries
- **Wave Propagation Accuracy** — speed, amplitude, and arrival time of excitation fronts

---

## 🔬 Contributions

1. Novel **multi-branch PINN architecture** decomposing PDE solutions into frequency-aware subnetworks
2. Integration of **Fourier feature encoding** with **adaptive residual sampling** in a unified framework
3. Physics-aware evaluation beyond global error norms — spectral decomposition and interface tracking
4. Demonstrated as a **surrogate model** for real-time phase-boundary tracking (battery electrode application)

---

## 📄 Citation

If you use this work, please cite:

```
Das, Debjit. "MAPINN: A Multi-Scale Adaptive Physics-Informed Neural Network 
for Interface-Dominated and Excitable PDE Systems." 
M.Sc. Dissertation, Department of Mathematics, School of Advanced Sciences, 
Vellore Institute of Technology, Chennai. April 2026.
```

---

## 🙏 Acknowledgements

Supervised by **Dr. Pankaj Shukla**, Assistant Professor, School of Advanced Sciences, VIT Chennai.

---

## 👤 Author

**Debjit Das** | Reg. No: 24MDT1086
- 📧 debjitdas1409@gmail.com
- 💼 [LinkedIn](https://linkedin.com/in/debjitdas82)
- 🐙 [GitHub](https://github.com/Das-Debjit)
- 🌐 [Portfolio](https://debjit-das-portfolio.vercel.app/)
