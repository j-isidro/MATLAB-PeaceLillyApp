# Peace Lily Optimizer — MATLAB App Designer

## Project Overview
EcoFlow is an interactive MATLAB App Designer application that calculates the optimal number of Peace Lily plants needed to balance CO₂ output in an occupied space. The app takes user inputs for room occupancy, volume, and light level, then uses two core numerical methods — **Newton-Raphson root finding** and **linear interpolation** — to solve for the plant count that achieves equilibrium between human CO₂ output and plant absorption.

The result is displayed in real time as an efficiency score parabola, with the optimal plant count marked at peak efficiency.


## App Interface
![EcoFlow App Interface](https://github.com/user-attachments/assets/2b2ed9dd-2700-478c-9efe-d5f47a7ffad0)

---

## Objectives
- Apply numerical methods (Newton-Raphson, interpolation) to a real-world environmental optimization problem
- Build a functional interactive Graphical User Interface (GUI) using MATLAB App Designer
- Dynamically update calculations and visualizations based on user inputs

---

## How It Works

The app solves the following equilibrium equation for the number of plants *x*:

```
f(x) = (People × CO₂ Rate) - (x × Plant Absorption Rate) = 0
```

**Inputs:**
- Number of occupants (slider, 1–50 people)
- Room volume (m³)
- Light level (Lux)

**Output:**
- Optimal number of Peace Lilies to achieve CO₂ equilibrium
- Efficiency score parabola showing performance relative to the optimal count

---

## Numerical Methods

### 1. Linear Interpolation — `getAbsorptionRate()`
Plant CO₂ absorption rate varies with light intensity. A lookup table of scientifically approximated light-to-absorption values is used, with `interp1()` performing linear interpolation between known data points to estimate absorption at any given Lux value.

```
lightTable = [0, 0; 100, 0.00003; 300, 0.00008; 1000, 0.00015]
```

### 2. Newton-Raphson Root Finding — `solveForPlants()`
The Newton-Raphson method iteratively solves for the number of plants where the equilibrium function equals zero:

```
x_new = x - f(x) / f'(x)
```

- Initial guess: x = 10 plants
- Tolerance: 0.01
- Max iterations: 50
- Converges rapidly due to the linear nature of f(x)

---

## App Architecture

Built using MATLAB's object-oriented `classdef` structure with App Designer:

- `getAbsorptionRate()` — interpolates plant absorption from light input
- `solveForPlants()` — runs Newton-Raphson to find equilibrium plant count
- `updateApp()` — recalculates and re-renders the plot on any input change
- `createComponents()` — builds all UI elements (slider, input fields, axes, labels)

All inputs are live — changing any value immediately triggers recalculation and replot.

---

## Tools & Languages
- **MATLAB App Designer** — GUI framework
- **MATLAB** — numerical computation, plotting
- **Numerical Methods:** Linear interpolation (`interp1`), Newton-Raphson iteration

---

## Skills Demonstrated
- MATLAB App Designer (UI layout, event-driven callbacks)
- Numerical methods implementation from scratch
- Real-time data visualization with dynamic plot updates
