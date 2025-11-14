# 📘 Nonexistence of Global Solutions for the $p$-Laplacian Wave Equation

### Numerical Verification via Fourier Pseudo-Spectral and Integrating-Factor RK4 Methods

This repository contains the numerical implementation and experiments for the paper:

> **Nonexistence of nontrivial global weak solutions for damped $p$-Laplacian wave equations with combined nonlinearities**
> by *Yinting Liu, Housen Wang, and Qiang Liu*

The goal is to numerically verify the finite-time blow-up predicted by theoretical results for the nonlinear damped $p$-Laplacian wave equation in two dimensions.

---

# 🧮 Mathematical Problem

We consider the truncated Cauchy problem for the nonlinear damped $p$-Laplacian wave equation:
[
\begin{cases}
u_{tt}-\Delta u_t - \Delta_p u = \lambda|u|^{\alpha} + \gamma|\nabla u|^{\beta},
& (x,t)\in \Omega\times(0,T),
u(x,0)=u_0(x),\
u_t(x,0)=u_1(x),
\end{cases}
]
where
[
\Omega=[0,L_x]\times[0,L_y], \qquad
\Delta_p u=\nabla!\cdot\left((|\nabla u|^2+\epsilon^2)^{\frac{p-2}{2}},\nabla u\right),
]
and periodic boundary conditions are imposed in both spatial directions.

Introducing the velocity variable $v=u_t$, the PDE is rewritten as the first-order system
[
\begin{cases}
u_t = v,
v_t = \Delta v + \Delta_p u + \lambda |u|^\alpha + \gamma |\nabla u|^\beta.
\end{cases}
]

---

# ⚙️ Numerical Method

## **Spatial Discretization: Fourier Pseudo-Spectral**

* The domain is discretized using a uniform grid of size (N_x\times N_y).
* Fourier transforms are used to compute spatial derivatives:
  [
  \widehat{\nabla u}=i\mathbf{k}\widehat{u},\qquad
  \widehat{\Delta u}=-|k|^2\widehat{u}.
  ]
* Nonlinear terms are computed in physical space:
  [
  \Delta_p u = \nabla \cdot ( a(|\nabla u|)\nabla u ),\qquad
  a=(|\nabla u|^2+\epsilon^2)^{(p-2)/2}.
  ]

### **2/3 Dealiasing Rule**

To avoid aliasing for nonlinear interactions, spectral coefficients are truncated as:
[
\chi(k_1,k_2)=
\begin{cases}
1, & |k_1|\le N_x/3 \ \text{and}\ |k_2|\le N_y/3,\
0, & \text{otherwise}.
\end{cases}
]

---

## ⏱ Time Integration: Integrating-Factor Runge–Kutta 4 (IF-RK4)

The stiff linear part (v_t=\Delta v) is treated exactly via the integrating factor:

[
\frac{d}{dt}(e^{-|k|^2 t}\widehat{v})
= e^{-|k|^2 t}\widehat{\mathcal{N}}(u),
]

where (\widehat{\mathcal{N}}(u)) contains all nonlinear terms.

Let
[
E = e^{-|k|^2\Delta t},
\qquad
E_{1/2} = e^{-|k|^2\Delta t/2}.
]

A classical four-stage IF-RK4 method is used to update both (u) and (v).

---

# 🚀 Numerical Experiments

All experiments are conducted on:

[
\Omega=[0,8\pi]^2,
\qquad
N_x=N_y=256,
\qquad
\Delta t = 10^{-3},
\qquad
T=10.
]

### **Initial Data**

[
\begin{cases}
u_0(x,y)=A\cos\left(\frac{2\pi x}{L_x}\right)\cos\left(\frac{2\pi y}{L_y}\right),[1mm]
u_1(x,y)=\varepsilon,
\end{cases}
\quad
A=1.2,\quad \varepsilon=10^{-3}.
]

### **Parameters**

[
\lambda=\gamma=2.5,\qquad
\epsilon=10^{-10}.
]

### **Blow-Up Detection**

A numerical blow-up is declared if

[
|u(\cdot,t)|*{L^\infty} > 10^{12}
\quad \text{or} \quad
|u(\cdot,t)|*{L^2} > 10^{12}.
]

The parameter triples ((p,\alpha,\beta)) are varied within the admissible regime predicted by the theoretical nonexistence result, and the blow-up time is recorded for each experiment.

---

# 📊 Example Outputs

* Blow-up time tables
* Evolution plots of (|u|*{L^\infty}) and (|u|*{L^2})
* Contour snapshots during blow-up
* Parameter sensitivity analysis

All figures appear in the `results/` directory.


---

# 📬 Contact

For questions or collaborations, feel free to contact:

**Housen Wang**

University of Cambridge

✉️ [hw729@cam.ac.uk](mailto:hw729@cam.ac.uk)

