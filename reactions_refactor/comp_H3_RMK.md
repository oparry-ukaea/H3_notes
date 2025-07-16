
# H3 vs. RMK

## Density

| RMK | H3                         |
| --- | -------------------------- |
|     | $C_s \prod_{r}{n_{r}} c_R$ |
| ??  | $C_s R$                    |

## Momentum C_s < 0

| RMK                             | H3              |
| ------------------------------- | --------------- |
| $\frac{C_s p_s R F_{G,s}}{n_s}$ |                 |
| $C_s p_s R G_s$                 | $C_s p_s R G_s$ |

## Momentum C_s > 0

| RMK                                                                                | H3                                            |
| ---------------------------------------------------------------------------------- | --------------------------------------------- |
| $\sum_{r}\left(\frac{-C_r C_s p_r p_s m_s M c_R F_{G,r}}{n_r S_{G,tot}}\right)$    |                                               |
| $\frac{C_s p_s m_s R}{S_{G,tot}}\sum_{r}\left(\frac{-C_r p_r F_{G,r}}{n_r}\right)$ |                                               |
| $S_{G,s} R \sum_{r}\left(-C_r p_r G_r\right)$                                      | $S_{G,s} R \sum_{r}\left(-C_r p_r G_r\right)$ |

Where
 
- $M$ is the mass action factor
- $S_{G,tot}$ is the RMK "splitting factor" (total weight) for momentum
- $F_{G,r}$ is the momentum flux of reactant $r$


and we used:

- $R = M c_R$
- $S_{G,s} = \frac{C_s p_s m_s}{S_{G,tot}}$
- $G_r = F_{G,r} / n_r$ 

## Energy C_s < 0

| RMK                                 | H3              |
| ----------------------------------- | --------------- |
| $\frac{C_s p_s M c_R F_{W,s}}{n_s}$ |                 |
| $\frac{C_s p_s R F_{W,s}}{n_s}$     |                 |
| $C_s p_s R W_s$                     | $C_s p_s R W_s$ |


## Energy C_s > 0

| RMK                                                                          | H3                                            |
| ---------------------------------------------------------------------------- | --------------------------------------------- |
| $\sum_r\left(\frac{-C_r C_s p_r p_s M c_R F_{W,r}}{S_{W,tot} n_r}\right)$    |                                               |
| $\frac{C_s p_s R}{S_{W,tot}}\sum_r\left(\frac{-C_r p_r F_{W,r}}{n_r}\right)$ |                                               |
| $S_{W,s} R \sum_{r}\left(-C_r p_r W_r\right)$                                | $S_{W,s} R \sum_{r}\left(-C_r p_r W_r\right)$ |

Where
 
- $M$ is the mass action factor
- $S_{W,tot}$ is the RMK "splitting factor" (total weight) for energy
- $F_{W,r}$ is the energy flux of reactant $r$


and we used:

- $R = M c_R$
- $S_{W,s} = \frac{C_s p_s}{S_{W,tot}}$
- $W_r = F_{W,r} / n_r$ 
