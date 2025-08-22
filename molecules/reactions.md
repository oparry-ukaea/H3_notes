# Reactions

<!-- Key:
- N: Not implemented
- Y: Implemented without mass rescaled rates
- Y*: Implemented with mass rescaled rates (e.g. $\langle\sigma v\rangle_D(T) = \langle\sigma v\rangle_H(T/2)$) for H isotopes, i.e. for $H$ below, read $H$|$D$|$T$ -->


Key
- AJ: Amjuel ([53] in Holm)
- HH: Hydhel ([51] in Holm)
- HV: H2VIBR ([52] in Holm)

## Atomic

| Reaction                             | Notes                                | DIV1D | SD1D | SOLPS | UEDGE | Hermes-3 | DB used by EIRENE  | DB used by H3, if different |
| ------------------------------------ | ------------------------------------ | ----- | ---- | ----- | ----- | -------- | ------------------ | --------------------------- |
| $H     + e   \to H^+   + 2e$         | Ionisation                           | Y     | Y    | Y     |       | Y        | AJ H.4 2.1.5       |                             |
| $H     + e   \to H^+   + 2e  + h\nu$ | Ionisation + radiative decay         | Y     | Y?   | Y?    |       | Y        |                    |                             |
| $H^+   + H   \to H     + H^+$        | Charge exchange                      | Y     | Y    | Y     |       | Y        | HYDHEL H.1,3 3.1.8 | AJ H.3 3.1.8 (p111)         |
| $H^+   + e   \to H$                  | Recombination (radiative)            | Y     | Y    | Y?    |       |          |                    |                             |
| $H^+   + e   \to H     + h\nu$       | Recombination (radiative power loss) | Y     | Y?   | Y     |       | Y        | AJ H.4,10 2.1.8    |                             |
| $H^+   + 2e  \to H     + e$          | Recombination (three body)           | Y     | Y?   | Y     |       | Y        | AJ H.4,10 2.1.8?   |                             |
| $H^+   + H   \to H^+   + H$          | Atom-ion elastic collisions          | Y     |      |       |       |          |                    |                             |

| Reaction                             | Notes                                | Default DB (Eirene) | DIV1D | SD1D | SOLPS | UEDGE | H3                    |
| ------------------------------------ | ------------------------------------ | ------------------- | ----- | ---- | ----- | ----- | --------------------- |
| $H     + e   \to H^+   + 2e$         | Ionisation                           | AJ H.4 2.1.5        | Y     | Y    | Y     |       | Y                     |
| $H     + e   \to H^+   + 2e  + h\nu$ | Ionisation + radiative decay         |                     | Y     | Y?   | Y?    |       | Y                     |
| $H^+   + H   \to H     + H^+$        | Charge exchange                      | HH H.1,3 3.1.8      | Y     | Y    | Y     |       | Y AJ H.3 3.1.8 (p111) |
| $H^+   + e   \to H$                  | Recombination (radiative)            |                     | Y     | Y    | Y?    |       |                       |
| $H^+   + e   \to H     + h\nu$       | Recombination (radiative power loss) | AJ H.4,10 2.1.8     | Y     | Y?   | Y     |       | Y                     |
| $H^+   + 2e  \to H     + e$          | Recombination (three body)           | AJ H.4,10 2.1.8?    | Y     | Y?   | Y     |       | Y                     |
| $H^+   + H   \to H^+   + H$          | Atom-ion elastic collisions          |                     | Y     |      |       |       |                       |

## Molecular

DIV1D: Kobussen25
SD1D: Zhou22
SOLPS: Kotov08
UEDGE: Holm22

