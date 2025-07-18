# Calculation of reaction source terms

The following describes how density, momentum and energy sources (due to population changes) are determined. The momentum and energy calculations follow the approach in [this RemKit module](https://github.com/SMijin/RMK_extensions/blob/master/RMK_extensions/multispecies/neutrals.py) (private repo!).

## Definitions

- $C_s$ is defined to be the population change of species $s$ in a given reaction, i.e. the number of that species on the right-hand side of the reaction string minus the number on the left-hand side.
- We define participation factors ($p_s$ for species $s$) that can be used to control (usually turn on or off) the contribution of each species to the population change source terms.
- The density and temperature-dependent reaction rate, $R(n,t)$ is defined in terms of the "mass action factor", $M$:

$$
\begin{align}
R(n,T) &= \prod_{r}(n_{r}) c_R(n,T) \\
       &= M c_R(n,T) \\
\end{align}
$$

where
- $c_R(n,T)$ is the reaction rate coefficient at (electron) number density $n$ and (electron) temperature $T$.
- $\prod_{r}{n_{r}}$, the mass action factor, is the product of all input/reactant species densities.

The (n,T) notation is dropped in the following subsections for the sake of simplicity, so $R\equiv R(n,T)$

## Density / number

Density source for species $s$:

$$
\begin{align}
\frac{\partial{n_s}}{\partial{t}} &= p_s C_s R
\end{align}
$$

where 

 - $p_s$ is the participation factor of species $s$
 - $C_s$ is the population change in species $s$
 - $R$ is the reaction rate in number per unit time.

## Momentum

Momentum source for species $s$:

$$
\begin{equation}
  \frac{\partial{G_s}}{\partial{t}} =
  \begin{cases}
    C_s R G_s & \text{for $C_s < 0$} \\
    S_{G,s} R \sum_{r} \left(-C_r p_r G_r\right) & \text{for $C_s > 0$} \\
    0 & \text{otherwise} \\
  \end{cases}
\end{equation}
$$

where $\sum_{r}$ indicates a sum over all reactants / in-state species which have a **-ve** pop. change (i.e. those that are consumed by the reaction) and

 - $p_r$ is the participation factor of reactant $r$
 - $C_r$ is the population change of reactant $r$
 - $C_s$ is the population change of species $s$
 - $R$ is the reaction rate
 - $G_r$ is the momentum associated with reactant $r$
 - $S_{G,s}$ is the momentum splitting factor for species $s$

The splitting factor $S_{G,s}$ is the mass of a species $s$ generated per reaction, divided by the total mass of all product species ($q$) that are generated ($C_s > 0$).
That is

$$
\begin{align}
S_{G,s} &= \frac{\Delta M_s}{\Delta M} \\
        &= \frac{C_s p_{s} m_{s}}{\sum_{q} \left(C_q p_{q} m_{q}\right)}
\end{align}
$$

## Energy

Energy source for species $s$:

$$
\begin{equation}
  \frac{\partial{G_s}}{\partial{t}} =
  \begin{cases}
    C_s R W_s & \text{for $C_s < 0$} \\
    S_{W,s} R \sum_{r} \left(-C_r p_r R W_r \right) & \text{for $C_s > 0$} \\
    0 & \text{otherwise} \\
  \end{cases}
\end{equation}
$$

where $\sum_{r}$ signifies a sum over all reactants / in-state species which have a **-ve** pop. change (i.e. those that are consumed by the reaction) and

 - $p_r$ is the participation factor of reactant $r$
 - $C_r$ is the population change of reactant $r$
 - $C_s$ is the population change of species $s$
 - $R$ is the reaction rate
 - $W_r$ is the energy associated with reactant species $r$
 - $W_s$ is the energy associated with species $s$

The splitting factor $S_{W,s}$ is the number of particles of species $s$ generated per reaction, divided by the total number of particles generated (subscript $q$, indicating $C_s > 0$).
That is

$$
\begin{align}
S_{W,s} &= \frac{\Delta N_s}{\Delta N} \\
        &= \frac{C_{s} p_{s}}{\sum_{q} C_{q} p_{q}}
\end{align}
$$


## Symmetric CX (special case)

For single atom/ion or *symmetric* CX (e.g. $d + d_+ \to d_+ + d$), population changes are zero for both participating species.

### Possible workaround
Could handle symmetric CX in the existing framework by discriminating between in/reactant and out/product versions of the same species when calculating pop changes.

i.e. rewrite

$$
\begin{equation}
H + H_{+} \to H_{+} H
\end{equation}
$$

as

$$
\begin{equation}
H_{in} + H_{+,in} \to H_{+,out} H_{out}
\end{equation}
$$

Then reactants all have -1 pop changes, products all have +1. When getting/setting data for the participating species, the suffixes would be automatically stripped such that the state is modified appropriately. Could use a wrapper around get/set operations that handles this when interacting with the state in Reaction::transform()?

<!-- 
## Examples

Need rechecking

### Density: Ionisation of $C_{+3}$

$C_{+3} + e \to C_{+4} + 2e$

$C_s$ is:
|          |     |
| -------- | --- |
| $C_{+3}$ | -1  |
| $C_{+4}$ | +1  |
| e        | +1  |

$$
\begin{align}
\frac{\partial{n_{C+3}}}{\partial{t}} &= -R n_{C+3} n_e \\
\frac{\partial{n_{C+4}}}{\partial{t}} &= R n_{C+3} n_e \\
\frac{\partial{n_{e}}}{\partial{t}} &= R n_{C+3} n_e \\
\end{align}
$$

### Momentum: Ionisation of $C_{+3}$

$C_{+3} + e \to C_{+4} + 2e$

${C+3}$ ($C_s < 0$) mom. source is
 
$$
\begin{align}
\frac{\partial{G_{C+3}}}{\partial{t}} &= R G_{C+3} \frac{- w_{C+3} }{n_{C+3}} \\
                                      &= -R m_{C+3} v_{C+3} \frac{w_{C+3} }{n_{C+3}} \\
\end{align}
$$

c.f. existing (OpenADASReaction)

$R m_{C+3} v_{C+3}$ -->
