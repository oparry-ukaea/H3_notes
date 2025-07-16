## Stoichometric alg


For a reaction

$r_1 + r_2 \to p_3 + p_4$

---

For CX we happen to know that 
 - the momentum from species 1 all goes to species 3
 - the momentum from species 2 all goes to species 4

Algorithmically, species 3 will receive momentum $R Q_3 (m_1 v_1 + m_2 v_2)$

where $Q$ is the splitting ratio. So we need:

$$
\begin{align}
R Q_3 (m_1 v_1 + m_2 v_2)  &= R m_1 v_1 \\
Q_3 (m_1 v_1 + m_2 v_2)  &= m_1 v_1 \\
Q_3  &= \frac{m_1 v_1}{m_1 v_1 + m_2 v_2} \\
&= \frac{m_3 v_3}{m_3 v_3 + m_4 v_4}
\end{align}
$$

where the last step follows because species 1 and 3 are the same.

So:
- Loop over reactants
    - Subtract reactant mom from reactant mom source
    - Add to reactants sum
- Loop over products
  - Compute mass ratio Q (accounting for product number)
  - Add Q to product mom source
Subtract each reactant 


for (r: reactants):
  reactant_mom = R * M_r * v_r
  reactants_mom_tot += reactant_mom
  state[species][r][momentum_source] -= reactant_mom

for (p: products):
  prev_prod_mom = R * M_p * v_p
  