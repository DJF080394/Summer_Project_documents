# Intelligent Conveyor Belt Tube Detection and Sorting System

### Computer vision, conveyor simulation, pneumatic sorting, and CAD-based system design

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Vision](https://img.shields.io/badge/Computer%20Vision-YOLOv8-red)
![Simulation](https://img.shields.io/badge/Simulation-PyBullet-orange)
![CAD](https://img.shields.io/badge/CAD-Fusion%20360-lightgrey)
![Robotics](https://img.shields.io/badge/Robotics-Conveyor%20Sorting-green)

---

## Overview

This repository contains the uploaded project package for an intelligent conveyor-belt tube detection and sorting system. The project combines:

- YOLO-style tube detection
- conveyor-belt simulation
- pneumatic air-jet sorting logic
- baseline controller evaluation
- PyBullet mesh and URDF assets
- Fusion 360 CAD models for the conveyor, bins, funnel, hopper, and air-jet components

The system is intended as an academic simulation and design project. It is not a validated industrial or clinical medical-waste handling system.

---

## Repository Structure

The repository is intentionally stored as a compact flat upload with source code, CAD models, result archives, figures, meshes, and URDF assets at the root level.

```text
Conveyor-Belt-Tube-Detection-System-main/
|-- 01_code.zip
|-- Conveyor Belt Project.f3d
|-- Conveyor Belt Shortened.f3d
|-- Conveyor Belt with Hopper.f3d
|-- README.md
|-- air jet.f3d
|-- baseline_results.zip
|-- bin (~recovered).f3d
|-- bin funnel.f3d
|-- figures.zip
|-- meshes.zip
`-- urdfs.zip
```

---

## File Description

| File | Description |
|---|---|
| `01_code.zip` | Main Python source code and configuration files for detection, simulation, baseline evaluation, and reinforcement-learning experiments. |
| `Conveyor Belt Project.f3d` | Full Fusion 360 CAD model of the conveyor-belt system. |
| `Conveyor Belt Shortened.f3d` | Shortened conveyor-belt CAD variant for a more compact system layout. |
| `Conveyor Belt with Hopper.f3d` | Conveyor-belt CAD model including a hopper structure. |
| `air jet.f3d` | Fusion 360 CAD model of the pneumatic air-jet sorting component. |
| `baseline_results.zip` | Baseline controller output files and evaluation results. |
| `bin (~recovered).f3d` | Recovered Fusion 360 CAD model of the collection bin. |
| `bin funnel.f3d` | Fusion 360 CAD model of the bin funnel component. |
| `figures.zip` | Figures and visual materials used for reporting and project explanation. |
| `meshes.zip` | Mesh assets used by the simulation environment. |
| `urdfs.zip` | URDF files used for PyBullet simulation models. |
| `README.md` | Project overview and repository guide. |

---

## Project Pipeline

1. Tube-like objects move through the conveyor-belt system.
2. The detection script identifies tube objects and estimates their class, position, and confidence.
3. The controller decides whether a pneumatic air jet should fire.
4. The simulation evaluates sorting behaviour and controller response quality.
5. Baseline results and visual materials are stored in the result and figure archives.
6. CAD files provide the mechanical design reference for the conveyor, hopper, bin, funnel, and air-jet assemblies.

---

## Code Package

The source code is stored in:

```text
01_code.zip
```

After downloading or cloning the repository, unzip this file before running the Python scripts:

```bash
unzip 01_code.zip
```

Depending on the extracted folder name, typical scripts may include:

```bash
python sample_test.py
python evaluate_baselines.py
python rl_training_ppo.py
python rl_training_sac.py
```

Some scripts may require the contents of `meshes.zip`, `urdfs.zip`, or `baseline_results.zip` to be extracted into the expected local paths before running.

---

## CAD Models

The main mechanical design files are provided as Fusion 360 `.f3d` files:

- `Conveyor Belt Project.f3d`
- `Conveyor Belt Shortened.f3d`
- `Conveyor Belt with Hopper.f3d`
- `air jet.f3d`
- `bin (~recovered).f3d`
- `bin funnel.f3d`

These files describe the conveyor structure, sorting mechanism, hopper, collection bin, funnel, and air-jet components used in the system design.

---

## Simulation Assets

The PyBullet simulation assets are stored in:

```text
meshes.zip
urdfs.zip
```

Extract these archives when reproducing or modifying the simulation environment.

---

## Results and Figures

Baseline outputs and project visuals are stored in:

```text
baseline_results.zip
figures.zip
```

These archives contain evaluation outputs, plots, diagrams, and other supporting visual materials for the project report.

---

## Notes

- Large assets are stored as `.zip` archives to keep the repository root compact.
- Fusion 360 is required to open or modify the `.f3d` CAD files.
- PyBullet simulation scripts may need local path adjustments after extracting the archives.
- The repository is structured for upload and review rather than direct one-command reproduction.

---

## Author

**Jianfeng Du**  
MSc Robotics Advanced Project  
University of Birmingham

Computer Vision | Conveyor Simulation | CAD Design | Pneumatic Sorting | Robotics
