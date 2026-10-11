# Action Identifiability in Protein-Design Agents

> **This repository serves a redirect. Do not delete it.**
> The URL `https://saanviiyer.github.io/action-identifiability/` is printed as a QR code on
> the MoML 2026 poster, so it has to keep resolving indefinitely.

**Project page (canonical):** https://saanviiyer.github.io/pages/projects/action-identifiability/

Saanvi S. Subramanian (Caltech) · Gabriela Lobinska (AITHYRA)
MoML 2026 (MIT) · AgenticLS @ NeurIPS 2026

---

## The claim

A closed-loop protein-design agent proposes an intervention, scores the resulting molecule, and
uses the score to choose the next action. This only works if the scorer can tell the available
interventions apart. We call that requirement **action identifiability**, and we measure whether
it holds for a concrete action–scorer pair: 78 COSMIC single-base-substitution signatures as the
action space, and distance in ESM-2 representation space as the score.

It does not hold.

| Result | Number |
| --- | --- |
| Median pairwise distance, COSMIC 96-channel space | 0.815 |
| Median pairwise distance, ESM-2 outcome regions | 0.0068 |
| Compression | ~120× |
| Pairs >0.5 apart in COSMIC but <0.011 apart after scoring | 1,780 / 3,003 (59.3%) |
| Structured action vs composition-matched control | −0.0027, 95% CI [−0.0063, 0.0012] |
| Policy top-1 accuracy on held-out proteins | 7.55% |
| Conformal coverage / mean set size | 92.2% / 66.8 of 78 actions |
| Adaptive lookahead vs fixed, at 100 scorer calls | +0.0113 worse, 95% CI [+0.0082, +0.0143] |
| Sequences passing Pfam's curated threshold for PF17041 | 0 |

## What is in here

```
index.html                 redirect to the canonical project page
static/images/             paper figures, poster
static/pdfs/               the paper
static/data/               seed-level results and bootstrap intervals
```

The figures and prose now live on the canonical page in the main site repository
(`saanviiyer.github.io`, at `pages/proj-action-identifiability.html`). The files below stay
mirrored here because they were linked from this URL before the move.

| File | Contents |
| --- | --- |
| `static/pdfs/action-identifiability-moml2026.pdf` | The paper |
| `static/images/poster.png` | The MoML 2026 poster |
| `static/data/all_seeds_summary.csv` | Per-seed improvement, accept rate, and length control for the structured, composition-matched, and random arms |
| `static/data/paired_uncertainty.json` | Paired bootstrap intervals and exact randomization p-values |
| `static/data/summary.json` | Policy top-1/top-5 against baselines with protein-cluster bootstrap |
| `static/data/agent_results.csv` | Per-protein, per-goal budget trajectories across four Pfam targets |

## Analysis code

The nine scripts behind the paper, each mapping to a section:

| Script | Section |
| --- | --- |
| `action_space_vs_scorer.py` | All 78 actions measured in both COSMIC and ESM-2 space |
| `cross_signature_steering.py` | Applies COSMIC actions to proteins; mean ESM-2 region reached |
| `prism_proto_design.py` | The Metropolis optimization loop (T = 0.02) |
| `proto_ablation.py` | Composition-matched, edit-count-matched, unselected-drift arms |
| `inverse_design_classifier.py` | Supervised policy and leave-actions-out variants |
| `equivalence_class_policy.py` | ESM-2 neighborhood sets, transitive-closure analysis |
| `selective_action_interface.py` | Conformal prediction sets, frozen abstention thresholds |
| `adaptive_policy_multibudget.py` | Lookahead vs fixed vs random at 25/50/100 scorer calls |
| `validate_designs_hmmer.py` | Independent PF17041 profile-HMM validation |

## Citation

```bibtex
@inproceedings{subramanian2026action,
  author    = {Saanvi S. Subramanian and Gabriela Lobinska},
  title     = {Action Identifiability in Protein-Design Agents},
  booktitle = {Workshop on Machine Learning for Molecules (MoML);
               NeurIPS Agentic Life Sciences Workshop (AgenticLS)},
  year      = {2026},
  url       = {https://saanviiyer.github.io/pages/projects/action-identifiability/}
}
```
