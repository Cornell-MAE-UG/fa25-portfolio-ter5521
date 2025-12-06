---
layout: default
title: Linear Actuator
description: Linear Actuator Lifting Design
technologies: Drawing
image: "/assets/images/Linear Actuator.jpg"
---
# ENGRD 2020: Linear Actuator Mechanism Design Problem

## Step 1: Rigid Body Design & Analysis

### A. Problem Definition

**Objective:**
Design a frame/mechanism to lift the maximum possible weight to the highest possible height within a constrained 2D design space.

**Constraints:**
* **Design Space:** 150 cm (Length) x 50 cm (Height).
* **Components:**
    * 1 Rigid Bar (Beam).
    * 3 Pin supports (2 ground-mounted at A and B).
    * 1 Linear Actuator connecting ground point B to beam point C.

**Design Degrees of Freedom:**
1.  **Bar Length ($L$):** 140 cm.
2.  **Ground Geometry:** Pin A is the main pivot at the origin (0,0). Pin B (actuator base) is on the ground at (36 cm, 0).
3.  **Actuator Connection:** The actuator connects to the beam at Point C, located 70 cm from the pivot A.

**Operational Assumption:**
* **Operating Range:** The mechanism is designed to lift from a minimum tip height of **20 cm** up to a maximum of **50 cm**.
* **Reasoning:** Starting from $y=0$ results in a zero moment arm (locking the mechanism). Starting at 20 cm provides the necessary initial leverage.
* **Actuator Fit:** The distance between B and C at the start (20 cm tip height) is **34.8 cm**, which perfectly accommodates the 34 cm retracted length of the actuator.

### B. Static Analysis (Rigid Body)

**Selected Actuator:**
* **Model:** Tolomatic IMA 55 RN05
* **Max Thrust Force ($F_{act}$):** 35.81 kN (35,810 N)

**Free Body Diagram (FBD) Logic:**
The bar is modeled as a lever pivoting at A. The capacity is determined by the **weakest position** (Start of Lift), where the moment arm is smallest.
* **Equilibrium:** $\sum M_A = 0$

**Calculations (Critical Case: Start of Lift @ 20 cm height):**
* **Beam Angle ($\theta$):** $\sin^{-1}(20/140) \approx 8.2^\circ$.
* **Geometry Check:**
    * Point C is at $(70\cos 8.2^\circ, 70\sin 8.2^\circ) \approx (69.3, 10.0)$.
    * Point B is at $(36, 0)$.
    * Vector BC is $(33.3, 10.0)$.
* **Moment Arm of Actuator ($d_{act}$):** Calculated as perpendicular distance from A to line BC:
    $$d_{act} = \frac{|x_C y_B - y_C x_B|}{\text{Length}_{BC}} = \frac{|(69.3)(0) - (10.0)(36)|}{\sqrt{33.3^2 + 10^2}} \approx \mathbf{10.36 \text{ cm}}$$
* **Moment Arm of Weight ($d_{load}$):** $140 \cos(8.2^\circ) \approx$ **138.6 cm**.

$$\sum M_A = 0$$
$$F_{act} \cdot d_{act} - W_{max} \cdot d_{load} = 0$$
$$35,810 \text{ N} \cdot 10.36 \text{ cm} = W_{max} \cdot 138.6 \text{ cm}$$

$$W_{max} = \frac{370,991}{138.6} \approx \mathbf{2,677 \text{ N}}$$

**Final Performance:**
* **Max Lift Height:** 50 cm
* **Max Weight Capacity:** 2.68 kN (2,677 N)
*(Note: While the capacity increases to ~6.4 kN at the top, the rated capacity must be limited to what the system can lift from the start.)*

### C. Final Mechanism Design

![Mechanism Sketch]({{ "/assets/images/Linear Actuator.jpg" | relative_url }}){: .project-image}
*Figure 1: Schematic of the lifting mechanism showing the critical starting position.*

---

## Step 2: Deformable Beam Design

