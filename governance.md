# Phytocure DAO Governance Model

## Overview

Phytocure is governed by a Decentralized Autonomous Organization (DAO) composed of $PYCURE token holders. Governance decisions range from protocol parameter changes to research grant allocations and distributor network policy.

---

## Governance Principles

1. **Transparency** — All proposals, votes, and treasury transactions are recorded on-chain
2. **Scientific Integrity** — Research committee has veto power over clinically unsafe proposals
3. **Progressive Decentralization** — Core team retains emergency multisig until protocol maturity
4. **Inclusivity** — Delegation allows non-technical holders to participate via trusted representatives

---

## Governance Bodies

### 1. Token Holder Assembly
- All $PYCURE holders with ≥ 100 tokens
- Vote on all standard proposals
- Quorum: 10% of circulating supply

### 2. Research & Clinical Committee (RCC)
- 7 elected members with verified medical or research credentials
- ORCID ID required for eligibility
- Mandate: Review clinical safety of all protocol changes
- Term: 12 months, staggered elections

### 3. Technical Steering Group (TSG)
- 5 core contributors + 2 elected community members
- Responsible for smart contract upgrades, security patches
- Emergency powers: can pause protocol for up to 72 hours without a vote

### 4. Protocol Treasury Council
- 5-of-9 multisig wallet holders
- Controls Protocol Treasury (`5BNvMkDC4eeNzxrUJjgeUU5eSJcSfwPriMcrsuxaphet`)
- Elected annually by Token Holder Assembly

---

## Proposal Types

| Type | Quorum | Approval | Timelock | Description |
|------|--------|----------|----------|-------------|
| Signal | 5% | >50% | None | Non-binding temperature check |
| Standard | 10% | >60% | 48h | Protocol parameter changes |
| Treasury | 10% | >66% | 72h | Fund allocation >50,000 $PYCURE |
| Constitutional | 20% | >75% | 7 days | Core governance rule changes |
| Emergency | N/A | TSG only | None | Critical security patches |

---

## Proposal Lifecycle

```
DRAFT → REVIEW (3 days) → VOTE (7 days) → TIMELOCK → EXECUTION
  ↑                           ↓
Community            If rejected → ARCHIVE
Discussion
```

### Stage 1: Draft (Community Forum)
- Author posts proposal with full specification
- Minimum 3 days discussion period
- Requires community feedback and iteration

### Stage 2: Formal Submission
- Author submits on-chain via governance interface
- Requires 10,000 $PYCURE deposit (returned if proposal passes)
- RCC reviews for clinical safety compliance

### Stage 3: Voting
- 7-day voting window
- Options: For / Against / Abstain
- Voting power = √(staked $PYCURE) for major proposals (quadratic)

### Stage 4: Execution
- Passed proposals enter timelock (type-dependent)
- TSG executes or automatically executed via smart contract
- Results published to research-data repository

---

## Research Grant Program

### Grant Categories

| Category | Max Grant | Review Period |
|----------|-----------|---------------|
| Micro-Grant | 5,000 $PYCURE | 2 weeks |
| Standard Grant | 50,000 $PYCURE | 4 weeks |
| Major Research | 500,000 $PYCURE | 8 weeks |

### Eligibility
- Published ORCID ID required
- Minimum 1 prior peer-reviewed publication in cannabinoid science preferred
- Open-access publication required for all funded research
- Data must be released to [phytocure/research-data](https://github.com/phytocure/research-data)

---

## Conflict of Interest Policy

- All committee members disclose $PYCURE holdings quarterly
- Members recuse themselves from votes where they hold a direct financial interest
- Distributor-affiliated members may not vote on distributor policy proposals

---

*© 2025 Conor William. CC BY 4.0.*
