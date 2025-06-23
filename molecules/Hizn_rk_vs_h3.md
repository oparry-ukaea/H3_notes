
$H + e \to H_+ + 2e$

## H3

```
  AA = from_ion["AA"] (=== to_ion["AA"])
  V1 = from_ion["velocity"]
  # Volume-averaged reaction rate
  reaction_rate = R * MF

  momentum_exchange = reaction_rate * AA * V1;
  subtract(from_ion["momentum_source"], momentum_exchange);
  add(to_ion["momentum_source"], momentum_exchange);
```

So, $dG = R {\rm MF} m_H v_H$

$$
\begin{align}
dG_{H} &= \\
       &= - R {\rm MF} m_H v_H
\end{align}
$$

$$
\begin{align}
dG_{H+} &= \\
        &= R {\rm MF} m_H v_H
\end{align}
$$


## RK

c_s < 0 for H

$$
\begin{align}
dG_{H} &= c_s w_s {\rm MF} R G / n_H \\
       &= -1 1 {\rm MF} R G / n_H \\
       &= - {\rm MF} R G / n_H \\
       &= - R {\rm MF} m_H v_H
\end{align}
$$

c_s > 0 for $H_+$, e

$$
\begin{align}
dG_{H+} &= -\sum_{s'}{c_{s'} c_s {\rm AA}_s / {~\rm SF~} {~\rm MF~} / n_s R G_s'}\\
        &= -(c_H c_H+ AA_{H+} {~\rm MF~} R G_H / {~\rm SF~} / n_H) \\
        &= R {\rm MF} m_H v_H (AA_{H+} / {~\rm SF~}) \\
\end{align}
$$
Outer loop (over all species) would include e for momentum, but H3 doesn't calculate an electron momentum source.
Inner loop (over reactants; H, e), but $e$ is filtered out by massFilterThreshold

Try implementing exactlh as RK has it, including splitting factors and mass factors with

- $nG = mv$
- ${\rm MF}~R=$ reaction_rate