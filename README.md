# Decision Boundary Model — Paper 0

**Formal foundation of the Agent Governance Series.**

> *Admissibility is not a property of evaluation — it is a property of execution.*

---

## Paper

**Atomic Decision Boundaries: A Structural Requirement for Guaranteeing Execution-Time Admissibility in Autonomous Systems**  
Marcelo Fernandez (TraslaIA), 2026

DOI: [TBD — Zenodo] &nbsp;·&nbsp; arXiv: [TBD]

---

## What this is

This repository contains the LaTeX source for **Paper 0** of the Agent Governance Series — a formal theory paper that characterizes the structural condition under which an admission control system can *guarantee* admissibility at execution time.

**The core result (Theorem 5.1):** No split evaluation system — one in which the decision function and the transition function are separate LTS transitions — can guarantee admissibility under all execution traces. This limitation is architectural, not a matter of policy expressiveness or available state.

The paper introduces:
- The **atomic decision boundary**: a formal property of admission control systems in which decision and state transition are jointly determined as a single indivisible step.
- A structural taxonomy: **atomic systems** vs. **split evaluation systems**, defined in terms of labeled transition systems (LTS).
- Complete formal semantics for the **Escalate** outcome, absent from classical TOCTOU analyses, including the Escalation Closure Requirement (Corollary 5.4).
- A mapping of RBAC, OPA, and ACP to the two classes.

**Paper 1 (ACP):** https://github.com/chelof100/acp-framework-en  
**Paper 2 (IML):** https://github.com/chelof100/iml-benchmark  
**arXiv (ACP):** https://arxiv.org/abs/2603.18829

---

## Repository contents

```
decision-boundary-model/
├── atomic-decision-boundaries.tex   # Full LaTeX source
├── README.md
├── LICENSE
└── .gitignore
```

This is a theory paper. There is no code or benchmark; the contribution is entirely formal.

---

## Formal results

### Main theorem

**Theorem 5.1 (Non-Equivalence).** Let `M_split` be any split evaluation system and `M_atom` any atomic decision boundary system over the same state space, action set, and admissibility predicate. Under Assumption 2.1 (Non-Triviality), there exists an execution trace `σ*` such that `M_split` executes an inadmissible transition while `M_atom` does not.

**Proof:** Constructive. The witness trace is:

```
σ* : s —[dec(a)]→ s_D —[e]→ s* —[exec(a)]→ T(s*, a)
```

where `Adm(s, a) = true` but `Adm(s*, a) = false` after environment action `e`.

### Corollaries

| # | Statement |
|---|---|
| **Cor. 5.1** | Split systems cannot guarantee admissibility at execution time |
| **Cor. 5.2** | External state does not restore atomicity |
| **Cor. 5.3** | Admissibility is a property of execution, not evaluation |
| **Cor. 5.4** | Escalate resolution is itself subject to the atomic boundary requirement |

### System classification

| System | Class | Basis |
|---|---|---|
| RBAC | Split | Permissions evaluated separately from execution |
| OPA | Split | Policy evaluation external to transition |
| OPA + Redis | Split | External state enriches `D`; structural gap remains |
| Kubernetes Admission | Partially atomic | Webhook out-of-band |
| ACP | **Atomic** | Decision and state mutation jointly enforced |

---

## Position in the series

| Paper | Title | Status |
|---|---|---|
| **Paper 0** | Atomic Decision Boundaries (this repo) | In preparation |
| **Paper 1** | [Agent Control Protocol (ACP)](https://arxiv.org/abs/2603.18829) | Published |
| **Paper 2** | [From Admission to Invariants (IML)](https://github.com/chelof100/iml-benchmark) | In preparation |
| **Paper 3** | Fairness under Atomic Governance | Future work |

**Stack logic:**
- Paper 0 proves *when* admissibility can be guaranteed (structural condition).
- Paper 1 builds a system that satisfies that condition (implementation).
- Paper 2 operates above the atomic boundary to detect drift invisible to enforcement.
- Paper 3 addresses fair allocation of atomic decisions across competing agents.

---

## Citation

```bibtex
@misc{fernandez2026dbm,
  title   = {Atomic Decision Boundaries: A Structural Requirement for
             Guaranteeing Execution-Time Admissibility in Autonomous Systems},
  author  = {Fernandez, Marcelo},
  year    = {2026},
  note    = {arXiv: [TBD]. DOI: [TBD]. Paper~0 of the Agent Governance Series.
             Source: https://github.com/chelof100/decision-boundary-model}
}
```

---

## Author

**Marcelo Fernandez** — TraslaIA — info@traslaia.com  
https://agentcontrolprotocol.xyz
