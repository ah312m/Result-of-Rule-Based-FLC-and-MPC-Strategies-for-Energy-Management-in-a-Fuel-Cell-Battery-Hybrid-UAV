# Result Repository for Rule-Based, Fuzzy Logic, and MPC Energy Management Strategies in a Fuel-Cell/Battery Hybrid UAV

## Overview

This repository contains the complete simulation-result archive associated with the paper:

**A Comparative Study of Rule-Based, Fuzzy Logic, and Model Predictive Control Strategies for Energy Management in a Fuel-Cell/Battery Hybrid Unmanned Aerial Vehicle**

The study compares three energy management strategies (EMS) for a hybrid unmanned aerial vehicle (UAV) powered by a proton-exchange-membrane fuel cell (PEMFC) and a lithium-ion battery (LIB):

1. **Rule-Based EMS (RB)**
2. **Fuzzy Logic Controller EMS (FLC)**
3. **Model Predictive Controller EMS (MPC)**

The purpose of this repository is to provide the full set of time-domain figures and numerical summaries used to support the comparative analysis. The repository is organized to allow the reader to inspect each controller independently at different initial battery state-of-charge (SoC) values and under both nominal and disturbed operating conditions.

---

## Study Configuration

All result folders correspond to simulations performed using the same hybrid UAV plant model, mission profile, and operating assumptions. This ensures that the differences observed in the results are caused by the EMS strategy itself rather than by different simulation settings.

The comparison includes:

- **3 EMS strategies:** Rule-Based, Fuzzy Logic, and MPC
- **11 initial battery SoC values:**  
  `0.05`, `0.15`, `0.25`, `0.35`, `0.45`, `0.50`, `0.55`, `0.65`, `0.75`, `0.85`, and `0.95`
- **2 operating conditions for each SoC value:**
  - **Nominal condition:** the UAV load follows the reference mission profile without stochastic perturbation.
  - **Disturbed condition:** the UAV load is subjected to stochastic disturbance, representing wind and atmospheric effects.
- **66 total simulation cases:**  
  `3 controllers × 11 initial SoC values × 2 operating conditions`

The results include both graphical time-domain responses and a text-based EMS summary for each controller/SoC case.

---

## Repository Structure

The repository is organized by controller type and initial battery SoC. Each folder name has the following form:

```text
<controller>_<initial_SoC>
```

where:

- `<controller>` indicates the EMS strategy:
  - `MPC` = Model Predictive Control
  - `fuzzy` = Fuzzy Logic Controller
  - `rule` = Rule-Based Controller
- `<initial_SoC>` indicates the initial battery state of charge in percent-like notation:
  - `05` = initial SoC of 0.05
  - `15` = initial SoC of 0.15
  - `25` = initial SoC of 0.25
  - ...
  - `95` = initial SoC of 0.95

For example:

```text
MPC_05     → MPC controller with initial battery SoC = 0.05
fuzzy_50   → Fuzzy logic controller with initial battery SoC = 0.50
rule_95    → Rule-based controller with initial battery SoC = 0.95
```

The main folder groups are:

```text
MPC_05,   MPC_15,   MPC_25,   MPC_35,   MPC_45,   MPC_50,   MPC_55,   MPC_65,   MPC_75,   MPC_85,   MPC_95
fuzzy_05, fuzzy_15, fuzzy_25, fuzzy_35, fuzzy_45, fuzzy_50, fuzzy_55, fuzzy_65, fuzzy_75, fuzzy_85, fuzzy_95
rule_05,  rule_15,  rule_25,  rule_35,  rule_45,  rule_50,  rule_55,  rule_65,  rule_75,  rule_85,  rule_95
```

---

## Contents of Each Result Folder

Each folder contains:

1. **Numbered figure files**
   - The figures are named numerically, for example:
     ```text
     figure_01.png
     figure_02.png
     figure_03.png
     ...
     ```
   - The figure number does not directly describe the plot title; therefore, the figure-to-content mapping is explained in the tables below.

