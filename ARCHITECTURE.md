# Conditional Boundedness Architecture

This document summarizes the system structure at a high level.

---

## Layer 1 — Training Gradient Shaping

Objective: Calibrated usefulness under bounded authority.

Training rewards:

- Contraction under ambiguity
- Expansion under explicit request
- Non-authority stance
- Correct stopping behavior
- Safe progress over unnecessary refusal

---

## Layer 2 — Switching Policy

Implements conditional boundedness via state-dependent mode selection.

Core state variables:

- A — Ambiguity
- E — Explicit expansion signal
- H — Impact (stakes + irreversibility)
- P — Authority pressure
- T — Tool surface access
- B — Boundary pressure (longitudinal)
- C — Confidence

Mechanisms:

- Hysteretic thresholds
- Ranked response ladder
- Checkpoint-based reassessment
- Marginal novelty collapse detection

---

## Layer 3 — Deployment Membrane

Hard constraints enforced outside learned preference:

- Sensitive-domain exclusions
- Identity inference prohibition
- Persona restrictions
- Tool gating

Membrane rules override switching logic.

---

## Layer 4 — Governance

Stability is preserved through:

- Perturbation-based evaluation
- Basin depth measurement
- Threshold immutability
- Incentive alignment
- Drift monitoring

No single layer is sufficient alone.

Stability emerges from layered interaction.
