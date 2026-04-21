# Kotov 2008 mechanism

## Atomic

| Reaction                       | Comment                    | Source        | Notes                                                                                              | Data in repo |
| ------------------------------ | -------------------------- | ------------- | -------------------------------------------------------------------------------------------------- | ------------ |
| $H     + e   \to H^+   + 2e$   | Ionisation                 | AJ H.4 2.1.5  |                                                                                                    | Y            |
| $H^+   + e   \to H     + h\nu$ | Recombination (radiative)  | AJ H.4 2.1.8  |                                                                                                    | Y            |
|                                |                            | AJ H.10 2.1.8 |                                                                                                    | Y            |
| $H^+   + 2e  \to H     + e$    | Recombination (three body) | AJ H.4 2.1.8, |                                                                                                    | Y            |
|                                |                            | AJ H.10 2.1.8 |                                                                                                    | Y            |
| $H^+   + H   \to H     + H^+$  | Charge exchange            | HH H.1 3.1.8  | Differs from H3 default. H.1 is $\sigma(E_{lab,1})$; H.3 (p165) is $\langle \sigma.v\rangle(T,E)$. | N            |
|                                |                            | HH H.3 3.1.8  | Presumably electron quantities??                                                                   | N            |

Note from Amjuel docs on H.1:
    "Collision cross [sections] are functions of relative velocity, but, due to historic reasons in the EIRENE databases, which initially had been built on data of ref. [2], the laboratory energy of one of the colliding particles (usually the charged particle) is used, with the second collision partner (usually the neutral particle) being at rest. I.e., $\sigma=\sigma(E{lab,1})$. To convert to center of mass energies, or to other isotopes of the same atom, one uses $E{lab,1}=m_1/(2 v_1^2)$  1 and $E_{CM}=\mu/2v_{rel}^2$ with $\mu=m_1m_2/(m_1+m_2)$ being the reduced mass and $v_{rel}=|v_1-v_2|$ the relative collision velocity."

## Molecular

Reactions listed in Kotov08:

| Reaction                               | Description                             | Source        | Notes                                                         | Data in repo |
| -------------------------------------- | --------------------------------------- | ------------- | ------------------------------------------------------------- | ------------ |
| $H_2   + e       \to H_2^+ + 2e$       | Non-dissociative izn                    | AJ H.4 2.2.9  | Kotov says AJ H.4 2.1.9; doesn't seem to exist                | Y            |
| $H_2   + e       \to 2D    + e$        | Dissociation                            | AJ H.4 2.2.5g | Kotov says AJ H.4 2.1.5g; doesn't seem to exist               | Y            |
| $H_2   + e       \to H     + H^+ + 2e$ | Dissociative izn                        | AJ H.4 2.2.10 | Kotov says  AJ H.4 2.1.10; doesn't seem to exist              | Y            |
| $H_2   + H^+     \to H_2^+ + H$        | Molecular CX / 'ion conversion'         | AJ H.2 3.2.3  | $\langle \sigma.v\rangle(T)$; assumption: $T = T_{H^+} = T_e$ | Y            |
| $H_2^+ + e       \to 2D$               | Dissociative recombination (of $H_2^+$) | AJ H.4 2.2.14 |                                                               | Y            |
| $H_2^+ + e       \to H     + H^+ + e$  | Dissociative excitation (of $H_2^+$)    | AJ H.4 2.2.12 |                                                               | Y            |
| $H_2^+ + e       \to 2D^+  + 2e$       | Dissociative izn (of $H_D^+$)           | AJ H.4 2.2.11 |                                                               | Y            |
| $H_2   + H^+     \to H_2 + H^+$        | Elastic collisions                      | AJ H.0 0.3T   | H.0 data not needed for fluid codes?                          | N            |
|                                        |                                         | AJ H.1 0.3T   | H.1 data not needed for fluid codes?                          | N            |
|                                        |                                         | AJ H.2 0.3T   |                                                               | Y            |

Differences in Kotov thesis:

| Reaction                              | Description             | Source        | Notes                                              | Data in repo |
| ------------------------------------- | ----------------------- | ------------- | -------------------------------------------------- | ------------ |
| $H_2^+ + e       \to H     + H^+ + e$ | Dissociation of $H_2^+$ | AJ H.4 2.2.12 | This replaces Dissociative excitation (of $H_2^+$) | Y            |

### Additional Molecular (Holm, 2022)

Holm claims some additional reactions are included in Kotov 08. He cites PPCP 50 (2008) 105012, but I can't see them mentioned in that paper, or in the EIRENE docs.

| Reaction                            | Description                         | Source        | Notes | Data in repo |
| ----------------------------------- | ----------------------------------- | ------------- | ----- | ------------ |
| $H_2  + e  \to H    + H^-$          | Dissociation of H2 with e-capture?? | AJ H.2 2.2.17 |       |              |
| $H^− + e   \to H    + 2e$           | Ionisation of $H^-$                 | HH H.2 7.1.1  |       |              |
| $H^+ + H^− \to H^+  + H(n = 2) + e$ | ??                                  | HH H.3 7.2.2  |       |              |
| $H^+ + H^− \to H^+  + H(n = 3) + e$ | ??                                  | HH H.2 7.2.3  |       |              |

## Characteristics and assumptions:

- $H_2^+$ only, no $H^-$ or $H_3^+$
- CRM (Amjuel rates??) doesn't take collisions between heavy particles into account, CX or elastic collisions - assumes lifetimes of excited states is shorter than the timescales of such collisions
- Only H.4 2.2.5g and H.2 3.2.3 take vibrationally excited states into account
- Rotational excitation neglected
- **MAR** takes place via
  - Molecular CX removes $H^+$, produces $H_2^+$
  - Dissociative recombination converts $H_2^+$ to $H$

## Sanity check against Kotov thesis equations

Check that all terms in Eqn 3.48 from Kotov thesis are accounted for by standard population change model:
$$
\begin{align}
    \frac{dn_{H_2}}{dt}   &= -(D_{H_2} + S_{H_2} + I_{H_2})n_e n_{H_2}\\
    \frac{dn_{H_2^+}}{dt} &= S_{H_2} n_e n_{H_2} - (R_{H_2^+} + D_{H_2^+} + S_{H_2^+})n_e n_{H_2^+}\\
    \frac{dn_H}{dt}       &= (2D_{H_2} + I_{H_2^+})n_e n_{H_2} + (2R_{H_2^+} + D_{H_2^+})n_e n_{H_2^+} - I_H n_e n_H + R_H n_e n_{H+}\\
    \frac{dn_{H^+}}{dt}   &= I_{H_2} n_e n_{H_2} + (D_{H_2^+} + 2S_{H_2^+})n_e n_{H_2^+} + I_H n_e n_H - R_H n_e n_{H+}
\end{align}
$$