### A. Deflection Analysis

The bar is modeled as a deformable beam under transverse loading. We check deflection under the rated load of **2,677 N**.

**Assumptions:**
1.  **Beam Model:** Simply supported beam with a center support and overhanging load.
    * **Pin Support (A):** At $x=0$.
    * **Roller Support (C):** At $x=0.7 \text{ m}$.
    * **Load (P):** At tip $x=1.4 \text{ m}$.
2.  **Forces:** Considering only transverse components of the actuator force and weight.
3.  **Material:** Steel ($E = 200$ GPa).

**Load & Reaction Calculation:**
* Load $P = 2,677 \text{ N}$ (down at $x=1.4$)
* $\sum M_A = 0 \Rightarrow R_C(0.7) - 2677(1.4) = 0 \Rightarrow R_C = 5,354 \text{ N} (\uparrow)$
* $\sum F_y = 0 \Rightarrow R_A + 5354 - 2677 = 0 \Rightarrow R_A = -2,677 \text{ N} (\downarrow)$

**Elastic Curve Derivation (Singularity Functions):**
$$EI y'' = -2677 x + 5354 \langle x - 0.7 \rangle^1$$

Integrate for Slope ($EI \theta$):
$$EI y' = -1338.5 x^2 + 2677 \langle x - 0.7 \rangle^2 + C_1$$

Integrate for Deflection ($EI y$):
$$EI y = -446.2 x^3 + 892.3 \langle x - 0.7 \rangle^3 + C_1 x + C_2$$

**Boundary Conditions:**
1.  At $x=0, y=0 \Rightarrow \mathbf{C_2 = 0}$
2.  At $x=0.7, y=0$:
    $$0 = -446.2(0.7)^3 + 0 + C_1(0.7)$$
    $$0 = -153.0 + 0.7 C_1 \Rightarrow \mathbf{C_1 = 218.6}$$

**Maximum Deflection Calculation:**
The maximum deflection occurs at the tip ($x=1.4 \text{ m}$).
$$EI y(1.4) = -446.2(1.4)^3 + 892.3(1.4 - 0.7)^3 + 218.6(1.4)$$
$$EI y(1.4) = -1224.4 + 306.1 + 306.0$$
$$EI y(1.4) = -612.3 \text{ N}\cdot\text{m}^3$$

$$\delta_{max} = \left| \frac{-612.3}{EI} \right|$$

### B. Beam Design & Selection

**Objective:**
Limit vertical deflection to less than 2% of the beam length.
$$\delta_{allowable} = 0.02 \times 1.4 \text{ m} = 0.028 \text{ m}$$

**Selection Calculation:**
I calculated the required Moment of Inertia ($I_{req}$) to keep deflection under 0.028 m.

$$\frac{612.3}{EI} \le 0.028$$
$$I \ge \frac{612.3}{200 \times 10^9 \times 0.028}$$
$$I \ge 1.09 \times 10^{-7} \text{ m}^4 = \mathbf{109,000 \text{ mm}^4}$$

**Selected Beam:**
I selected a **Square Hollow Section (Box Tube)** to maximize stiffness while minimizing weight.
* **Material:** Structural Steel ($E=200$ GPa)
* **Dimensions:** 60 mm x 60 mm
* **Wall Thickness:** 3 mm

**Verification:**
$$I_{actual} = \frac{B^4 - b^4}{12} = \frac{60^4 - 54^4}{12}$$
$$I_{actual} = \frac{12,960,000 - 8,503,056}{12} \approx \mathbf{371,412 \text{ mm}^4}$$

**Conclusion:**
Since $I_{actual} (371,412) > I_{req} (109,000)$, the design is extremely safe and meets all criteria.

### C. Final Beam Design

![Beam Cross Section]({{ "/assets/images/Beam Cross Section.jpg" | relative_url }}){: .project-image}
*Figure 2: Final selection: 60x60x3mm Steel Square Hollow Section.*