| Reaction                                               | Notes                                  | DEFAULT DB      | DIV1D | SD1D | SOLPS           | UEDGE         | H3 (planned!)   |
| ------------------------------------------------------ | -------------------------------------- | --------------- | ----- | ---- | --------------- | ------------- | --------------- |
| $H_2   + e       \to H_2^+ + 2e$                       | Non-dissociative izn                   | AJ H.4 2.2.9    | Y     | Y    | Y               |               | N               |
| $H_2   + e       \to H     + H^+ + 2e$                 | Dissociative izn                       | AJ H.4 2.2.10   | N     | Y    | Y               |               | N               |
| $H_2   + e       \to 2H    + e$                        | (Neutral) Dissociation                 | AJ H.4 2.2.5g   | Y     | Y    | Y               | Y             | N               |
| $H_2   + H^+     \to H_2^+ + H$                        | Molecular CX / 'ion conversion'        | AJ H.2 3.2.3    | Y     | Y    | Y               | Y             | N               |
| $H_2^+ + e       \to 2H$                               | Dissociative recombination ($H_2^+$)   | AJ H.4 2.2.14   | Y     | Y    | Y               |               | N               |
| $H_2^+ + e       \to H     + H^+ + e$                  | Dissociative excitation ($H_2^+$)      | AJ H.4 2.2.12   | Y     | Y    | Y               |               | N               |
| $H_2^+ + e       \to 2H^+  + 2e$                       | Dissociative izn ($H_2^+$)             | AJ H.4 2.2.11   | Y     | Y    | Y               |               | N               |
| $H^+   + H^-     \to 2H$                               | $H^-$ CX                               |                 | Y     | N    | N               | AJ H.4 7.2.3a | N               |
| $H^+   + H^-     \to 2e    + H^+ + H$                  | Ionisation (with $H^−$)                |                 | Y     | N    | N               | AJ H.4 7.2.3b | N               |
| $e     + H_2     \to H^-   + H$                        | Dissociative attachment                | AJ H.2 2.2.17   | Y     | N    | Y (Holm claims) |               | N               |
| $e     + H_2     \to e     + H_2^* \to e + H_2 + h\nu$ | Molecular excitation + radiative decay |                 | Y     |      | N               |               | N               |
| $H^+   + H_2     \to H^+   + H_2$                      | Molecule-ion elastic collisions        | AJ H.0,1,3 0.3T | Y     | Y    | Y               |               | `AJ H.3 0.3T?`  |
| $H^+   + H_2 + e \to 3H$                               | MAR via $H^−$                          |                 | Y     | N    |                 | N             | `AJ H.4 3.2.3r` |
|                                                        |                                        |                 |       |      |                 |               |                 |

### Molecule-related

| Reaction                         | Notes     | DEFAULT DB   | DIV1D | SD1D | SOLPS           | UEDGE | H3 (planned!) |
| -------------------------------- | --------- | ------------ | ----- | ---- | --------------- | ----- | ------------- |
| $H^-   + e       \to H + 2e$     | $H^-$ izn | HH H.2 7.1.1 |       |      | Y (Holm claims) |       |               |
| $H^+ + H^- \to H^+ + H(n=2) + e$ |           | HH H.3 7.2.2 |       |      | Y (Holm claims) |       |               |
| $H^+ + H^- \to H^+ + H(n=3) + e$ |           | HH H.3 7.2.3 |       |      | Y (Holm claims) |       |               |



Alternative names:
- "MAR via $H^−$" is "MAR via $H_2^+$ for cold $H_2$" in the Amjuel description
- "Ionisation (with $H^−$") is "CX multistep izn rate for $H^-$" in the Amjuel description

Discrepancies to resolve:
- $H_2^+ + e \to 2H$ is written as $H_2^+ + e \to H + H(n=2-8)$ in Holm; check AJ
- Holm22 claims that "The Kotov-2008 model is metastable-unresolved ... and evaluates the transport and dissociation of a single $H_2$ species without considering transport of the vibrationally excited populations of electronic ground-state molecules.", but table 1 in Kotov08 lists the reaction data refs which Holm says are "metastable resolved"...


Questions:
- Kotov08 states that the rates (from Amjuel and HydHel) are for Deuterium. Is there mass-rescaling going on?
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

