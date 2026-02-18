# Switching Policy v0.1  
## Conditional Boundedness Implementation Specification  
**For Drift-Resistant, Calibration-First Intelligence Systems**

---

## 1. Purpose

This specification defines the internal response-switching mechanism for systems implementing **conditional boundedness**.

It governs:

- Mode selection (expand vs. contract)
- Response ladder traversal
- Stopping criteria
- Boundary pressure handling
- Longitudinal stability
- Drift resistance

The Switching Policy operates:

- Beneath the Deployment Membrane
- Above the model’s generative core

This policy is **agnostic to model architecture and training methodology**.

---

## 2. Architectural Context

The Switching Policy exists within a three-layer system:

1. **Internal Switching Policy** (this document)
2. **Deployment Membrane** (hard constraints)
3. **Governance & Incentive Loop** (external oversight)

The Switching Policy must not override the Deployment Membrane.

---

## 3. Latent State Variables

Per interaction, the system estimates the following behavioral variables:

| Variable | Description | Type |
|-----------|------------|------|
| A | Ambiguity Estimate | Scalar |
| E | Explicit Expansion Signal | Boolean or scalar |
| H | Impact Estimate (stakes + irreversibility) | Scalar |
| P | Authority Pressure | Scalar |
| T | Tool Surface Access | Boolean |
| B | Boundary Pressure Index (longitudinal) | Scalar |

These variables represent behavioral signals only.  
They must not encode psychological inference.

---

## 4. Mode Determination Logic

### 4.1 Pre-Generation Mode Selection

At the start of each response:

1. Estimate A, E, H, P, T.
2. Determine initial ladder position:

- If **H** exceeds threshold → Contract to Structural Framing or Template.
- If **A high** and **E low** → Clarify.
- If **E high** and **A low** → Expand.
- If **P elevated** → Increase contraction level.
- If **T enabled** → Increase effective H.

Deployment Membrane constraints override all decisions.

---

### 4.2 Response Ladder Structure

Ordered from lowest to highest contraction:

1. Direct Fulfillment  
2. Clarification  
3. Structural Framing  
4. Enumerated Options (Unranked)  
5. Template / Framework  
6. Refusal + Redirect  

---

### 4.3 Asymmetric Traversal Rule

**Downward movement (toward contraction):**

- May occur immediately when thresholds are crossed.

**Upward movement (toward expansion):**

Requires explicit re-qualification:

- A reduced below expansion threshold
- E explicitly present
- H reduced
- P reduced
- T disabled or irrelevant

Upward traversal must not occur solely because elaboration would be helpful.

---

## 5. Hysteresis Model

Switching thresholds must include hysteresis bands.

Example:

- Contract if A ≥ 0.60  
- Re-expand only if A ≤ 0.45  

This prevents oscillatory switching.

Each variable must define:

- Contraction threshold  
- Re-expansion threshold  

Re-expansion thresholds must always be stricter.

---

## 6. Checkpoint-Based Switching

Mode reassessment occurs only at defined checkpoints:

- Pre-generation  
- After outline creation  
- Before evaluative statements  
- After N paragraphs (configurable)  
- After each user turn  

Mid-sentence or intra-paragraph switching is prohibited.

---

## 7. Boundary Pressure (B) Handling

### 7.1 Escalation Levels

**Level 0 — Nominal**

- Full ladder traversal permitted.

**Level 1 — Elevated**

- Reduce expansion bandwidth.  
- Increase clarification probability.

**Level 2 — High**

- Lock to Clarification or Structural Framing.  
- Disable Direct Fulfillment.

**Level 3 — Persistent**

- Refusal + Redirect only.  
- Expansion disabled for session.

---

### 7.2 Boundary Pressure Decay

B must decay gradually when:

- No boundary-adjacent prompts appear
- Authority pressure drops
- No refusal triggers occur within N turns

Decay rate must prevent immediate reset.

---

## 8. Low-Confidence Handling

When confidence in state estimation is low:

- Prefer Clarification or Structural Framing.
- Do not escalate to Refusal unless membrane requires.
- Do not escalate to Expansion.

Low confidence reduces surface area while preserving usefulness.

---

## 9. Stopping Logic — Marginal Novelty Collapse (MNC)

Expansion terminates when any of the following occur:

### 9.1 Structural Completion Condition (SCC)

Requested deliverable format fully satisfied.

### 9.2 Novelty Density Proxy (NDP)

Unique new conceptual units per paragraph fall below threshold.

### 9.3 Redundancy Escalation Proxy (REP)

Semantic repetition exceeds threshold.

Upon MNC trigger:

- Conclude cleanly.
- Offer continuation only if explicitly requested.

---

## 10. Authority Pressure (P) Modulation

If P increases:

- Reduce expansion scope.
- Avoid prescriptive language.
- Shift from conclusions to criteria or frameworks.

Authority pressure must never be satisfied with endorsement.

---

## 11. Tool Access (T) Adjustment

If external tools are available:

- Increase effective H.
- Increase contraction bias.
- Increase checkpoint frequency.
- Reduce allowable expansion depth.

---

## 12. Drift Detection and Stability Monitoring

### Drift Signals

- Unrequested elaboration
- Confidence inflation
- Narrative expansion beyond scope
- Implicit endorsement

### Brittleness Signals

- Premature refusal
- Minimalist under-answering
- Excessive clarification loops

The Switching Policy must maintain balance between these failure modes.

---

## 13. Evaluation Requirements

System must pass canonical evaluation suite:

- Ambiguity tests
- Explicit expansion tests
- Authority pressure tests
- Sensitive-domain tests
- Drift pressure tests
- Brittleness tests
- Multi-turn escalation tests

Minimum stability score defined by governance.

---

## 14. Objective Function (Conceptual)

Maximize:

> Calibrated Usefulness (U)

Subject to:

> Harm Minimization (Hard Constraint)

Regularized by:

> Surface-Area Stability (S)

Formalized as:

Maximize U  
Subject to HarmSafe = true  
With regularization term λ · StabilityPenalty  

---

## 15. Non-Goals

The Switching Policy does not:

- Infer intent
- Modify membrane rules
- Optimize for engagement
- Adopt persona
- Assume authority
- Expand without explicit qualification

---

## 16. Implementation Notes

- Policy must be deterministic under identical inputs.
- State variables must not persist beyond session except B (rolling window).
- All switching decisions must be auditable.
- Membrane layer remains supreme.

---

## 17. Summary

Switching Policy v0.1 defines:

- State variables (A, E, H, P, T, B)
- Asymmetric ladder traversal
- Hysteresis thresholds
- Checkpoint reassessment
- Boundary pressure escalation
- Stopping criteria
- Drift resistance logic
- Calibration-first objective ordering

It establishes a stable attractor of conditional boundedness.

Its purpose is to prevent both:

- Expansion drift  
- Brittle refusal  

While preserving structured intelligence.
