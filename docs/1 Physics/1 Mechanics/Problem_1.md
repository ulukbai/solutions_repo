# Problem 1
import numpy as np
import matplotlib.pyplot as plt

# Set up basic initial conditions
initial_velocity = 50  # m/s
gravity = 9.81         # m/s²

# Generate a list of angles from 0 to 90 degrees
angles_deg = np.linspace(0, 90, 500)
angles_rad = np.radians(angles_deg)  # Convert degrees to radians

# Calculate projectile range for each angle using the classic physics formula
# R = (v^2 * sin(2θ)) / g
ranges = (initial_velocity ** 2) * np.sin(2 * angles_rad) / gravity

# Plot the results
plt.figure(figsize=(10, 6))
plt.plot(angles_deg, ranges, color='steelblue', label=f'Initial speed = {initial_velocity} m/s')
plt.title('Projectile Range vs Launch Angle')
plt.xlabel('Launch Angle (degrees)')
plt.ylabel('Range (meters)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Projectile Motion: Range vs Launch Angle

## 🎯 Objective
The goal of this project is to explore how the horizontal distance (range) of a projectile depends on the angle at which it's launched. This is a classic problem in physics, but it’s also a great example of how mathematical models describe real-world motion.

## ⚙️ Theoretical Background
The equation for the range \( R \) of a projectile (assuming no air resistance and launch/landing at the same height) is:

\[
R = \frac{v_0^2 \cdot \sin(2\theta)}{g}
\]

Where:
- \( v_0 \) is the initial velocity,
- \( \theta \) is the launch angle,
- \( g \) is the acceleration due to gravity (9.81 m/s²).

This formula shows that the range depends on the sine of **double** the launch angle. The range reaches a maximum when \( \theta = 45^\circ \), because \( \sin(90^\circ) = 1 \).

## 💻 Implementation

The simulation is written in Python using `numpy` and `matplotlib`. It calculates and plots the projectile range for angles between 0° and 90°, with a fixed initial speed.


