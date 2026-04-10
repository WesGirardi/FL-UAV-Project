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

### State Vector

The quadrotor is modeled as a 6-DOF rigid body with 12 states:

$$\mathbf{x} = [x,\ y,\ z,\ \dot{x},\ \dot{y},\ \dot{z},\ \phi,\ \theta,\ \psi,\ p,\ q,\ r]^T$$

where $(x, y, z)$ is world-frame position, $(\dot{x}, \dot{y}, \dot{z})$ is world-frame velocity, $(\phi, \theta, \psi)$ are roll/pitch/yaw Euler angles, and $(p, q, r)$ are body-frame angular rates.

---

### Rotor Forces & Moments

Each rotor produces thrust proportional to the square of its speed. The four rotor inputs map to a total thrust and three moments:

$$F_T = k(\omega_1^2 + \omega_2^2 + \omega_3^2 + \omega_4^2)$$

$$L = kd(-\omega_2^2 + \omega_4^2) \quad \text{(roll moment)}$$

$$M = kd(-\omega_1^2 + \omega_3^2) \quad \text{(pitch moment)}$$

$$N = b(-\omega_1^2 + \omega_2^2 - \omega_3^2 + \omega_4^2) \quad \text{(yaw moment)}$$

where $k$ is the thrust coefficient, $b$ is the drag coefficient, and $d$ is the arm length.

**Rotor layout (top view):**
```
    1 (CW)
4 (CCW)  2 (CCW)
    3 (CW)
```

---

### Translational Dynamics

World-frame accelerations are computed by projecting the body-frame thrust through a ZYX Euler rotation matrix:

$$m\ddot{x} = (\cos\phi\sin\theta\cos\psi + \sin\phi\sin\psi)\ F_T$$

$$m\ddot{y} = (\cos\phi\sin\theta\sin\psi - \sin\phi\cos\psi)\ F_T$$

$$m\ddot{z} = -mg + (\cos\phi\cos\theta)\ F_T$$

---

### Rotational Dynamics

Body-frame angular accelerations follow Euler's equations:

$$\dot{p} = \frac{(I_{yy} - I_{zz})qr + L}{I_{xx}}$$

$$\dot{q} = \frac{(I_{zz} - I_{xx})pr + M}{I_{yy}}$$

$$\dot{r} = \frac{(I_{xx} - I_{yy})pq + N}{I_{zz}}$$

---

### Euler Angle Kinematics

Body angular rates are mapped to Euler angle rates:

$$\dot{\phi} = p + (q\sin\phi + r\cos\phi)\tan\theta$$

$$\dot{\theta} = q\cos\phi - r\sin\phi$$

$$\dot{\psi} = \frac{q\sin\phi + r\cos\phi}{\cos\theta}$$

---

### Hover Condition

At hover, total thrust equals weight with all rotors at equal speed:

$$4k\omega_{hover}^2 = mg \implies \omega_{hover} = \sqrt{\frac{mg}{4k}}$$

---

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
| $I_{xx}$ / $I_{yy}$ | $5 \times 10^{-3}$ kg·m² |
| $I_{zz}$ | $1 \times 10^{-2}$ kg·m² |
| Thrust coeff $k$ | $3 \times 10^{-6}$ N/(rad/s)² |
| Drag coeff $b$ | $1 \times 10^{-7}$ Nm/(rad/s)² |

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
