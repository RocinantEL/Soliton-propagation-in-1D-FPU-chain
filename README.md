# Nonlinear Soliton Generation in a 1D $\beta$-FPU Chain

Numerical simulation and spectral analysis of continuous soliton generation (nonlinear supratransmission) in a driven 1D Fermi–Pasta–Ulam ($\beta$-FPU) lattice using a symplectic Velocity Verlet integrator.

## Physical Model

The system consists of a 1D chain of $N = 512$ unit-mass particles with fixed boundary conditions ($u_0 = u_{N-1} = 0$) and cubic nearest-neighbor interactions ($\beta = 1.0$). The interaction force between adjacent sites is:

$$F(\Delta u) = \Delta u + \beta (\Delta u)^3$$

The equation of motion for internal lattice sites ($n = 2, \dots, N-2$) is:

$$\ddot{u}_n = F(u_{n+1} - u_n) - F(u_n - u_{n-1})$$

The first active site ($n = 1$) is harmonically driven at a frequency above the linear phonon band cutoff ($\omega_{\max} = 2.0$):

$$u_1(t) = a \sin(\omega_{\text{driver}} t), \quad \omega_{\text{driver}} = 2.12, \quad a = 0.287$$

Above a critical driving amplitude, nonlinear modes (solitons/breathers) penetrate the forbidden band gap and propagate along the chain.

## Numerical Method & Analysis

- **Time Integration:** Symplectic Velocity Verlet scheme with time step $\Delta t = 0.01$ over $25{,}000$ steps ($T = 250.0$, sampled every 100 steps).
- **Temporal Spectral Analysis:** Fast Fourier Transform (`scipy.fft.fft`) of single-site displacement trajectories $u_n(t)$ to extract dominant oscillation frequencies.
- **Spatial Spectral Analysis:** Windowed spatial FFT (`scipy.fft.rfft` with a Hanning window) averaged over a selected space-time window to measure the dominant wavenumber $p$ and wavelength $\lambda = 2\pi / p$.
- **Energy Flux & Soliton Energy:** Computation of local energy flux $j_n(t) = \frac{1}{2}(v_n + v_{n+1}) F(u_{n+1} - u_n)$ and total transmitted soliton energy via trapezoidal integration (`np.trapezoid`).

## Repository Structure

```text
.
├── periodic_FPU.ipynb   # Main simulation, animation, FFT, and energy flux analysis
├── requirements.txt     # Python dependencies
└── README.md
