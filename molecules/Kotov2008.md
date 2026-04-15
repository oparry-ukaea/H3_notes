# Kotov 2008

## Mechanism

### Atomic

| Reaction                       | Comment                    | Source        | Notes                                                                       | Data in repo |
| ------------------------------ | -------------------------- | ------------- | --------------------------------------------------------------------------- | ------------ |
| $D     + e   \to D^+   + 2e$   | Ionisation                 | AJ H.4 2.1.5  |                                                                             | Y            |
| $D^+   + e   \to D     + h\nu$ | Recombination (radiative)  | AJ H.4 2.1.8  |                                                                             | Y            |
|                                |                            | AJ H.10 2.1.8 |                                                                             | Y            |
| $D^+   + 2e  \to D     + e$    | Recombination (three body) | AJ H.4 2.1.8, |                                                                             | Y            |
|                                |                            | AJ H.10 2.1.8 |                                                                             | Y            |
| $D^+   + D   \to D     + D^+$  | Charge exchange            | HH H.1 3.1.8  | Differs from H3 default. H.1 is <sigma.v>(T); H.3 (p165) is <sigma.v>(T,E). | N            |
|                                |                            | HH H.3 3.1.8  | Presumably electron quantities??                                            | N            |

### Molecular

| Reaction                               | Description                             | Source        | Notes                                                         | Data in repo |
| -------------------------------------- | --------------------------------------- | ------------- | ------------------------------------------------------------- | ------------ |
| $D_2   + e       \to D_2^+ + 2e$       | Non-dissociative izn                    | AJ H.4 2.2.9  | Kotov says AJ H.4 2.1.9; doesn't seem to exist                | Y            |
| $D_2   + e       \to 2D    + e$        | Dissociation                            | AJ H.4 2.2.5g | Kotov says AJ H.4 2.1.5g; doesn't seem to exist               | Y            |
| $D_2   + e       \to D     + D^+ + 2e$ | Dissociative izn                        | AJ H.4 2.2.10 | Kotov says  AJ H.4 2.1.10; doesn't seem to exist              | Y            |
| $D_2   + D^+     \to D_2^+ + D$        | Molecular CX / 'ion conversion'         | AJ H.2 3.2.3  | $\langle \sigma.v\rangle(T)$; assumption: $T = T_{D^+} = T_e$ | Y            |
| $D_2^+ + e       \to 2D$               | Dissociative recombination (of $D_2^+$) | AJ H.4 2.2.14 |                                                               | Y            |
| $D_2^+ + e       \to D     + D^+ + e$  | Dissociative excitation (of $D_2^+$)    | AJ H.4 2.2.12 |                                                               | Y            |
| $D_2^+ + e       \to 2D^+  + 2e$       | Dissociative izn (of $H_D^+$)           | AJ H.4 2.2.11 |                                                               | Y            |
| $D_2   + D^+     \to D_2 + D^+$        | Elastic collisions                      | AJ H.0 0.3T   | H.0 data not needed for fluid codes?                          | N            |
|                                        |                                         | AJ H.1 0.3T   | H.1 data not needed for fluid codes?                          | N            |
|                                        |                                         | AJ H.2 0.3T   |                                                               | Y            |

#### Additional Molecular (Holm, 2022)

Holm claims some additional reactions are included in Kotov 08. He cites PPCP 50 (2008) 105012, but I can't see them mentioned in that paper, or in the EIRENE docs.

| Reaction                            | Description                         | Source        | Notes | Data in repo |
| ----------------------------------- | ----------------------------------- | ------------- | ----- | ------------ |
| $D_2  + e  \to D    + D^-$          | Dissociation of H2 with e-capture?? | AJ H.2 2.2.17 |       |              |
| $D^− + e   \to D    + 2e$           | Ionisation of $D^-$                 | HH H.2 7.1.1  |       |              |
| $D^+ + D^− \to D^+  + D(n = 2) + e$ | ??                                  | HH H.3 7.2.2  |       |              |
| $D^+ + D^− \to D^+  + D(n = 3) + e$ | ??                                  | HH H.2 7.2.3  |       |              |