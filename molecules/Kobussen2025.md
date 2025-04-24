# DIV1D

## Sections

2. DIV1D summary
3. SOLPS-ITER "mappings"
4. DIV1D molecular model
5. Comparison between (steady-state) DIV1D and SOLPS-ITER
6. Dominant collisional-radiative processes in DIV1D, SOLPS-ITER models
7. Density ramp sims
8. TCV sims (steady-state and density ramp)

## DIV1D summary

### Assumptions

* Quasineutrality: $n_e = n_i = n$
* Single temperature: $T_e=T_i$
* 1D grid along field line(s); stagnation point to target
  
### Core equations

Solves four time-dependent PDEs for plasma density, parallel momentum, energy, neutral density in SI units:

$$
\begin{align}
\frac{\partial n}{\partial t} &= -B\frac{\partial}{\partial x}\left(\frac{\Gamma_n}{B}\right) + S_n \\
\frac{\partial n m v_\parallel}{\partial t} &= -B\frac{\partial}{\partial x}\left(\frac{\Gamma_{\rm mom}}{B}\right) - \frac{\partial p}{\partial x} + S_{\rm mom} \\
\frac{\partial n e T}{\partial t} &= -B\frac{\partial}{\partial x}\left(\frac{q_\parallel}{B}\right) + v_\parallel\frac{\partial p}{\partial x} + S_{\rm ene} \\
\frac{\partial n_n}{\partial t} &= \frac{\partial}{\partial x}D\frac{\partial}{\partial x}n_n + S_{\rm neutral} \\
\end{align}
$$

### Neutral model
5 volumes containing neutrals, each with a different density, $n_b^i$ (i=1-5).
Each volume is *outside* the SOL (I think) but in contact with different regions of it.

These are (roughly, needs more clarification):
1. An upper divertor volume (ignored in Kobussen 25)
2. A second upper divertor volume (ignored in Kobussen 25)
3. The common flux region (CFR), from the stagnation point to the X-point.
4. The private flux region (PFR), from the X-point to the target. 
5. Divertor CFR


Rate of neutral exchange is determined by the neutral flux density (in $m^{-2}s^{-1}$) from the SOL to the external volume:
$$
\begin{align}
\Gamma_{ex} = \frac{n_n-n_b^i}{\lambda(x) \tau_n}
\end{align}
$$

Hence volumes can act as sinks if their densities are lower than the SOL's neutral density.

### Cell volumes

"Volume" of 1D cell $i$ is:

$$
\begin{equation}
V_i = A_i \lambda_i = 2 \pi R_i \Delta x_i \sin(\theta_i)\lambda_i
\end{equation}
$$

$A_i$ is the area of the cell in contact with the external neutral volume.
$lambda_i$ is poloidal cell width.
$R_i$ is the radial coordinate of the cell.
$\Delta x_i$ the cell 1D length.

Poloidal SOL width is determined from the $\sin(\theta(x))$ parameter using

$$
\begin{equation}
\lambda(x) = B_{trans}(x) \sin(\theta(x)) = C
\end{equation}
$$

where $B_{trans}(x)$ is the component of the magnetic field used to simulate cross-field transport.
Hence, for fixed $B_{trans}(x)$, SOL width depends only on $\sin(\theta(x))$ and on the SOL width at the outer midplane, $\lambda_{omp}$.

### Neutral atom momentum balance updates

* Orig Div1D - no momentum transfer from ions to neutrals in divertor region.
* SOLPS-ITER suggests atoms have $\sim50\%$ flow velocity of the ions in the divertor.
* Solution - add equation for neutral momentum and modify neutral density equation

$$
\begin{align}
\frac{\partial n_n m_n v_n}{\partial t} &= -\frac{\partial}{\partial x}\left( n_n m_n v_n^2 \right) - \frac{\partial p_n}{\partial x} + S_{\rm mom,n} \\
\frac{\partial n_n}{\partial t} &= \frac{\partial}{\partial x}D\frac{\partial}{\partial x}n_n -\frac{\partial}{\partial x}\left( n_n v_n \right) + S_{\rm neutral} \\
\end{align}
$$

* Assume $m_n\sim m$, $p_n=2e n_n T_n$
* To avoid adding a neutrals energy equation, assume $E_n$=0.5 eV.
* $S_{\rm mom,n}$ is determined by collisional processes in the divertor (see appendix B).

### Molecule model

Add molecules density equation

$$
\begin{align}
\frac{\partial n_m}{\partial t} &= \frac{\partial}{\partial x}D_m\frac{\partial}{\partial x}n_m + S_{\rm m} \\
\end{align}
$$

where $D_m$ is the diffusion coefficient for the molecules.

* Assume no net parallel velocity (unlike SD1D)
* Justified by 

### Collisional radiative processes

* Including molecules makes it necessary to track many more collisional-radiative processes.
* Complete list in appendix E (includes momentum, energy losses through inelastic collisions)
* Most important reactions are:

Atomic / atomic ions:

