# Met-Enkephalin Pose Overlay

**[kuhfeldrf.github.io/met-enkephalin-pose-overlay](https://kuhfeldrf.github.io/met-enkephalin-pose-overlay/)**

Four placements of `YGGFM` in the active-state μ-opioid receptor, superposed on one
receptor frame and measured against chain P of **8F7Q**. An interactive 3Dmol.js viewer
with the coordinates served alongside it.

**Each predicted pose is the one its own method ranked first, chosen before any
comparison to the experimental structure.** That ordering is what makes this a test
rather than an illustration.

## Result

| Method | Backbone RMSD (res 1–5) | All-heavy | Tyr1–Asp149 anchor |
|---|---|---|---|
| Experimental 8F7Q | reference | — | 4.55 Å |
| HADDOCK3 blind | 2.56 Å | 4.40 Å | 2.55 Å |
| Chai-1 | 2.28 Å | 2.64 Å | 1.11 Å |
| Protenix + MSA | **1.73 Å** | 1.58 Å | 2.45 Å |

All three methods place the peptide in the orthosteric pocket within 2.6 Å backbone
RMSD. Protenix is closest at 1.73 Å, and its **25-model median is 1.55 Å**, so the
result does not depend on which sample was picked.

## Two things this figure does not show

These are stated on the page itself and repeated here because they are the parts most
easily misread:

- **Every prediction over-tightens the salt bridge.** The experimental Tyr1 amine sits
  4.55 Å from Asp149; all three predictions place it at 1.11–2.55 Å. These are
  energy-minimised or model-confident contacts, not measured physiological distances,
  and should not be quoted as such.
- **Recovering one pose is not a screen.** Met-enkephalin has a crystal structure to
  check against; a milk-derived candidate does not. On this pilot, scoring tracks global
  burial and peptide length rather than the D3.32 register — the best mis-registered
  HADDOCK pose scored −70.0 and outranked 9 of 10 near-native poses, and co-folding
  confidence reaches **AUROC 0.500** once length is controlled.

## Provenance

**Reference.** 8F7Q, active-state human MOR with β-endorphin bound; chain P residues 1–5
are the experimental met-enkephalin pose. Released 2022-12-14, after the Protenix
`base_default_v1.0.0` training cutoff of 2021-09-30, so this complex was **not in
training**. DAMGO's 6DDF was, so the YGGF-in-pocket motif was learnable.

**HADDOCK3.** Blind: `ranair` ab initio, no orthosteric restraints, no superposition,
4000 rigidbody → flexref → emref. Pose `emref_67`, score −114.2, AIR energy 0.

**Chai-1.** Single-sequence with ESM embeddings, 5 seeds × 5 samples. Shown: seed 0,
model 1 (top by aggregate score, 0.4187). Across 25 models backbone RMSD 1.33–6.04 Å,
median 2.24 Å.

**Protenix + MSA.** Paired and unpaired receptor MSA, 5 seeds × 5 samples, 3 recycles,
200 timesteps. Shown: seed 1, sample 0 (top by ranking score, 0.9484). Across 25 models
1.24–4.39 Å, median 1.55 Å.

## Files

`receptor_8f7q.pdb` (chain R, 287 residues) plus `pep_experimental.pdb`,
`pep_haddock.pdb`, `pep_chai.pdb` and `pep_protenix.pdb`. RMSD is computed over residues
1–5 after superposing each model's receptor onto 8F7Q chain R by sequence alignment; the
anchor distance is measured inside each model's own receptor.
