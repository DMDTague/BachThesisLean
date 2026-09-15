````markdown
# Exact List-Edge Labelings on Finite Bipartite Multigraphs

This repository contains Lean 4 formalizations accompanying Dylan Tague's work on exact list-edge labelings of finite bipartite multigraphs.

The development formalizes the exact-list lower bound, a stronger nested-minimizer theorem, the exact one-step uncrossing surplus identity, the resulting Latin-square growth bound, and structural results for cubic bipartite multigraphs including star products, tight-cut contractions, and Pfaffian descent.

## Exact-list lower bound

Let `R` be a finite left-`k`-regular bipartite multigraph, with parallel edges treated as distinct edge copies. For every exact left-list assignment `L` of size `k`, the formalization proves

\[
N(L,R) \ge c_k(R),
\]

where `N(L,R)` is the number of admissible exact-list edge labelings and `c_k(R)` is the number of proper edge-colorings from a fixed labelled `k`-palette.

The main Lean theorem is

`exactListLowerBound_machineChecked`

in `BachThesisLean/Uncrossing/MainBound.lean`.

The development also proves the stronger nonregular nested-minimizer theorem

`nested_minimizer`

in `BachThesisLean/Uncrossing/NestedMinimizer.lean`.

## Exact uncrossing surplus

The formalization proves the exact one-step surplus identity

\[
N(S,R)-N(S',R)
=
\sum_{\psi\in\Psi^*}2^{q(F_\psi)+r(F_\psi)}.
\]

The corresponding Lean theorem is

`uncross_surplus_eq_sum_contributors_pow_q_add_r`

in `BachThesisLean/Uncrossing/ManuscriptSurplus.lean`.

The finite contributor set `Ψ*` is represented by `frozenPairContributors`.

## Latin specialization

The Latin-square development formalizes:

- the canonical class `U`;
- the constant-diagonal class `V`;
- the reduced count `rho`;
- the unrestricted count `L`;
- the crown identity `c_(n-1)(R_n) = V_n`; and
- the residual/canonical equivalence giving `N_(n-1)(R_n) = U_(n+1)`.

Together with the exact-list theorem, these results imply

\[
L_{n+1} \ge (n+1)!L_n,
\]

and yield the Lean theorem

`latin_superfactorial_lowerBound`.

## Cubic bipartite graphs

The cubic development is edge-copy-aware throughout and includes formalizations of:

- perfect-matching existence and prescribed-edge extension;
- matching-coveredness;
- edge-root and vertex-root port masks;
- EEP characterizations and two-port bounds;
- star-product matching and factor decomposition;
- EEP and 2EP composition and projection;
- explicit tight-cut contractions and reconstruction;
- matching extension through tight cuts;
- brace and simple-brace reductions;
- amplification reductions;
- square smoothing and witness lifting;
- small-shore and Heawood certificates; and
- TF3 probe reductions.

The unconditional implication chain formalized internally is

\[
TF3 \Longrightarrow EVP \Longrightarrow EEP.
\]

## Pfaffian descent

The repository contains an internal Pfaffian witness and sign formalism for finite bipartite multigraphs.

The formalization includes:

- reference and relative permutation-sign theory;
- graph-isomorphism transport;
- spanning-subgraph inheritance;
- odd-path smoothing;
- square-smoothing transport;
- star-product relative-sign and edge-sign factorization;
- three-port normalization; and
- Pfaffian witness descent through cubic tight cuts.

The endpoint of this chain is `BachThesisLean/Cubic/TightCutPfaffianSet.lean`, which proves that a Pfaffian witness on the original graph induces Pfaffian witnesses on both explicit tight-cut contractions under the stated hypotheses.

The converse tight-cut Pfaffian implication is not asserted by the formalization.

## Formalized scope

The repository distinguishes machine-checked results from finite evidence, external literature, and open research statements.

In particular, the development does not introduce external graph-theoretic results as Lean axioms. The reverse brace implication `EVP -> TF3` used in the accompanying manuscript relies on Häggkvist, while the prescribed-edge result attributed to Diwan and the nonplanar Pfaffian-brace result attributed to Gorsky--Johanni--Wiederrecht remain external unless separately formalized.

The Latin floor, common-core equality criterion, universal `TF_k` / cubic rainbow-component conjecture, and per-edge enumerative Galvin problem also remain outside the proved theorem layer.

The exact formalization boundary is documented in:

- [`docs/FORMALIZATION_SCOPE.md`](docs/FORMALIZATION_SCOPE.md)
- [`KNOWN_GAPS.md`](KNOWN_GAPS.md)

## Building the formalization

The project uses Lean 4.19.0, Mathlib, and Lake.

With `elan` installed, run:

```text
lake update
lake build
```

## Independent proof checking

The repository includes additional source and kernel-level verification.

Run:

```text
python scripts/check_formalization.py
lake build
lake env lean Verification.lean
```

The verification pipeline checks:

- source hygiene and import coverage;
- the complete rooted Lean library;
- the transitive axioms of the public theorem and definition layer; and
- non-vacuity conditions on the audited environment.

The kernel audit permits only Lean's standard logical axioms:

- `propext`
- `Classical.choice`
- `Quot.sound`

and rejects unexpected transitive axioms.

See [`docs/VERIFICATION.md`](docs/VERIFICATION.md) for the verification contract.

## Mathematical report

A public mathematical report accompanying the formalization is included at

[`docs/capstone/EXACT_LIST_EDGE_LABELINGS_FINAL_REPORT.md`](docs/capstone/EXACT_LIST_EDGE_LABELINGS_FINAL_REPORT.md).

The final thesis-to-Lean correspondence records which manuscript statements are represented by Lean declarations and which remain external, computational, expository, or open.
````
