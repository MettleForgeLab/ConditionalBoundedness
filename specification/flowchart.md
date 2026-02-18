# PART I — Switching Policy v0.1 Flowchart

This flowchart describes the decision process per turn and at checkpoints.

It can be translated directly into:

- Rule engine logic  
- Evaluation scripts  
- RLHF labeling schema  
- Simulation harness  
- Policy middleware  

---

## A. High-Level Switching Flow

### Per-Turn Execution

```
START TURN
  ↓
Estimate A, E, H, P, T
Update B (rolling window)
Estimate C (confidence in state estimation)
  ↓
[Membrane Check]
    ├─ If sensitive-domain or prohibited → REFUSE + REDIRECT → END
    ↓
[Boundary Pressure Gate]
    ├─ If B ≥ 0.75 (Level 3) → REFUSE + REDIRECT → END
    ├─ If 0.50 ≤ B < 0.75 (Level 2) → LOCK MODE = Clarify / Structure
    ├─ If 0.25 ≤ B < 0.50 (Level 1) → Reduce expansion bandwidth
    ↓
[Impact Gate]
    ├─ If H ≥ 0.65 → MODE = Template
    ├─ Else if H ≥ 0.50 → MODE = Structure
    ↓
[Ambiguity Gate]
    ├─ If A ≥ 0.60 → MODE = Clarify
    ↓
[Authority Gate]
    ├─ If P ≥ 0.65 → MODE = Structure (criteria framing)
    ↓
[Confidence Gate]
    ├─ If C < 0.50 → Prefer Clarify or Structure
    ↓
[Expansion Gate]
    ├─ If E ≥ 0.70
         AND A ≤ 0.45
         AND H < 0.50
         AND P < 0.50
         AND B < 0.50
         → MODE = Expand (Options or Deep Explanation)
    ├─ Else → MODE = Direct Fulfillment (minimal)
    ↓
GENERATE RESPONSE (respecting mode caps)
    ↓
CHECKPOINT LOOP
```

---

## B. Hysteresis Rules (Bidirectional Stability)

Each scalar variable defines:

- Contraction entry threshold  
- Re-expansion exit threshold  

| Variable | Enter Contraction | Exit Contraction |
|----------|------------------|------------------|
| A | ≥ 0.60 | ≤ 0.45 |
| H | ≥ 0.50 | ≤ 0.45 |
| P | ≥ 0.65 | ≤ 0.40 |
| B | ≥ 0.50 | ≤ 0.30 |
| C (low confidence) | < 0.50 | > 0.65 |

**Rule:**  
Upward traversal (toward expansion) is permitted only if the variable crosses its exit threshold.

This prevents oscillation and threshold gaming.

---

## C. Checkpoint-Based Reassessment

Switching may occur only at defined checkpoints:

- After outline generation  
- After every 2 paragraphs in long-form  
- Before evaluative or prescriptive language  
- After each user turn  
- After explicit scope change  

### At Each Checkpoint

1. Re-estimate A, H, P, B, C  
2. Apply hysteresis logic  
3. If contraction required → shift downward  
4. If upward movement allowed → shift upward  
5. If MNC triggered → terminate cleanly  

Mid-sentence switching is disallowed.

---

## D. Marginal Novelty Collapse (Stopping Subroutine)

At checkpoint:

1. If deliverable satisfied (SCC) → STOP  
2. Compute novelty proxy:  
   - If last 2 paragraphs introduce ≤ 1 new independent point → STOP  
3. Detect redundancy escalation → STOP  

### On Stop

- Conclude cleanly  
- Offer optional continuation (non-expansive)

---

## E. Boundary Pressure Update Function

At end of turn:

- If boundary-adjacent content detected → `B += 0.15`  
- If override attempt detected → `B += 0.25`  
- If safe turn with no boundary proximity → `B -= 0.05`  
- Clamp B between 0 and 1  

Decay must be gradual.  
No instant reset.

---

