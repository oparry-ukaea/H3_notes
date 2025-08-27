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

## Molecular or molecular adjacent

Refs:
- DIV1D: Kobussen25
- SD1D: Zhou22
- SOLPS: Kotov08
- UEDGE: Holm22

| Reaction                                           | Notes                                  | DEFAULT DB      | DIV1D | SD1D | SOLPS           | UEDGE | H3 (planned!)  |
| -------------------------------------------------- | -------------------------------------- | --------------- | ----- | ---- | --------------- | ----- | -------------- |
| $H_2   + e       \to H_2^+ + 2e$                   | Non-dissociative izn                   | AJ H.4 2.2.9    | Y     | Y    | Y               |       | N              |
| $H_2   + e       \to H     + H^+ + 2e$             | Dissociative izn                       | AJ H.4 2.2.10   | N     | N    | Y               |       | N              |
| $H_2   + e       \to 2H    + e$                    | (Neutral) Dissociation                 | AJ H.4 2.2.5g   | Y     | Y    | Y               | Y     | N              |
| $H_2   + H^+     \to H_2^+ + H$                    | Molecular CX / 'ion conversion'        | AJ H.2 3.2.3    | Y     | Y    | Y               | Y     | N              |
| $H_2^+ + e       \to 2H$                           | Dissociative recombination ($H_2^+$)   | AJ H.4 2.2.14   | Y     | Y    | Y               |       | N              |
| $H_2^+ + e       \to H     + H^+ + e$              | Dissociative excitation ($H_2^+$)      | AJ H.4 2.2.12   | Y     | Y    | Y               |       | N              |
| $H_2^+ + e       \to 2H^+  + 2e$                   | Dissociative izn ($H_2^+$)             | AJ H.4 2.2.11   | Y     | Y    | Y               |       | N              |
| $H^+   + H^-     \to 2H$                           | $H^-$ multistep CX recombination       | AJ H.4 7.2.3a   | Y     | N    | N               | Y     | N              |
| $H^+   + H^-     \to 2e    + H^+ + H$              | Ionisation (with $H^−$)                | AJ H.4 7.2.3b   | Y     | N    | N               | Y     | N              |
| $H_2   + e       \to H^-   + H$                    | Dissociative attachment                | AJ H.2 2.2.17   | Y     | N    | Y (Holm claims) |       | N              |
| $H_2   + e       \to H_2^* + e \to H_2 + e + h\nu$ | Molecular excitation + radiative decay |                 | Y     | N    | N               |       | N              |
| $H^+   + H_2     \to H^+   + H_2$                  | Molecule-ion elastic collisions        | AJ H.0,1,3 0.3T | Y     | N    | Y               |       | `AJ H.3 0.3T?` |
| $H^+   + H_2 + e \to 3H$                           | MAR via $H_2^+$, cold $H_2$            | AJ H.4 3.2.3r   |       | Y    |                 | N     |                |
| $H^-   + e       \to H + 2e$                       | $H^-$ izn                              | HH H.2 7.1.1    |       |      | Y (Holm claims) |       |                |
| $H^+ + H^- \to H^+ + H(n=2) + e$                   |                                        | HH H.3 7.2.2    |       |      | Y (Holm claims) |       |                |
| $H^+ + H^- \to H^+ + H(n=3) + e$                   |                                        | HH H.3 7.2.3    |       |      | Y (Holm claims) |       |                |


Alternative names:
- "MAR via $H^−$" is "MAR via $H_2^+$ for cold $H_2$" in the Amjuel description
- "Ionisation (with $H^−$") is "CX multistep izn rate for $H^-$" in the Amjuel description

Questions and discrepancies:
- Kobussen claim "SD1D only includes MAR via D−, whereas [we] include both MAR and MAD via D−"
  - Why do Zhou call $H^+   + H_2 + e \to 3H$ "MAR via $H^-$"? Why do Amjuel call the same reaction "MAR via $H_2^+$"??
