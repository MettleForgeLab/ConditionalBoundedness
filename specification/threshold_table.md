# Switching Policy v0.1 — Formal Threshold Table (Numerical Ranges)

---

## 0. Conventions

All latent variables are normalized to `[0, 1]`, where:

- `0.00` = none / low  
- `1.00` = strong / high  

Hysteresis uses two thresholds per variable:

- **Enter threshold** — triggers contraction or restriction  
- **Exit threshold** — allows re-expansion or relaxation  

Exit thresholds must always be stricter (lower) than entry thresholds to prevent oscillation.

---

# 1) Ambiguity (A)

| Action | Threshold |
|--------|------------|
| Enter Clarify mode | A ≥ 0.60 |
| Exit Clarify mode | A ≤ 0.45 |
| Hard-block expansion unless clarified | A ≥ 0.70 |

**Notes:**

- If `A ≥ 0.60`, the system should ask one targeted clarification before expanding.
- If `A ≥ 0.70`, restrict to `Clarify → Structure` until A drops.

---

# 2) Explicit Expansion Signal (E)

E may be Boolean or scalar.

Recommended scalar interpretation:

- `0.0` = no explicit request  
- `0.5` = implicit request (“tell me more”)  
- `1.0` = explicit request (“brainstorm 20,” “deep dive,” “expand fully”)  

| Expansion Eligibility | Threshold |
|-----------------------|------------|
| Expansion allowed (if other gates pass) | E ≥ 0.70 |
| Expansion discouraged (use structure/options first) | 0.40 ≤ E < 0.70 |
| Expansion disallowed (unless user clarifies) | E < 0.40 |

---

# 3) Impact (H) — Stakes + Irreversibility

H is a composite estimate.

| Action | Threshold |
|--------|------------|
| Prefer Structure over Direct | H ≥ 0.50 |
| Prefer Template over Options | H ≥ 0.65 |
| Force Refusal if sensitive-domain triggered | H ≥ 0.80 (membrane overrides regardless) |
| Exit high-impact contraction | H ≤ 0.45 |

**Notes:**

- If `H ≥ 0.65`, shift from “options” toward templates/checklists.
- Prevents authority posture in high-consequence contexts.

---

# 4) Authority Pressure (P)

| Action | Threshold |
|--------|------------|
| Block endorsements / “what would you do” | P ≥ 0.50 |
| Force Criteria/Framework mode | P ≥ 0.65 |
| Raise Boundary Pressure trend | P ≥ 0.75 persistent ≥ 2 turns |
| Exit authority contraction | P ≤ 0.40 |

**Notes:**

At `P ≥ 0.65`:
- Disallow Direct Fulfillment that reads as prescriptive.
- Use structural framing (factors, tradeoffs, decision criteria).

---

# 5) Tool Surface Access (T)

Recommended binary model:

- `T = 0` → text-only  
- `T = 1` → tools/actuation available  

Optional scalar scoring:

- `0.0` text-only  
- `1.0` tool access enabled  

**Policy Rule:**

If `T = 1`:

```
H′ = min(1, H + 0.10)
```

Then:

- Increase contraction bias  
- Tighten expansion depth caps (see §8)

---

# 6) Boundary Pressure (B)

B is a rolling index across recent turns (e.g., last 6–10 turns).  
It reflects boundary-proximity behavior, not intent.

| Level | Name | Threshold |
|-------|------|------------|
| B0 | Nominal | B < 0.25 |
| B1 | Elevated | 0.25 ≤ B < 0.50 |
| B2 | High | 0.50 ≤ B < 0.75 |
| B3 | Persistent | B ≥ 0.75 |

### Escalation Rule (Example)

- Boundary-adjacent event → `+0.15`
- Override attempt → `+0.25`
- Safe turn → `−0.05`
- Clamp to `[0,1]`

### Behavior Per Level

- **B1** → Reduce expansion bandwidth; increase clarification probability  
- **B2** → Lock to Clarify/Structure; disable Direct  
- **B3** → Refusal + Redirect only for remainder of session (unless decay)

---

# 7) Confidence (C) in Latent State Estimation

Optional but recommended. Range `[0,1]`.

| Behavior | Threshold |
|-----------|------------|
| Low confidence | C < 0.50 |
| Very low confidence | C < 0.35 |

**Rules:**

- If `C < 0.50` → Bias to Clarify or Structure  
- If `C < 0.35` → Clarify only (unless request is fully unambiguous + low-impact)

---

# 8) Expansion Bandwidth Caps (Length / Depth Controls)

To prevent drift even when expansion is allowed:

### Token / Section Caps by Mode

| Mode | Default Depth Cap |
|-------|-------------------|
| Direct Fulfillment | 1–3 short paragraphs |
| Clarification | 1–2 questions max |
| Structural Framing | 5–9 bullets or 6–10 lines |
| Options | N options exactly as requested (default 5–12) |
| Template | 1 template + short usage note |
| Refusal | 2–4 lines + allowed alternatives |

### Longform Expansion (E high, A low, H low, P low, B0–B1)

- Allow 3–6 sections maximum before MNC checkpoint  
- If `T = 1`, reduce max sections by 1

---

# 9) Marginal Novelty Collapse (MNC) Thresholds

## Structural Completion Condition (SCC)

Stop immediately when requested format is satisfied.

---

## Novelty Density Proxy (NDP)

Trigger stop if:

- Last 2 paragraphs introduce ≤ 1 new independent point.

---

## Redundancy Escalation Proxy (REP)

Trigger stop if:

- Two consecutive paragraphs primarily restate prior points.

---

### Checkpoint Frequency

- Every 2 paragraphs in longform  
- After each section  

---

# 10) Mode Selection Summary Table

| Condition | Default Ladder Rung |
|------------|--------------------|
| A ≥ 0.60 | Clarify |
| A < 0.60 and E ≥ 0.70 and H < 0.50 and P < 0.50 and B0–B1 | Options or Expanded Explanation |
| H ≥ 0.50 | Structural Framing |
| H ≥ 0.65 | Template |
| P ≥ 0.65 | Criteria/Framework (no endorsements) |
| B2 | Clarify/Structure only |
| B3 | Refusal + Redirect only |
| C < 0.50 | Clarify or Structure |

---

# Mapping to Ache-Band Pacing (Presentation Layer Only)

This does **not** change switching.  
It adjusts delivery density.

- **Softfold (0.69–0.75)** → Default user-facing pacing  
- **Narrowband (0.70–0.73)** → Precision outputs  
- **Openband (0.65–0.80)** → Ideation outputs  

All remain bounded by MNC and Boundary Pressure (B).

---
