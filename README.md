# Autonomous UAV Mission Simulator
A MATLAB-based 6-DOF quadrotor flight simulation built to model autonomous mission execution, trajectory tracking, and GNC system performance under real-world disturbances.

Developed as a portfolio project to demonstrate applied skills in flight dynamics, control systems design, and simulation — with a focus on UAV applications in search & rescue and autonomous surveillance missions.

---

## Project Roadmap

| Phase | Focus | Status |
|-------|-------|--------|
| 1 | Quadrotor equations of motion & hover simulation | ✅ Complete |
| 2 | Waypoint-following autopilot (PID/GNC) | 🔄 In progress |
| 3 | Mission profiles, wind disturbances & visualization | 🔜 Upcoming |

---

## Phase 1 — Equations of Motion & Hover Test

### What's modeled
A full 6-DOF rigid-body quadrotor using Newton-Euler equations of motion:

- **Translational dynamics** — world-frame accelerations driven by total rotor thrust, projected through a ZYX Euler rotation matrix
- **Rotational dynamics** — body-frame angular accelerations via Euler's equations, driven by differential rotor torques
- **Euler angle kinematics** — body angular rates mapped to Euler angle rates

**State vector (12 states):**
```
[x, y, z, xdot, ydot, zdot, phi, theta, psi, p, q, r]
 |position |  |velocity  |  |euler angles|  |body rates|
```

**Control inputs:** 4 rotor speeds [ω₁, ω₂, ω₃, ω₄] in rad/s

### Files
```
/
├── quadrotor_eom.m      # Equations of motion (plant model)
├── run_simulation.m     # Simulation runner & plotting
└── README.md
```

### How to run
1. Clone the repo and open in MATLAB
2. Run `run_simulation.m`
3. Outputs: 6-panel state plot + 3D trajectory visualization

### Parameters (450mm quadrotor)
| Parameter | Value |
|-----------|-------|
| Mass | 0.5 kg |
| Arm length | 0.225 m |
| Ixx / Iyy | 5×10⁻³ kg·m² |
| Izz | 1×10⁻² kg·m² |
| Thrust coeff (k) | 3×10⁻⁶ N/(rad/s)² |
| Drag coeff (b) | 1×10⁻⁷ Nm/(rad/s)² |

---

## Background & Motivation

Finding a job in aerospace and motorsports engineering is competitive. Rather than wait, I'm building real, demonstrable work that reflects the kind of simulation and controls engineering I want to do professionally.

This project draws on my academic background in GNC, flight dynamics, and MATLAB/Simulink modeling — and is structured the way I'd approach it in a professional environment: documented, version-controlled, and built incrementally.

---

## Skills Demonstrated
- 6-DOF rigid body dynamics modeling
- MATLAB ODE integration (`ode45`)
- Flight dynamics & Euler angle kinematics
- Controls & GNC system design (Phase 2)
- Technical documentation

---

## Contact
**Wes Girardi** — Aerospace Engineer  
[LinkedIn](https://www.linkedin.com/in/wes-girardi) • wesgirardi@hotmail.com