2. **EMS Summary text file**
   - Each folder also contains a text file summarizing the EMS result for that specific controller and initial SoC value.
   - The summary file provides the main numerical indicators used to evaluate the controller behavior, such as voltage regulation, battery stress, hydrogen consumption, internal battery losses, and cumulative charge/discharge behavior.

---

## MPC Folder Contents

Each `MPC_xx` folder contains **11 figures** and one EMS summary text file.

The 11 figures are divided into:

- **Figures 1–5:** nominal operating condition
- **Figures 6–10:** disturbed operating condition
- **Figure 11:** direct comparison between nominal and disturbed conditions

### Figure Mapping for MPC Folders

| Figure file | Operating condition | Content |
|---|---|---|
| `figure_01.png` | Nominal | Power sharing and DC-bus regulation |
| `figure_02.png` | Nominal | Fuel-cell reference tracking |
| `figure_03.png` | Nominal | Battery internal variables |
| `figure_04.png` | Nominal | Energy-balance indicators |
| `figure_05.png` | Nominal | MPC decision variables — optimal cost and admissible reference range |
| `figure_06.png` | Disturbed | Power sharing and DC-bus regulation |
| `figure_07.png` | Disturbed | Fuel-cell reference tracking |
| `figure_08.png` | Disturbed | Battery internal variables |
| `figure_09.png` | Disturbed | Energy-balance indicators |
| `figure_10.png` | Disturbed | MPC decision variables — optimal cost and admissible reference range |
| `figure_11.png` | Nominal vs. Disturbed | Comparative plot between nominal and disturbed operation for the same MPC/SoC case |

### Interpretation of MPC Figures

The MPC result set includes one additional figure category that is not available in the rule-based and fuzzy folders: **MPC decision variables — optimal cost and admissible reference range**. This figure is specific to the predictive controller because MPC computes an optimal fuel-cell reference by evaluating candidate control decisions over a prediction horizon. Therefore, the MPC-specific figure visualizes the internal optimization behavior, including the cost evolution and the admissible range of the fuel-cell power reference.

---

## Fuzzy Logic Controller Folder Contents

Each `fuzzy_xx` folder contains **9 figures** and one EMS summary text file.

The 9 figures are divided into:

- **Figures 1–4:** nominal operating condition
- **Figures 5–8:** disturbed operating condition
- **Figure 9:** direct comparison between nominal and disturbed conditions

### Figure Mapping for Fuzzy Folders

| Figure file | Operating condition | Content |
|---|---|---|
| `figure_01.png` | Nominal | Power sharing and DC-bus regulation |
| `figure_02.png` | Nominal | Fuel-cell reference tracking |
| `figure_03.png` | Nominal | Battery internal variables |
| `figure_04.png` | Nominal | Energy-balance indicators |
| `figure_05.png` | Disturbed | Power sharing and DC-bus regulation |
| `figure_06.png` | Disturbed | Fuel-cell reference tracking |
| `figure_07.png` | Disturbed | Battery internal variables |
| `figure_08.png` | Disturbed | Energy-balance indicators |
| `figure_09.png` | Nominal vs. Disturbed | Comparative plot between nominal and disturbed operation for the same fuzzy/SoC case |

### Interpretation of Fuzzy Figures

The fuzzy controller figures show how the Mamdani-type fuzzy EMS distributes the load demand between the fuel cell and battery based on linguistic control rules. The plots are useful for observing the smoothness of the fuel-cell command, the degree of battery assistance, and the controller response to stochastic load disturbance.

Unlike MPC, the fuzzy controller does not solve an online optimization problem; therefore, there is no figure for optimal cost or admissible control range.

---

## Rule-Based Controller Folder Contents

Each `rule_xx` folder contains **9 figures** and one EMS summary text file.

The 9 figures are divided into:

