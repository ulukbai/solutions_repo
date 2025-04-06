# 🌀 Analysis of a Forced Damped Pendulum

## 📌 Motivation

The forced damped pendulum is a fascinating physical system that combines restoring forces, damping, and external periodic driving. These interactions lead to a rich variety of behaviors—from simple oscillations to chaotic motion. Studying such systems helps us understand real-world phenomena like energy harvesting devices, structural vibrations, and resonance in mechanical systems.

---

## ⚙️ Mathematical Model

The equation governing the motion of a forced damped pendulum is:

\[
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = A \sin(\omega_d t)
\]

Where:
- \( \theta \): angle of displacement
- \( b \): damping coefficient
- \( g \): gravitational acceleration
- \( L \): length of the pendulum
- \( A \): amplitude of external driving force
- \( \omega_d \): frequency of driving force

---

## 🧪 Python Simulation

import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# --- System parameters ---
g = 9.81        # gravity (m/s^2)
L = 1.0         # pendulum length (m)
b = 0.5         # damping coefficient
A = 1.2         # amplitude of the driving force
omega_d = 2/3   # frequency of the driving force

# --- Initial conditions ---
theta0 = 0.2    # initial angle (radians)
omega0 = 0.0    # initial angular velocity (rad/s)

# --- Time settings ---
t_start = 0
t_end = 100
t_points = 5000
t = np.linspace(t_start, t_end, t_points)

# --- Differential equation of the forced damped pendulum ---
def pendulum_eq(t, y):
    theta, omega = y
    dtheta_dt = omega
    domega_dt = -b * omega - (g / L) * np.sin(theta) + A * np.sin(omega_d * t)
    return [dtheta_dt, domega_dt]

# --- Solving the system using Runge-Kutta method ---
sol = solve_ivp(pendulum_eq, [t_start, t_end], [theta0, omega0],
                t_eval=t, method='DOP853', rtol=1e-8, atol=1e-8)

# --- Extract the solution ---
theta = sol.y[0]
omega = sol.y[1]

#Angle vs Time
plt.figure(figsize=(10, 5))
plt.plot(t, theta, color='teal', label='Angle θ(t)')
plt.title('Forced Damped Pendulum')
plt.xlabel('Time (s)')
plt.ylabel('Angle (rad)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

#Phase Portrait (Angle vs Angular Velocity)
plt.figure(figsize=(10, 5))
plt.plot(theta, omega, color='purple')
plt.title('Phase Portrait')
plt.xlabel('Angle (rad)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid(True)
plt.tight_layout()
plt.show()

#Angular Velocity vs Time
plt.figure(figsize=(10, 5))
plt.plot(t, omega, color='orange')
plt.title('Angular Velocity vs Time')
plt.xlabel('Time (s)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid(True)
plt.tight_layout()
plt.show()

# --- Energy calculations ---
kinetic_energy = 0.5 * L**2 * omega**2
potential_energy = g * L * (1 - np.cos(theta))
total_energy = kinetic_energy + potential_energy

# --- Plot: Energy over Time ---
plt.figure(figsize=(10, 5))
plt.plot(t, kinetic_energy, label='Kinetic Energy')
plt.plot(t, potential_energy, label='Potential Energy')
plt.plot(t, total_energy, label='Total Energy')
plt.title('Pendulum Energy Over Time')
plt.xlabel('Time (s)')
plt.ylabel('Energy (Joules)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
