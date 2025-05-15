# RemKit (+ new RemKit module) approach

For each transition / reaction (that isn't symmettric CX), set up terms for

## Density / number
$$
\begin{align}
\frac{\partial{n_s}}{\partial{t}} &= c_s R \prod_{s'{\in}I}{n_{s'}}
\end{align}
$$

where the product is over $I$, the set of input/reactant species and

 - $c_s$ is the population change
 - $n_{s'}$ the species density of species $s'$
 - $R$ is the reaction rate.

### e.g. Ionisation of $C_{+3}$

$C_{+3} + e \to C_{+4} + 2e$

$c_s$ is:
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




## Momentum

$$
\begin{align}
\frac{\partial{G_s}}{\partial{t}} &= \frac{c_s w_s R G_s}{n_s} \text{ if } c_s < 0 \\
\frac{\partial{G_s}}{\partial{t}} &= - R \sum_{s'} \left(\frac{m_s}{m_{s'}} c_{s'} \frac{w_s w_{s'}}{w_{out}} \frac{G_{s'}}{n_{s'}}\right) \text{ if } c_s > 0 \\
\end{align}
$$

where the sum is over all reactants / instate species which themselves have a **+ve** pop. change.

 - $c_s$ is the population change
 - $w_s$ the participation weight
 - $G_s$ the species flux
 - $n_s$ the species density of species $s$
 - $w_{out}$ is the sum of participation weights over the products
 - $R$ is the reaction rate.

Note that:

- splittingFactor in the code is $w_{out}$
- $c_s$ currently labelled $S$; change
- $w_s$ term ignored for now
- $G_s$ gets incorporated later in H3 (I think)
- massActionFactor is the product of all the reactant densities
- When computing momentum changes for species with -ve pop changes:
  - Only the species itself contributes to the source term
- When computing momentum changes for species with +ve pop changes:
  - Reactants with -ve pop. changes (those being "consumed") contribute *+vely*
  - Reactants with +ve pop. changes (those being net generated) contribute *-vely*

### e.g. Ionisation of $C_{+3}$

$C_{+3} + e \to C_{+4} + 2e$

${C+3}$ ($c_s < 0$) mom. source is
 
$$
\begin{align}
\frac{\partial{G_{C+3}}}{\partial{t}} &= R G_{C+3} \frac{- w_{C+3} }{n_{C+3}} \\
                                      &= -R M_{C+3} v_{C+3} \frac{w_{C+3} }{n_{C+3}} \\
\end{align}
$$

c.f. existing (OpenADASReaction)

$R M_{C+3} v_{C+3}$

## Energy

ToDo

---

### Symmetric CX

Could crowbar symmetric CX into existing framework by differentiating input, output species in pop change map
  
Possible implementation; rewrite

$$
\begin{equation}
H + H_{+} \to H_{+} H
\end{equation}
$$

as

$$
\begin{equation}
H_{SCXin} + H_{+,SCXin} \to H_{+,SCXout} H_{SCXout}
\end{equation}
$$

Then reactants all have -1 pop changes, products all have +1, but labels in the state[species] map automatically strip the \_SCX fuffix.

- Enum class where pb_name != name ??
- Or maybe SymCXReaction subclass of Reaction that handles everything?
- Details tbd
