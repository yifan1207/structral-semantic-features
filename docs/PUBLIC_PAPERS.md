# Public Papers and Artifact Map

## Same Targets, Different Computation

**Full title:** Same Targets, Different Computation: How Post-Training Divides Work Across Model Layers

- Paper: https://arxiv.org/abs/2605.07284
- Release repository: https://github.com/yifan1207/first-divergence-crosspatching
- Main workspace experiments: `exp23`, `exp36`, `exp37`, `exp47`, `exp49`, `exp51`, `exp53`, `exp56`, `exp58`, and `exp60`
- Public checker: `scripts/reproduce/check_same_base_dependencies_paper.py` in the release repository

The paper asks whether a learned late-stack effect works on base-model upstream state or depends on upstream computation learned alongside it. Its central controlled experiment holds target responses and training setup fixed while changing whether the output mode is requested by familiar language or a newly learned nonce cue.

## The Convergence Gap

**Full title:** The Convergence Gap: Instruction-Tuned Language Models Stabilize Later in the Forward Pass

- Release repository: https://github.com/yifan1207/convergence-gap-instruction-tuning
- Main workspace experiments: `exp09`, `exp11`, `exp14`, `exp15`, `exp19`, `exp22`, `exp54`, and `exp55`
- Public checker: `scripts/reproduce/check_convergence_gap_claims.py` in the release repository

The paper asks when paired checkpoints settle on their own final next-token prediction. It uses endpoint-matched, endpoint-free, fixed-history, and matched-prefix intervention controls.

## Relationship

The papers share infrastructure and paired checkpoints but have different estimands:

| Paper | Primary object | Main intervention |
|---|---|---|
| Same Targets, Different Computation | Dependence between earlier state and learned late changes | Cross a base or descendant upstream state with a base or descendant late stack |
| The Convergence Gap | Stabilization of a model's own prediction through depth | Graft or swap matched-prefix MLP windows and compare layerwise readouts |

Convergence-gap experiments are not evidence for the cross-patching paper's main claims, and cross-patching experiments are not used to define the convergence gap.

## Historical Work

The workspace also contains earlier steering, residual-direction, crosscoder, and geometry experiments. These remain useful research context but are not automatically part of either paper's public evidence chain. Use each release repository's artifact map as the source of truth.