- **Figures 1–4:** nominal operating condition
- **Figures 5–8:** disturbed operating condition
- **Figure 9:** direct comparison between nominal and disturbed conditions

### Figure Mapping for Rule-Based Folders

| Figure file | Operating condition | Content |
|---|---|---|
| `figure_01.png` | Nominal | Power sharing and DC-bus regulation |
| `figure_02.png` | Nominal | Fuel-cell reference tracking |
| `figure_03.png` | Nominal | Battery internal variables |
| `figure_04.png` | Nominal | Energy-balance indicators |
| `figure_05.png` | Disturbed | Power sharing and DC-bus regulation |
| `figure_06.png` | Disturbed | Fuel-cell reference tracking |
| `figure_07.png` | Disturbed | Battery internal variables |
| `figure_08.png` | Disturbed | Energy-balance indicators |
| `figure_09.png` | Nominal vs. Disturbed | Comparative plot between nominal and disturbed operation for the same rule/SoC case |

### Interpretation of Rule-Based Figures

The rule-based controller figures represent the behavior of the deterministic EMS under fixed operating rules and SoC thresholds. These results are useful as a baseline for evaluating the improvements obtained by fuzzy logic and MPC strategies. The rule-based plots help illustrate the limitations of fixed-threshold control under disturbed loading, especially in terms of DC-bus voltage regulation, fuel-cell ramping behavior, and battery stress.

---

## Description of the Main Figure Categories

### 1. Power Sharing and DC-Bus Regulation

This figure shows how the total UAV load power is shared between the PEMFC and the battery. It also shows the DC-bus voltage behavior relative to its reference value. This plot is central for evaluating the controller ability to maintain electrical stability while satisfying the propulsion load demand.

Typical signals in this category include:

- UAV load power
- Fuel-cell output power
- Battery power contribution
- DC-bus voltage
- DC-bus voltage reference or regulation band

---

### 2. Fuel-Cell Reference Tracking

This figure evaluates how accurately and smoothly the fuel cell follows the reference command generated by the EMS. It is important because PEMFC systems have limited dynamic response and should not be forced to follow highly abrupt load variations.

Typical signals in this category include:

- Fuel-cell reference power
- Actual fuel-cell output power
- Fuel-cell tracking error
- Saturation or emergency-limiting events
- Fuel-cell efficiency
- Hydrogen consumption rate
- Fuel-cell ramp-rate behavior

---

### 3. Battery Internal Variables

This figure focuses on the battery-side response. It is used to assess the stress imposed on the lithium-ion battery and the role of the battery as a transient energy buffer.

Typical signals in this category include:

- Battery open-circuit voltage
- Battery terminal voltage
- Battery current
- Battery power
- Battery C-rate
- State of charge
- Cumulative discharge energy
- Cumulative charge energy
- Internal battery losses

---

### 4. Energy-Balance Indicators

This figure illustrates the energy-flow consistency of the hybrid system. It is useful for understanding whether the combined PEMFC/battery system is supplying the requested load and how the DC-bus capacitor reacts to short-term energy mismatch.

Typical signals in this category include:

- Net injected power
- Supply deficit
- DC-bus voltage derivative
- Equivalent stored energy in the DC-bus capacitor
- Cumulative load energy
- Cumulative fuel-cell energy
- Cumulative battery charge and discharge energy

---

### 5. MPC Decision Variables — Optimal Cost and Admissible Reference Range

This figure exists only in the `MPC_xx` folders. It shows the internal predictive decision-making process of the MPC controller.

Typical signals in this category include:

- Optimal cost function value
- Lower and upper admissible fuel-cell reference limits
- Selected optimal fuel-cell reference
- Filtered load demand
- Rate of change of selected reference or load demand

This plot is important for verifying that the MPC decision remains feasible and that the selected fuel-cell command stays within the allowed physical and operational constraints.

---

### 6. Nominal-vs-Disturbed Comparison

The final figure in each folder compares the nominal and disturbed responses for the same controller and initial SoC value. This comparison is useful for evaluating robustness against stochastic load variations.