| Index | Reaction                                   | Notes                                         | Also in SD1D? |
| ----- | ------------------------------------------ | --------------------------------------------- | ------------- |
| 1     | $e + D \to 2e+D^+$                         | Collisional ionisation of D                   | Y             |
|       | $e + D \to 2e+D^+$                         | Collisional ionisation of D + radiative decay | Y?            |
| 2     | $D^+ + D \to D+D^+$                        | D charge exchange                             | Y             |
| 3     | $e + D^+ \to D$                            | D recombination (radiative + three-body)      | Y             |
|       | $e + D^+ \to D + h\nu$                     | D recombination (radiative power loss)        | Y?            |
| ?     | $D^+ + D \to D^+ + D$                      | (elastic) electron-ion collisions             | ?             |
| 4     | $e + D_2 \to 2e  + D_2^+$                  | Molecular ionisation                          | Y             |
| 5     | $e + D_2 \to e + 2D$                       | Collisional dissociation                      | Y             |
| 6     | $D^+ + D_2 \to D + D_2^+$                  | Molecular charge exchange                     | Y             |
| 7     | $e + D_2^+ \to 2D$                         | Dissociative recombination                    | Y             |
| 8     | $e + D_2^+ \to e + D^+ + D$                | Collisional dissociation of $D_2^+$           | Y             |
| 9     | $e + D_2^+ \to 2e + 2D^+$                  | Dissociative ionisation of $D_2^+$            | Y             |
| 10    | $D^+ D^- \to 2D$                           | $D^-$ charge exchange                         | N             |
| 11    | $D^+ D^- \to 2e + D^+ + D$                 |                                               | N             |
| ?     | $e + D_2 \to D^- + D$                      | Dissociative attachment                       | N?            |
| ?     | $e + D_2 \to e + D_2^* \to e + D_2 + h\nu$ | Molecular excitation + radiative decay        | ?             |
| ?     | $D^+ + D_2 \to D^+ + D_2$                  | (elastic) molecule-ion collisions             | ?             |

N.B. Hermes-3 also has 3-body recombination: $2e + D^+ \to D + e$

