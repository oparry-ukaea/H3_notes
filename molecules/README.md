# Molecules in Hermes-3

## Tasks

1. Lit review
    * [Holm - UEDGE](./Holm2023.md)
    * [Kobussen - DIV1D](./Kobussen2025.md)
    * [Kotov - SOLPS-ITER](./Kotov2008.md)
    * [Zhou - SD1D](./Zhou2022.md)
    * Key questions:
      * What do we need for rough equivalence with SOLPS
      * What are SOLPS' shortcomings?
      * Should $D_2^+$, $D^-$ be transported?

2. Init development
   * Refactoring of atomic reactions (unify hydrogenic, ionic?). Leave open option to use linearised rates (see below).
   * Reactions in H3 with unit tests
3. Test in 1D and compare to DIV1D (sims will be provided; maybe [here??](https://zenodo.org/records/15236644)).
4. Test in 2D and compare to SOLPS-ITER (sims will be provided).
5. Option to use linearised reactions - huge potential speedup.


[Which reactions are in which code](reactions.md)