For MPC folders, this is:

```text
figure_11.png
```

For fuzzy and rule-based folders, this is:

```text
figure_09.png
```

---

## EMS Summary Files

Each folder includes an EMS summary text file. The summary file is intended to provide a compact numerical description of the corresponding simulation case.

The summary files should be used together with the figures. While the figures provide time-domain interpretation, the summary files provide numerical performance indicators for cross-comparison.

The EMS summary may include indicators such as:

- Mean absolute DC-bus voltage error
- RMS DC-bus voltage error
- Maximum DC-bus voltage transient
- Final DC-bus voltage
- Hydrogen consumption
- Maximum battery current
- Maximum battery C-rate
- Battery internal losses
- Cumulative battery discharge energy
- Cumulative battery charge energy

These indicators support quantitative comparison across controller type, initial SoC, and load condition.

---

## Recommended Reading Procedure

To analyze the repository systematically, the following procedure is recommended:

1. **Select the controller type**
   - Choose one of `MPC`, `fuzzy`, or `rule`.

2. **Select the initial SoC case**
   - For example, use `MPC_50` to inspect the MPC result at initial SoC = 0.50.

3. **Inspect the nominal figures**
   - For MPC: `figure_01.png` to `figure_05.png`
   - For fuzzy/rule-based: `figure_01.png` to `figure_04.png`

4. **Inspect the disturbed figures**
   - For MPC: `figure_06.png` to `figure_10.png`
   - For fuzzy/rule-based: `figure_05.png` to `figure_08.png`

5. **Inspect the nominal-vs-disturbed comparison**
   - For MPC: `figure_11.png`
   - For fuzzy/rule-based: `figure_09.png`

6. **Read the EMS summary file**
   - Use the numerical metrics to compare the controller performance at the same initial SoC.

7. **Repeat for other SoC values**
   - This allows evaluation of robustness over the complete battery operating range.

---

## Comparative Use of the Repository

The repository can be used to answer questions such as:

- Which EMS gives the best DC-bus voltage regulation?
- Which controller produces the lowest battery current stress?
- Which strategy gives the lowest hydrogen consumption?
- How does initial battery SoC affect controller performance?
- How does each EMS behave under disturbed load conditions?
- Does the controller performance remain consistent over low, medium, and high initial SoC values?
- How much additional information does the MPC optimization layer provide compared with fuzzy and rule-based EMS?

---

## Result Archive Size

Based on the folder organization:

- **MPC results:**  
  `11 SoC cases × 11 figures = 121 figures`

- **Fuzzy logic results:**  
  `11 SoC cases × 9 figures = 99 figures`

- **Rule-based results:**  
  `11 SoC cases × 9 figures = 99 figures`

Therefore, the repository contains approximately:

```text
319 result figures + 33 EMS summary files
```

This makes the repository a complete extended-result archive for the comparative study.

---

## Notes on Figure Numbering

The figure files are intentionally stored using numerical names such as `figure_01.png`, `figure_02.png`, and so on. This avoids long file names and keeps the folder structure compact. Because the numerical names do not directly describe the content, the mapping tables in this README should be used when interpreting the figures.

---

## Reproducibility Purpose

The main purpose of this repository is to improve reproducibility and transparency. The paper presents selected representative plots and summarized tables, while this repository provides the complete figure set for every controller, every initial SoC value, and both operating conditions.

This allows researchers to verify the reported conclusions, inspect individual operating cases, and compare the controllers over the full simulation envelope rather than only through selected examples.

---

## License

This repository is released under the MIT License. See the `LICENSE` file for details.

---

## Suggested Citation

If this repository is used in academic work, please cite the associated paper:

**A Comparative Study of Rule-Based, Fuzzy Logic, and Model Predictive Control Strategies for Energy Management in a Fuel-Cell/Battery Hybrid Unmanned Aerial Vehicle**

