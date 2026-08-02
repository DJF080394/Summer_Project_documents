# Intelligent Conveyor Sorting Using YOLO and Reinforcement Learning for Medical Waste

### Sustainable automated plastic sorting using computer vision, reinforcement learning, PyBullet simulation, and robotic disassembly planning

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![RL](https://img.shields.io/badge/Reinforcement%20Learning-PPO%20%7C%20SAC-green)
![Simulation](https://img.shields.io/badge/Simulation-PyBullet-orange)
![Vision](https://img.shields.io/badge/Computer%20Vision-YOLOv8-red)
![Robotics](https://img.shields.io/badge/Robot-UR5%20%2B%20Robotiq85-lightgrey)

---

## Overview

This repository contains the lightweight GitHub version of an MSc robotics project on simulation-based medical tube sorting and disassembly. The project combines:

- computer vision for tube detection
- PyBullet-based conveyor simulation
- timing-aware pneumatic sorting control
- PPO and SAC reinforcement-learning policies
- Performance Metrics for controller comparison
- UR5-style robotic disassembly planning

The system is designed for a controlled, non-clinical stream of clean tube-like plastic objects. It should be understood as a reproducible simulation-based sorting study rather than a validated industrial medical-waste handling system.

---

## System Architecture

![YOLO-to-control tube sorting workflow](./results/system_overview_schematic.png)

The pipeline connects perception, control, simulation, and planned disassembly:

1. Tube-like plastic objects enter the conveyor scene.
2. YOLO detects whole tube objects and returns class, position, confidence, and short-term stability.
3. A timing-aware state is constructed from the detection output, conveyor motion, target jet position, and nozzle-window status.
4. The timing baseline, PPO, or SAC controller selects either no-action or one of five air-jet commands.
5. PyBullet simulates the sorting outcome and records reward, correct response, no response, and wrong response.
6. Sorted tubes are collected in bins before the planned UR5-style robot disassembly stage.

---

## Technologies Used

- Python
- PyBullet
- Gymnasium
- Stable-Baselines3
- OpenCV
- YOLOv8-style detection
- NumPy
- Matplotlib
- URDF-based simulation assets

---

## Reinforcement Learning Formulation

The sorting controller is formulated as a Markov Decision Process:

```text
M = <S, A, P, R, gamma>
```

### Timing-Aware State

The state links perception to conveyor timing:

```python
[y_t, class_t, confidence_t, target_jet_y, delta_y,
 x_t, v_x_t, v_y_t, in_nozzle_window, already_fired]
```

### Action Space

The controller uses six pneumatic commands:

```python
0 = Jet 1
1 = Jet 2
2 = Jet 3
3 = Jet 4
4 = Jet 5
5 = No action
```

PPO selects directly from this discrete action set. SAC produces a continuous scalar output that is floored and clipped into the same six-command interface.

### Controllers

- **Timing baseline**: rule-based controller using class-to-jet mapping and nozzle-window timing.
- **PPO**: discrete actor-critic reinforcement-learning controller.
- **SAC**: entropy-regularised reinforcement-learning controller with discretised pneumatic output.

---

## Results Summary

The current evaluation uses **Performance Metrics** measured only when a tube is inside the physically relevant nozzle-window interval. Ordinary conveyor travel before the tube reaches the jet is not counted as a controller response.

![Controller response metrics](./results/rl_100k_controller_metrics.png)

| Controller | Deterministic Correct Response | Randomised Correct Response | Main Observation |
|---|---:|---:|---|
| Timing baseline | 100.0% | 100.0% | Calibrated reference controller |
| PPO | 75.0% | 50.0% | Learns useful nozzle-window responses after reward correction |
| SAC | 50.0% | 50.0% | Responsive but conservative under the current setup |

Key findings:

- Reward convergence alone is not sufficient to prove useful sorting behaviour.
- The corrected PPO run avoids the earlier full no-response collapse.
- SAC remains responsive but leaves many relevant nozzle-window decisions as no-response.
- The timing baseline is the strongest reference controller in the present simulation.
- Physical prototype testing and richer final-bin validation are still required.

---

## Repository Structure

```text
Conveyor-Belt-Tube-Detection-System-main/
|-- code/
|   |-- tube_detection_project.py
|   |-- sample_test.py
|   |-- object_deyection.py
|   |-- evaluate_baselines.py
|   |-- rl_training_ppo.py
|   |-- rl_training_sac.py
|   |-- train_final_rl_controllers.py
|   |-- run_decision_zone_formal_training.py
|   |-- summarise_formal_outputs.py
|   `-- evaluate_formal_outputs.py
|-- data/
|   `-- README.md
|-- docs/
|   |-- GIT_WORKFLOW.md
|   |-- large_files_not_uploaded.csv
|   `-- paper_chinese_translation_and_analysis.md
|-- figures/
|-- results/
|   |-- system_overview_schematic.png
|   |-- rl_100k_controller_metrics.png
|   |-- rl_100k_state_action_heatmaps.png
|   |-- rl_100k_baseline_ppo_sac_comparison.png
|   `-- rl_100k_baseline_ppo_sac_metrics.csv
|-- tools/
|-- CONTRIBUTING.md
|-- requirements.txt
`-- README.md
```

Large local archives, CAD files, report builds, and temporary outputs are kept outside the lightweight GitHub-facing structure and are ignored by Git where appropriate.

---

## Main Scripts

| Script | Purpose |
|---|---|
| `code/tube_detection_project.py` | Main conveyor and tube detection project script |
| `code/sample_test.py` | Simulated camera view, YOLO display, and conveyor scene testing |
| `code/object_deyection.py` | Synthetic object detection and annotation workflow |
| `code/evaluate_baselines.py` | Timing baseline evaluation |
| `code/rl_training_ppo.py` | PPO training entry point |
| `code/rl_training_sac.py` | SAC training entry point |
| `code/train_final_rl_controllers.py` | Shared PPO/SAC training helper |
| `code/run_decision_zone_formal_training.py` | Formal decision-zone training and evaluation workflow |
| `code/summarise_formal_outputs.py` | CSV and metric summarisation |
| `code/evaluate_formal_outputs.py` | Formal output evaluation |

---

## Setup

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

Typical commands:

```bash
python code/sample_test.py
python code/evaluate_baselines.py
python code/rl_training_ppo.py
python code/rl_training_sac.py
```

Some scripts may require restored datasets, model weights, URDF files, or adjusted local paths before full reproduction. Large files excluded from the lightweight upload are listed in:

```text
docs/large_files_not_uploaded.csv
```

---

## Future Work

- Physical conveyor prototype validation
- More realistic pneumatic delay and air-jet force modelling
- Domain randomisation across belt speed, friction, mass, lighting, and detection confidence
- Final-bin success and throughput measurement
- False rejection and air-cost-per-correct-sort metrics
- Improved reward tuning and repeated-seed RL evaluation
- Higher-fidelity robotic cap disassembly with torque, friction, and grasp-force validation

---

## Author

**Jianfeng Du**  
MSc Robotics Advanced Project  
University of Birmingham

Computer Vision | Reinforcement Learning | PyBullet Simulation | Robotic Disassembly | Sustainable Automation
