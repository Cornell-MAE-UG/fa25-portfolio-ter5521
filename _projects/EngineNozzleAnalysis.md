---
layout: default
title: Nozzle Analysis
description: Linear Actuator Lifting Design
technologies: Drawing
image: "/assets/images/Engine.png"
---
# Thermodynamic Analysis of the SpaceX Raptor V2 Engine Nozzle

## 1. Introduction and Device Selection
This report analyzes the **converging-diverging (de Laval) nozzle** of the **SpaceX Raptor V2 engine**. The Raptor V2 is a full-flow staged combustion cycle engine powered by cryogenic liquid methane and liquid oxygen. This analysis focuses specifically on the nozzle component, which functions as a steady-state open system designed to convert the high enthalpy of the combustion gases into kinetic energy for propulsion.

## 2. Qualitative Description
The Raptor nozzle is a bell-shaped, converging-diverging duct designed to accelerate exhaust gases to hypersonic speeds.
1.  **Combustion Chamber (Inlet):** The working fluid enters the nozzle from the main combustion chamber at extremely high pressure and temperature with negligible velocity (stagnation conditions).
2.  **Throat (Converging Section):** The flow accelerates subsonically until it reaches the nozzle throat (minimum area), where it becomes **sonic (Mach 1)**. This is a "choked flow" condition.
3.  **Exit (Diverging Section):** Downstream of the throat, the area expands. Because the flow is supersonic, this area increase causes the gas to expand (pressure drops) and accelerate further (velocity increases), converting internal energy ($u$) and flow work ($Pv$) into kinetic energy.

<figure class="project-image">
	<img src="{{ "/assets/images/Engine.png" | relative_url }}" alt="Photo of the SpaceX Raptor V2 engine side view" />
	<figcaption>Figure 1: The SpaceX Raptor V2 Engine, displaying the regenerative cooling channels on the bell nozzle. (Source: SpaceX)</figcaption>
</figure>

<figure class="project-image">
	<img src="{{ "/assets/images/De_Laval_nozzle_2.png" | relative_url }}" alt="Schematic of De Laval nozzle showing Pressure, Temperature, and Velocity trends" />
	<figcaption>Figure 2: Cross-sectional schematic of nozzle geometry showing the inverse relationship between pressure and velocity in the diverging section. (Source: Citizendium)</figcaption>
</figure>

## 3. System Diagram and Thermodynamic Model
We define the Control Volume (CV) enclosing the gas flowing from the combustion chamber exit (State 1) to the nozzle exit plane (State 2).

<figure class="project-image">
	<img src="{{ "/assets/images/NozzleCVDiagram.jpg" | relative_url }}" alt="Control Volume diagram of nozzle with mass flow and state labels" />
	<figcaption>Figure 3: Control Volume (CV) for the nozzle analysis. $\dot{Q} \approx 0$ and $\dot{W} = 0$.</figcaption>
</figure>

### Assumptions:
1.  **Steady State:** The engine is firing at a constant thrust level.
2.  **Adiabatic:** $\dot{Q} \approx 0$. While the nozzle is regeneratively cooled, the heat loss is small compared to the immense enthalpy flux of the exhaust gas.
3.  **No Work:** $\dot{W} = 0$. The nozzle has no moving shafts or pistons.
4.  **Potential Energy:** $\Delta PE \approx 0$.
5.  **Ideal Gas:** We treat the exhaust gas as an ideal gas with constant average specific heats.

## 4. Governing Equations
Based on the assumptions above, we apply the conservation laws central to thermodynamic propulsion.

### Mass Balance
For steady flow, the mass flow rate is constant throughout the nozzle:
$$\dot{m} = \rho_1 A_1 V_1 = \rho_{throat} A_{throat} V_{throat} = \rho_2 A_2 V_2$$

### Energy Balance (First Law)
Starting with the steady-flow energy equation:
$$\dot{Q} - \dot{W} + \dot{m}(h_1 + \frac{V_1^2}{2}) = \dot{m}(h_2 + \frac{V_2^2}{2})$$
With $\dot{Q}=0$, $\dot{W}=0$, and assuming $V_1 \approx 0$ (stagnation conditions in the chamber):
$$h_1 = h_2 + \frac{V_2^2}{2}$$
Solving for exit velocity:
$$V_2 = \sqrt{2(h_1 - h_2)}$$
For an ideal gas, $\Delta h = c_p \Delta T$, so:
$$V_2 = \sqrt{2 c_p (T_1 - T_2)}$$