- Kobussen and Zhou don't actually list the Amjuel data labels, they just say they use AJ, like Wiesen2015 (SOLPS-ITER pres. paper) and Reiter05 (EIRENE pres. paper). Neither of those list specific Amjuel labels.
- $H_2^+ + e \to 2H$ is written as $H_2^+ + e \to H + H(n=2-8)$ in Holm; check AJ
- Holm22 claims that "The Kotov-2008 model is metastable-unresolved ... and evaluates the transport and dissociation of a single $H_2$ species without considering transport of the vibrationally excited populations of electronic ground-state molecules.", but table 1 in Kotov08 lists the reaction data refs which Holm says are "metastable resolved"...
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


### MAD

Several reactions involving $D_2^+$ and $D^-$ lead to the dissociation of molecules (MAD).
MAD can result in an important source of neutral D atoms and plays a role in the power balance (section 4.3).

### MAR

Three main chains:

| Label      |     | Reaction                                                   | Notes                                                                          |
| ---------- | --- | ---------------------------------------------------------- | ------------------------------------------------------------------------------ |
| 1. DA-MAR  | DA  | $H_2(v) + e \to H^- + H$                                   | Dissociative attachment (DA) of vibrationally excited molecules, *followed by* |
|            | MN  | $H^- + H^+  \to H + H^*$                                   | mutual neutralization (MN) (also called $H^-$ multistep CX recombination?)     |
| 2. IC-MAR  | IC  | $H_2(v) + H^+ \to H_2^+ + H$                               | Molecular CX or Ion Conversion(IC) *followed by*                               |
|            | DR  | $H_2^+(v) + e \to H + H^*$                                 | dissociative recombination  (DR)                                               |
| 3. MIC-MAR | IC  | $H_2(v) + H^+ \to H_2^+ + H$                               | Molecular CX or Ion Conversion(IC) *followed by*                               |
|            | MIC | $H_2(v) +  H_2^+(v) \to H_3^+ + H$                         | molecular to triatomic molecular ion conversion (MIC) *followed by*            |
|            | DR  | $H_3^+(v) + e \to 3H$ *OR* $H_3^+(v) + e \to H_2(v) + H^*$ | one of two possible DR reactions                                               |

(... and potentially a de-excitation $H + H^* \to 2H$).


### Amjuel MAD, MAI, MAR reactions
Amjuel docs suggest the following possible rates for MAD, MAR, MAI.
Possibly irrelevant though; Kobussen25 (for example; appendix C) seem to derive overall rates by combining the rates of each reaction in the main MAD/MAI/MAR chains:

| Label                        | AJ ref  | Reaction string                      | Notes                                                      |
| ---------------------------- | ------- | ------------------------------------ | ---------------------------------------------------------- |
| MAD via $H^-$                | 2.2.17d | $H_2(+ H^+) + e \to H^+ + 2H$        | **Cold $H_2$**: $E_{H_2} = 0.1$ eV                         |
| MAR via $H^-$                | 2.2.17r | $H_2(+ H^+) + e \to 3H$              | **Cold $H_2$** + lots of caveats! Check AJ pdf.            |
| MAD via $H_2^+$ (cold $H_2$) | 3.2.3d  | $H_2(+ e) + H^+ \to H^+ + H + H(+e)$ | **Cold $H_2^+$**: $E_{H_2} = 0.1$ eV, $n_e=n_p$, $T_e=T_p$ |
| MAI via $H_2^+$ (cold $H_2$) | 3.2.3i  | $H_2(+ e) + H^+ \to 2H^+ H + e(+e)$  | **Cold $H_2^+$**: $E_{H_2} = 0.1$ eV                       |
| MAR via $H_2^+$ (cold $H_2$) | 3.2.3r  | $H^2(+ e) + H^+ \to 3H$              | Lots of caveats! Check AJ pdf.                             |

All involve " $H^2$ multistep models ".