DIV1D doesn't transport $D_2^+$, SD1D does (**Need to decide which to do in H3** ):
* DIV1D assumption: Destruction timescales of $D_2^+$ and $D_-$ are much faster than their transport times (and therefore they don't need their own momentum and energy equations; OP AND density??)
* Instead DIV1D assumes a fixed $f$ in $n_{D_2^+}=f n_{D_2}$ and calculates associated rates accordingly.
* SD1D, on the other hand, *does* track $D_2^+$ density, so that value is used directly in the rate calcs.

DIV1D models MAR and MAD, SD1D only MAR (+ MAI for both):
* Molecular Activated Recombination (MAR), Molecular Activated Dissociation (MAD) and Molecular Activated Ionization (MAI) are modelled by various chained combinations of reactions 1-11.
* Inclusion of 10 and 11 means MAR via $D^-$ and MAD via $D^-$ are both modelled. 
* Since SD1D doesn't have 10 and 11, it only models *MAR* via $D^-$.

DIV1D uses AMJUEL for ion-neutral reactions:
* SOLPS_ITER/EIRENE and DIV1D both use AMJUEL for reactions with H.
* For Deuterium, DIV1D rates are calculated using a rescaled ion temperature: $\langle\sigma v\rangle_D(T)=\langle\sigma v\rangle_H(T/2)$ where $\langle\sigma v\rangle_i$ is the rate coefficient for species $i$.

### Geometry (to accommodate MAST-U)

* Allow $\sin(\theta(x))$, $R(x)$ to vary along SOL; set by mapping from SOLPS MAST-U sims directly.
* Allow baffle point to be different to X-point (previous sims focussed on TCV, which Kobussen claim is "unbaffled", but see [recent TCV work](https://iopscience.iop.org/article/10.1088/1741-4326/ace45f)).
* Soften density change between the core and divertor common flux regions.

### Self-consistent background and core density

Previous DIV1D set (presumably constant) neutral volume densities $n_b^i$ from SOLPS-ITER sims. To model gas puffs, neutral densities need to vary self-consistently.

Model:
* Neutrals can "leak" between adjacent volumes at rates $\Gamma_{leak}^{ij}$.
* Neutrals can enter the volumes as "pumps" ($S_{pump}^i$) and "puffs" ($S_{puff}^i$).
* Some ions impinging the target get recycled as neutrals, which can go into the SOL, or one of the reservoirs ($S_{tar}^i$).
* New neutral volume density equations are then:

$$
\begin{equation}
\frac{d n_b^i}{dt} = \frac{\Gamma_{leak}^{i-1,i} - \Gamma_{leak}^{i,i+1}}{V^i} + S_{pump}^i + S_{puff}^i + S_{tar}^i + S_c^i + \frac{1}{V^i}\sum_p{\frac{n_n^p - n_b^i}{\tau_n} A_p}
\end{equation}
$$

* The leakage fluxes can be determined by considering two opposing one-way Maxwellian fluxes through a gap of area $A^{ij}$.

**Lots more on this (p8,p9), but skipping it for now**

### Comparison with SOLPS - profiles

* Heat flux density and electron temperature profiles
* The electron density profile of DIV1D shows a rapid increase around the baffle point, where the external neutral density suddenly increases
  * increased ion source due to ionization of neutrals beyond the baffle
* Plasma flow velocity profile of DIV1D peaks around the X-point, whereas SOLPS has maximum parallel flow velocity at the baffle entrance. A possible reason is the geometry implementation used by DIV1D
  * At the X-point, λ is large, leading to slow exchange with the external volumes, low neutral density in the SOL, and therefore underestimated momentum losses.
  * Beyond the X-point, λ decreases, leading to higher momentum losses, causing the electron velocity to peak at the X-point.
* The atomic and molecular density profiles of DIV1D and SOLPS are similar, especially in the divertor region.
* The parallel flow velocity of the atoms of DIV1D lies within the value intervals of the 1D SOLPS mapping, except at the target, because DIV1D uses vn(L) = 0 as a boundary condition here.

### Comparison with SOLPS - Collisional radiative processes

Ion sources and sinks:
* MAR, MAI and EIR reaction rates are similiar between SD1D and DIV1D (probably because underlying density profs are similar).
* MAR dominates EIR (as an ion sync) beyond the baffle entrance
* Ionisation of atoms dominates over MAR throughout the SOL

Momentum loss:
* CX dominates momentum loss almost everywhere, except the last 70 cm of before the target, where elastic collision between ions and molecules are more important
  * More molecules near the target, but also lower T that gives higher collision cross section

Power dissipation:
* Most heat dissipated after the baffle entrance
* Molecules account for $\sim20\%$ of power dissipation in DIV1D sim

MAR/MAD:
* Two channels for MAR/MAD:
  1. via $D_2^+$, created in molecular CX
  2. via $D^-$, created by *dissociative attachment
* DIV1D finds $D^-$ reactions only dominate close to the target
* But $D^-$ reactions expected to be important in their knock-on effect on the equilibirum
* SOLPS-ITER don't include $D^-$ because "due to isotope dependencies, generating $D^-$ is less likely than $H^-$". Implication is that Kobussen et al. disagree. 

### Comparison with SOLPS - Ramp-up sims

* Heat flux at target: New DIV1D model matches SOLPS very nicely
* Particle flux at target: New DIV1D model matches much better than old one and is close-ish to SOLPS, not as good as heat flux.
* Differences likely due to different SOL widths in different (*steady-state*) SOLPS sims vs single SOL width in one *time-evolving* DIV1D sim.

### Compatison with TCV

* Nothing critical; skipped

### Appendix A

* Tables of input params

#### Appendix B

* Full details of equation implementation, including formulation of source terms from reaction rate cross sections
* Most important section if we want to re-implement Kobussen approach

### Appendix C

* Description of which combination of reactions are attributed to
  * MAR, MAR via $D_2^+$
  * MAR, MAR via $D^-$
  * Energy loss through $D_2^+$, $D^-$ reactions

### Appendix D

* Glossary of variables

### Appendix E

* Full table of collisional-radiative (CR) processes with rate constants
  

## Useful refs

* Code papers
  * DIV1D presentation paper [[4]](https://dx.doi.org/10.1088/1361-6587/ac9dbd)
  * DIV1D major update paper [[5]](https://dx.doi.org/10.1088/1361-6587/ad2e37)
  * SD1D [[7]](https://dx.doi.org/10.1088/1361-6587/ac6827)
* Modelling general
  * AMJUEL's mass-rescaled rates underestimates molecular charge exchange at low temperature [[13]](https://dx.doi.org/10.1088/1741-4326/acd394) and [[14]](https://arxiv.org/abs/2311.16732)
  * Use of AMJUEL for CR processes in plasma and plasma-neutral interactions (or possibly their equaivalence with SD1D) [[5]](https://dx.doi.org/10.1088/1361-6587/ad2e37) and [[10]](https://doi.org/10.13182/FST47-172)
* Experimental
  * Molecular interactions have significant influence on the divertor plasma in MAST-U experiments [[6]](https://dx.doi.org/10.1088/1741-4326/acf946)
* Other
  * SOLPS-ITER sims show high molecular density in divertor region [this paper; preprint!]
  * DIV1D without molecules struggles to model the MAST-U SOL [5](https://dx.doi.org/10.1088/1361-6587/ad2e37)
  * SD1D uses neutral energy equation and molecular momentum and energy equations [[7]](https://dx.doi.org/10.1088/1361-6587/ac6827)

## To define:

* Common flux region (CFR):
* Private flux region (PFR):
* Stagnation point
  * Around the midplane in the SOL?
* Divertor baffles aims to
  * enhance the containment of neutral particles within the divertor region (minimizie the number of neutral particles returning to the core)
  * reduce the pressure at the target, improving power exhaust and reducing the target heat load
  * reduces unwanted coupling between the divertor and the core plasma