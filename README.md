# Six-Wheeled Robot Control Performance Analysis

This repository contains the simulation results comparing two control strategies for a six-wheeled mobile robot: 
1. **RBFNN + SMC** (Radial Basis Function Neural Network with Sliding Mode Control)
2. **SMC only** (Pure Sliding Mode Control)

The simulations demonstrate the control performance under challenging conditions, particularly when the robot experiences center of gravity (CoG) offsets that vary over time.

## Performance Comparison

### Circular Trajectory

The circular trajectory test demonstrates how both controllers handle continuous turning with constant curvature. The RBFNN+SMC controller maintains better tracking performance throughout the path.

![Circular Trajectory Comparison](gif/circular_trajectory.gif)

**Key observations:**
- The RBFNN+SMC controller (blue) maintains closer proximity to the target trajectory
- The SMC-only controller (red) shows larger tracking errors, especially under CoG offset conditions
- Position error for RBFNN+SMC remains smaller throughout the trajectory

### Sinusoidal Trajectory

The sinusoidal path presents a greater challenge with continuously varying curvature. This test highlights the adaptive capability of the RBFNN+SMC controller.

![Sinusoidal Trajectory Comparison](gif/sinusoidal_trajectory.gif)

**Key observations:**
- RBFNN+SMC adapts quickly to the changing curvature
- SMC-only controller exhibits larger oscillations and overshoots
- RBFNN effectively compensates for the time-varying CoG offset

### Quintic Trajectory

The quintic trajectory test shows performance during transitions between different path segments with smooth acceleration profiles.

![Quintic Trajectory Comparison](gif/quintic_trajectory.gif)

**Key observations:**
- RBFNN+SMC provides smoother transitions at control points
- SMC-only controller struggles to maintain accuracy during curvature changes
- RBFNN+SMC demonstrates superior disturbance rejection

## Performance Analysis

### Time-Varying Center of Gravity Effects

One of the key challenges in this simulation was the time-varying center of gravity (CoG) offset. The RBFNN controller shows significant advantages in handling these dynamics:

1. **Uncertainty Approximation**: The RBFNN component actively learns and approximates the uncertain dynamics caused by the shifting CoG, allowing for more accurate compensation.

2. **Disturbance Rejection**: When the CoG shifts over time, it introduces time-varying disturbances to the system dynamics. RBFNN+SMC shows superior disturbance rejection compared to SMC alone.

3. **Adaptation**: The RBFNN controller adapts its parameters online, enabling it to respond to changes in the system's behavior due to CoG shifts.

4. **Reduced Tracking Error**: Across all trajectory types, the RBFNN+SMC controller consistently maintains smaller tracking errors when compared to the SMC-only controller.

5. **Reduced Control Effort**: Despite the better performance, the RBFNN+SMC controller often requires less control effort (lower torque peaks) as it compensates for uncertainties more efficiently.

### Limitations of SMC-Only Approach

The SMC-only controller shows several limitations when dealing with CoG offsets:

1. **Chattering**: Without the RBFNN adaptive component, the SMC controller must rely on high-gain feedback to overcome uncertainties, which can lead to control chattering.

2. **Parameter Sensitivity**: The SMC controller's performance is more sensitive to parameter tuning and degrades significantly under varying CoG conditions.

3. **Slower Response**: The SMC-only approach shows slower response to sudden changes in trajectory curvature, leading to larger transient errors.

## Conclusion

The simulation results clearly demonstrate the superior performance of the RBFNN+SMC controller over the SMC-only approach, especially under challenging conditions with time-varying center of gravity offsets. The adaptive learning capability of the RBFNN component provides significant advantages in handling system uncertainties and disturbances, resulting in improved tracking performance, reduced control effort, and enhanced robustness.

These results highlight the potential of neural network-based adaptive control approaches for robust control of mobile robots under uncertain and varying operating conditions.
