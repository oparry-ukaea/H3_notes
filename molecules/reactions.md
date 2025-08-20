# Reactions

Key:
- N: Not implemented
- Y: Implemented without mass rescaled rates
- Y*: Implemented with mass rescaled rates (e.g. $\langle\sigma v\rangle_D(T) = \langle\sigma v\rangle_H(T/2)$) for H isotopes


For $H$ below, read $H$, $D$, or $T$

## Atomic

| Reaction                             | Notes                                | DIV1D | SD1D | SOLPS | UEDGE | Hermes-3 | DB used by EIRENE    | DB used by H3, if different |
| ------------------------------------ | ------------------------------------ | ----- | ---- | ----- | ----- | -------- | -------------------- | --------------------------- |
| $H     + e   \to H^+   + 2e$         | Ionisation                           | Y     | Y    | Y     |       | Y        | AMJUEL H.4 2.1.5     |                             |
| $H     + e   \to H^+   + 2e  + h\nu$ | Ionisation + radiative decay         | Y     | Y?   | Y?    |       | Y        |                      |                             |
| $H^+   + H   \to H     + H^+$        | Charge exchange                      | Y     | Y    | Y     |       | Y        | HYDHEL H.1,3 3.1.8   | AMJUEL H.3 3.1.8 (p111)     |
| $H^+   + e   \to H$                  | Recombination (radiative)            | Y     | Y    | Y?    |       |          |                      |                             |
| $H^+   + e   \to H     + h\nu$       | Recombination (radiative power loss) | Y     | Y?   | Y     |       | Y        | AMJUEL H.4,10 2.1.8  |                             |
| $H^+   + 2e  \to H     + e$          | Recombination (three body)           | Y     | Y?   | Y     |       | Y        | AMJUEL H.4,10 2.1.8? |                             |
| $H^+   + H   \to H^+   + H$          | Atom-ion elastic collisions          | Y     |      |       |       |          |                      |                             |


## Molecular

| Reaction                                   | Notes                                        | DIV1D (Kobussen25) | SD1D (Zhou22) | SOLPS | UEDGE | Hermes-3 | DB used by EIRENE   | DB used by H3, if different |
| ------------------------------------------ | -------------------------------------------- | ------------------ | ------------- | ----- | ----- | -------- | ------------------- | --------------------------- |
| $H_2   + e   \to H_2^+ + 2e$               | Non-dissociative ionisation                  | Y                  | Y             | Y     |       | N        | AMJUEL H.4 2.1.9    |                             |
| $H_2   + e   \to H     + H^+ + 2e$         | Dissociative ionisation                      | N                  | Y             | Y     |       | N        | AMJUEL H.4 2.1.10   |                             |
| $H_2   + e   \to 2H    + e$                | Dissociation                                 | Y                  | Y             |       |       | N        | AMJUEL H.4 2.1.5g   |                             |
| $H_2   + H^+ \to H_2^+ + H$                | Molecular charge exchange / 'ion conversion' | Y                  | Y             | Y     |       | N        | AMJUEL H.2 3.2.3    |                             |
| $H_2^+ + e   \to 2H$                       | Dissociative recombination ($H_2^+$)         | Y                  | Y             | Y     |       | N        | AMJUEL H.4 2.2.14   |                             |
| $H_2^+ + e   \to H     + H^+ + e$          | Dissociative excitation ($H_2^+$)            | Y                  | Y             | Y     |       | N        | AMJUEL H.4 2.2.12   |                             |
| $H_2^+ + e   \to 2H^+  + 2e$               | Dissociative ionisation ($H_2^+$)            | Y                  | Y             | Y     |       | N        | AMJUEL H.4 2.2.11   |                             |
| $H^+   + H^- \to 2H$                       | $H^-$ charge exchange                        | Y                  | N             |       |       | N        |                     |                             |
| $H^+   + H^- \to 2e + H^+ + H$             | Ionisation (with $H^−$)                      | Y                  | N             |       |       | N        |                     |                             |
| $e + H_2 \to H^- + H$                      | Dissociative attachment                      | Y                  | N             |       |       | N        |                     |                             |
| $e + H_2 \to e + H_2^* \to e + H_2 + h\nu$ | Molecular excitation + radiative decay       | Y                  |               |       |       | N        |                     |                             |
| $H^+ + H_2 \to H^+ + H_2$                  | Molecule-ion elastic collisions              | Y                  | Y             | Y     |       | N        | AMJUEL H.0,1,3 0.3T | Plan on AMJUEL H.3 0.3T?    |
| $H^+ + H_2 + e \to 3H$                     | MAR via H−                                   |                    | Y             |       |       | N        |                     |                             |

Questions:
- SD1D and UEDGE papers presents H rates - do they use mass-rescaling for D,T?
- Do SOLEDGE3X have molecules? Latest papers (2024) only mention Neutrals via EIRENE.

### Dissociative ionisation in Amjuel vs. Hydhel:

The dissociative ionisation rates in the Amjuel and Hydhel data are slightly different.

Amjuel includes the channel:

$e + H_2^+ \to H^* + H \to H+ + H$

while Hydhel (instead?) includes:

 $e + H2+ → e + H2+ * → H+ + H$. 

Where:
- $H^*$ is the excited atomic state
- $H_2^{+*}$ is the (vibrationally) excited molecular state

Further discussion in Zhou22, details on channels in Janev03