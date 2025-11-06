# Thermal Phase Shifters for Optical Linear Multipliers
[![Topic](https://img.shields.io/badge/Field-Silicon%20Photonics-blue)](#)
[![Simulation](https://img.shields.io/badge/Simulators-Lumerical%20%7C%20Ansys%20HEAT%20%7C%20FDTD%20%7C%20MODE-orange)](#)
[![Language](https://img.shields.io/badge/Modeling-MATLAB-yellow)](#)
[![Authors](https://img.shields.io/badge/Authors-Mukesh%20Sekar%20%7C%20Kevin%20Mienta-green)](#)

**ECE 544 — Photonic Devices and Systems**  
Colorado State University | Department of Electrical & Computer Engineering  
📧 msekar@colostate.edu · kmient1@colostate.edu  

---

## 🧭 Overview
This project explores **energy-efficient thermal phase shifters (TOPS)** within **Mach–Zehnder Interferometers (MZIs)** to enable **optical linear multipliers** for **Optical Neural Networks (ONNs)**.  
Using **Lumerical HEAT, MODE, and FDTD** along with **MATLAB**, the study investigates how **heater materials** (Al, Cu, Au, Ag) and **wire-to-waveguide distances** affect:
- **Thermal efficiency**
- **Optical loss**
- **Phase modulation precision**

Key findings:  
> 🔹 **Aluminum** provides the best thermal efficiency across all distances.  
> 🔹 **Silver** yields the lowest optical loss at 200 nm spacing.  
> 🔹 Wire distance and heater material drastically influence ONN performance scalability.

---

## 🎯 Objective
Develop and simulate **thermal phase shifters** that:
- Offer **low-power phase control** in MZI arms.  
- Balance **thermal tuning efficiency** and **optical loss**.  
- Support **scalable optical linear multiplication** for ONNs.  

---

## 🧱 Methodology

### Simulation Stack
| Domain | Tool | Purpose |
|:-------|:------|:--------|
| Thermal Analysis | **Ansys HEAT Solver** | Temperature & power sweeps |
| Optical Modes | **Lumerical MODE (FDE)** | Phase shift from ∆nₑff |
| Full 3D Optical | **Lumerical FDTD** | Waveguide loss vs. wire distance |
| System Level | **Lumerical INTERCONNECT** | MZI optical multiplication |
| Compact Modeling | **MATLAB** | Matrix-vector multiplication |

---

## 🧪 Design Setup

| Parameter | Description |
|------------|-------------|
| **Waveguide** | 220 nm × 450 nm Si strip (TE mode) |
| **Wire Materials** | Aluminum, Copper, Gold, Silver |
| **Wire Distances** | 200 nm, 500 nm, 1 µm above waveguide |
| **Simulation Region** | Si base + SiO₂ cladding + air |
| **Wavelength** | 1550 nm coherent source |

---

## 🔬 Simulation Flow

1. **HEAT Solver (Thermal Efficiency)**  
   - Apply uniform power region to wire  
   - Sweep 0.02–0.1 W and record waveguide temperature  
   - Extract ∆T vs. Power curve  

2. **MODE (FDE)**  
   - Import HEAT temperature mesh  
   - Compute effective refractive index shift using  
     Δφ = (2π × L/λ) × (Δn_eff)  
   - Determine efficiency metric: **mW/FSR**

3. **FDTD (Optical Loss)**  
   - 3D mesh simulation over 20 µm waveguide section  
   - Compute input/output power to derive loss:  
     Optical Loss = P_in − P_out  

4. **MATLAB & INTERCONNECT**  
   - Validate optical linear multiplication using MZI transfer matrix  
   - Compare compact vs. circuit-level model performance  

---

## 📈 Results

### 🧮 Thermal Efficiency (mW/FSR)
| Wire Distance | Al | Cu | Au | Ag |
|---------------:|---:|---:|---:|---:|
| 200 nm | **36.60** | 36.68 | 36.66 | 36.68 |
| 500 nm | **40.56** | 40.58 | 40.59 | 40.57 |
| 1 µm  | **46.28** | 46.31 | 46.31 | 46.32 |

**Observation:** Aluminum requires the least power to achieve a 2π phase shift → highest efficiency.

---

### 💡 Optical Loss (20 µm MZI segment)
| Wire Distance | Best Material | Comment |
|---------------|---------------|----------|
| 200 nm | **Silver** | Lowest absorption loss |
| 500 nm | — | Negligible loss (mesh-limited) |
| 1 µm | — | No significant loss detected |

---

### 🧮 Optical Linear Multiplication Validation
| θ (radians) | O₁ | O₂ |
|--------------|----|----|
| 0 | 0 | 1 |
| π/4 | 0.383 | 0.924 |
| π/2 | 0.707 | 0.707 |
| 3π/4 | 0.924 | 0.383 |
| π | 1 | 0 |

✅ MATLAB compact model and Lumerical INTERCONNECT circuit model produce identical outputs.  
Simulated insertion loss (5.32 dB) at θ = π/2 → reduces O₁ to match O₁(θ=π/4), confirming sensitivity to optical attenuation.

---

## 🧠 Key Insights
- **Aluminum heaters** maximize phase modulation per watt — ideal for high-density ONN meshes.  
- **Silver** offers the best optical transparency but lower thermal efficiency.  
- **Wire height** directly impacts power consumption; closer placement = better modulation but higher optical coupling risk.  
- **Loss impacts ONN accuracy:** 5 dB insertion loss ≈ half amplitude in MZI, distorting matrix multiplication fidelity.  

---

## ⚙️ Repository Layout

