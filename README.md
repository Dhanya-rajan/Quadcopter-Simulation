# 🚁 3D Quadcopter Dynamics Simulation (MATLAB)

This repository contains a **full 3D physics-based MATLAB simulation of a quadcopter (drone)** using **Newton–Euler rigid body dynamics**. The model captures both **translational and rotational motion**, including **attitude dynamics, thrust generation, gravity, and inertial coupling**.

This project demonstrates **6-DOF flight dynamics, numerical integration, and aerospace control-oriented modeling** using real governing equations.

---

## 📌 Project Purpose

The objective of this project is to:
- Model **3D translational motion** of a quadcopter
- Model **3D rotational (attitude) motion**
- Apply **Newton’s Second Law and Euler’s rotational equations**
- Simulate **thrust forces from four rotors**
- Track:
  - Position: $x, y, z$
  - Velocity: $\dot{x}, \dot{y}, \dot{z}$
  - Angles: $\phi$ (roll), $\theta$ (pitch), $\psi$ (yaw)
  - Angular rates: $p, q, r$

This is a **true 6-DOF rigid-body flight model**.

---

## Governing Physics & Equations of Motion

All dynamics are derived from **Newton–Euler equations for rigid bodies**.

---

## ✅ 1. Translational Dynamics (Newton’s Second Law)

The net force on the quadcopter is:

$$
\sum \vec{F} = m \vec{a}
$$

Resulting in:

$$
m \ddot{\vec{r}} = \vec{F}_{thrust} + \vec{F}_{gravity}
$$

---

### Thrust Force (Body → Inertial Frame)

Total thrust from the four rotors:

$$
F_T = k_T (\omega_1^2 + \omega_2^2 + \omega_3^2 + \omega_4^2)
$$

Converted into inertial coordinates using the rotation matrix $R$:

$$
\vec{F}_{thrust} =
R
\begin{bmatrix}
0 \\
0 \\
F_T
\end{bmatrix}
$$

---

### Gravity Force

$$
\vec{F}_{gravity} =
\begin{bmatrix}
0 \\
0 \\
-mg
\end{bmatrix}
$$

---

### Final Translational Acceleration

$$
\ddot{\vec{r}} =
\frac{1}{m}
\left(
R
\begin{bmatrix}
0 \\
0 \\
F_T
\end{bmatrix}
+
\begin{bmatrix}
0 \\
0 \\
-mg
\end{bmatrix}
\right)
$$

---

## ✅ 2. Rotational Kinematics (Euler Angles)

The body angular velocity vector:

$$
\vec{\omega} =
\begin{bmatrix}
p \\
q \\
r
\end{bmatrix}
$$

Euler angle rates relate to body angular rates through:


```math
\begin{bmatrix}
\dot{\phi} \\
\dot{\theta} \\
\dot{\psi}
\end{bmatrix}
=
\begin{bmatrix}
1 & \sin\phi \tan\theta & \cos\phi \tan\theta \\
0 & \cos\phi & -\sin\phi \\
0 & \dfrac{\sin\phi}{\cos\theta} & \dfrac{\cos\phi}{\cos\theta}
\end{bmatrix}
\begin{bmatrix}
p \\
q \\
r
\end{bmatrix}
```





---

## ✅ 3. Rotational Dynamics (Euler’s Rigid Body Equation)

$$
\vec{\tau} = I \dot{\vec{\omega}} + \vec{\omega} \times (I \vec{\omega})
$$

Solving for angular acceleration:

$$
\dot{\vec{\omega}} =
I^{-1}
\left(
\vec{\tau} - \vec{\omega} \times (I \vec{\omega})
\right)
$$

---

## ✅ 4. Control Torques from Rotors

Torque contributions from each rotor:

### Roll Torque

$$
\tau_\phi = L k_T (\omega_2^2 - \omega_4^2)
$$

### Pitch Torque

$$
\tau_\theta = L k_T (\omega_3^2 - \omega_1^2)
$$

### Yaw Torque

$$
\tau_\psi = k_D (\omega_1^2 - \omega_2^2 + \omega_3^2 - \omega_4^2)
$$

---

## ✅ 5. Numerical Time Integration

All state variables are integrated using **forward Euler integration**:

### Linear Motion
$$
\vec{v}_{t+1} = \vec{v}_t + \vec{a} \Delta t
$$

$$
\vec{r}_{t+1} = \vec{r}_t + \vec{v} \Delta t
$$

### Angular Motion
```math
\vec{\omega}_{t+1} = \vec{\omega}_t + \dot{\vec{\omega}} \Delta t
```


### Graphs 


<img width="480" height="350" alt="Screenshot 2025-12-09 173309" src="https://github.com/user-attachments/assets/3a4b79ed-de22-4831-bd19-c27fa68b78ae" />
<img width="480" height="345" alt="Screenshot 2025-12-09 173716" src="https://github.com/user-attachments/assets/c9ce97f3-f44c-456f-978c-2c43ea3c8eae" />
<img width="480" height="350" alt="Screenshot 2025-12-09 173730" src="https://github.com/user-attachments/assets/4637f8eb-f596-43b1-b94f-5ed3308a0165" />
<img width="480" height="350" alt="Screenshot 2025-12-09 173745" src="https://github.com/user-attachments/assets/2da6d880-6f5c-429c-a98a-eeba77f9b057" />