### Entropy Balance & Isentropic Efficiency
In an ideal, reversible nozzle, entropy is generated ($S_{gen}=0$) and the process is isentropic ($s_1 = s_{2s}$).
However, real nozzles have friction and shocks. We characterize this using **Isentropic Nozzle Efficiency ($\eta_N$)**:
$$\eta_N = \frac{\text{Actual KE at exit}}{\text{Isentropic KE at exit}} = \frac{V_{2a}^2}{V_{2s}^2} \approx \frac{h_1 - h_{2a}}{h_1 - h_{2s}}$$

## 5. Performance Analysis with Operating Data
We will analyze the expansion using approximate data for the Raptor V2.

**Data Sources:**
* Chamber Pressure ($P_1$): 300 bar (30 MPa) [Source: SpaceX Specifications]
* Chamber Temperature ($T_1$): ~3600 K (Estimated for Methalox combustion)
* Expansion Ratio ($\epsilon = A_2/A_{throat}$): ~35 (Sea Level version)
* Specific Heat Ratio ($k$): ~1.2 (High temp exhaust gas)
* Specific Heat ($c_p$): ~2200 J/kg·K

### Calculating Theoretical Exit Velocity ($V_{2s}$)
Using the isentropic relation for an ideal gas expanding to Sea Level pressure ($P_2 = 1 \text{ bar}$):
$$T_{2s} = T_1 \left( \frac{P_2}{P_1} \right)^{\frac{k-1}{k}}$$
$$T_{2s} = 3600 \text{ K} \left( \frac{1 \text{ bar}}{300 \text{ bar}} \right)^{\frac{0.2}{1.2}} \approx 3600(0.0033)^{0.166} \approx 1388 \text{ K}$$

Now, using the energy balance:
$$V_{2s} = \sqrt{2 (2200 \text{ J/kg K}) (3600 \text{ K} - 1388 \text{ K})}$$
$$V_{2s} = \sqrt{4400 (2212)} \approx \sqrt{9,732,800} \approx 3120 \text{ m/s}$$

This high exit velocity is what generates the thrust ($F = \dot{m}V_e$).

## 6. Analysis of Change in Operating Conditions: Altitude (Back Pressure)
The performance of a nozzle is critically dependent on the relationship between the **Exit Pressure ($P_{exit}$)** and the **Ambient Back Pressure ($P_{amb}$)**.

**The Design Change:**
We compare the standard Raptor nozzle operation at **Sea Level** ($P_{amb} = 1$ bar) versus operating the same nozzle in a **Vacuum** ($P_{amb} \approx 0$ bar).

### Scenario A: Sea Level Operation (Design Condition)
At sea level, the nozzle is designed such that the pressure of the gas at the exit ($P_{exit}$) roughly matches the ambient air pressure ($P_{amb}$). This is **Optimal Expansion**. The exhaust plume flows straight out.

### Scenario B: Vacuum Operation (Under-Expansion)
If we take this same nozzle to space ($P_{amb} = 0$):
* The gas pressure at the exit ($P_{exit} = 1$ bar) is now much *higher* than the surroundings.
* The gas continues to expand *after* leaving the nozzle.
* **Performance Impact:** The nozzle is "under-expanded." We are leaving potential energy on the table. The gas had more pressure it could have converted into velocity, but the nozzle wasn't long enough to capture it.

### Scenario C: Sea Level Operation of a Vacuum Nozzle (Over-Expansion)
If we swapped the nozzle for a larger "Raptor Vacuum" nozzle (Expansion ratio ~90) and fired it at sea level:
* The nozzle tries to expand the gas down to 0.1 bar.
* However, the ambient air is at 1 bar.
* $P_{amb} > P_{exit}$. The atmosphere crushes the exhaust plume.
* **Performance Impact:** This causes **Flow Separation**. The flow detaches from the nozzle walls, causing chaotic shock waves inside the nozzle. This can mechanically destroy the engine and significantly reduces isentropic efficiency ($\eta_N$) and thrust.

<figure class="project-image">
	<img src="{{ "/assets/images/NozzleSituations.png" | relative_url }}" alt="Comparison diagram of Over-expanded, Under-expanded, and Optimal nozzle plumes" />
	<figcaption>Figure 4: Impact of ambient pressure on plume geometry. Note the "shock diamonds" present in non-optimal expansion regimes. (Source: ResearchGate)</figcaption>
</figure>

## 7. Conclusion
The Raptor V2 nozzle effectively uses the principles of steady-flow energy conversion to turn high-pressure enthalpy into kinetic energy. However, its efficiency is tightly coupled to the ambient pressure. A nozzle optimized for sea level loses efficiency in a vacuum due to under-expansion, while a vacuum-optimized nozzle risks flow separation and damage if operated at sea level. This necessitates different nozzle designs (Raptor Sea Level vs. Raptor Vacuum) for different stages of flight.