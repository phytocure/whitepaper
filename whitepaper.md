# Phytocure: A Decentralized Clinical Cannabis Medicine Protocol on the Solana Blockchain

**Author:** Conor William
**ORCID:** [0009-0005-8307-2353](https://orcid.org/0009-0005-8307-2353)
**Email:** phytocure420@gmail.com
**Date:** May 2025
**Version:** 1.0.0

**DOI:** [10.5281/zenodo.20143620](https://doi.org/10.5281/zenodo.20143620)
**Preprints.org ID:** 213326
**Journal:** *Cannabis and Cannabinoid Research* — Under Review

---

## Abstract

Access to evidence-based cannabis medicine remains constrained by fragmented regulatory frameworks, opaque supply chains, and an absence of interoperable clinical infrastructure. Phytocure proposes a decentralized science (DeSci) protocol built on the Solana blockchain that addresses these structural deficiencies through four interdependent modules: (1) on-chain clinical prescription attestation with verified practitioner credentialing, (2) a tokenized open research publication and peer-review system, (3) an AI-assisted cannabinoid strain analysis engine providing therapeutic profiling, and (4) an immutable on-chain transaction ledger for auditability. The $PYCURE token (CA: `9jBbyCpEoWa9frvtAbq4xNQ8xoHPedeWYkVBDVU9pump`) serves as the network's coordination mechanism, aligning incentives across patients, practitioners, researchers, and distributors. This paper presents the protocol architecture, cryptographic mechanisms, economic model, and governance framework.

**Keywords:** decentralized science, cannabis medicine, blockchain, Solana, cannabinoids, DeSci, clinical prescriptions, tokenomics, DAO governance, therapeutic applications

---

## 1. Introduction

### 1.1 The Problem

Cannabis medicine sits at the intersection of two converging crises: a global chronic pain epidemic affecting over 1.5 billion people (WHO, 2022), and a crisis of scientific reproducibility that undermines evidence-based prescribing. Despite legal medical cannabis programmes in over 50 jurisdictions, clinicians lack access to standardised, tamper-proof patient records; researchers face structural barriers to open data sharing; and patients cannot verify the provenance or cannabinoid content of their medicine.

The consequences are measurable:
- **Prescription fragmentation:** A patient moving between jurisdictions carries paper records that cannot be cryptographically verified
- **Research siloing:** Cannabis research is disproportionately published in paywalled journals, with raw data rarely shared
- **Supply chain opacity:** Adulterated cannabis products have caused documented hospitalisations in multiple jurisdictions (Blount et al., 2021)
- **Clinical knowledge gaps:** The 2024 WHO Expert Committee on Drug Dependence noted that dose standardisation remains a critical unresolved challenge

### 1.2 The Opportunity

Blockchain technology offers properties uniquely suited to these challenges: immutability, cryptographic provenance, programmable incentives, and permissionless access. The Solana network, capable of processing 65,000 transactions per second at sub-cent fees, provides the throughput required for a clinical-scale system.

Decentralized Science (DeSci) — the application of Web3 mechanisms to scientific infrastructure — has demonstrated viability in genomics (EncryptGen), biomarker research (Molecule.to), and drug discovery (VitaDAO). Phytocure extends this paradigm to clinical cannabis medicine.

### 1.3 Scope

This whitepaper describes:
- The technical architecture of the Phytocure Protocol
- The four core functional modules
- The $PYCURE token economic model
- The DAO governance structure
- Security considerations and threat model
- Regulatory alignment strategy

---

## 2. Background

### 2.1 Cannabinoid Pharmacology

The endocannabinoid system (ECS), comprising CB1 and CB2 receptors, endogenous ligands (anandamide, 2-AG), and degradative enzymes (FAAH, MAGL), regulates a broad range of physiological processes including pain modulation, inflammation, appetite, memory, and immune function (Pertwee, 2008).

Phytocannabinoids interact with the ECS in complex, dose-dependent, and strain-variable ways:

| Cannabinoid | Primary Targets | Key Therapeutic Applications |
|-------------|----------------|------------------------------|
| Δ9-THC | CB1, CB2 | Analgesia, appetite, nausea, PTSD |
| CBD | 5-HT1A, TRPV1, GPR55 | Anxiety, epilepsy, inflammation |
| CBG | CB1 partial agonist | Antibacterial, neuroprotection |
| CBC | TRPA1, TRPV4 | Anti-inflammatory, antidepressant |
| THCV | CB1 antagonist (low dose) | Glycaemic control, appetite suppression |
| CBN | CB1, CB2 (weak) | Sedation, antibacterial |

Terpenes — monoterpenes (myrcene, limonene, pinene) and sesquiterpenes (caryophyllene, humulene) — modulate cannabinoid pharmacokinetics and contribute to the "entourage effect" (Russo, 2011).

### 2.2 Regulatory Landscape

As of 2025, medical cannabis is legal in 54 countries. Key frameworks include:
- **Australia (TGA):** Special Access Scheme Category B; 300,000+ approvals as of 2024
- **Germany (BtMG):** Pharmacy-dispensed cannabis since 2017; prescription digitisation underway
- **Canada (ACMPR):** Patient self-registration with licensed producers
- **United Kingdom (VMD):** Specialist prescribing only; significant access barriers persist

No jurisdiction has implemented an interoperable, cryptographically verifiable prescription system. Phytocure is designed to be regulatory-layer agnostic — the on-chain record supplements, rather than replaces, national frameworks.

### 2.3 Prior DeSci Work

| Project | Domain | Mechanism |
|---------|--------|-----------|
| VitaDAO | Longevity | IP-NFT for research funding |
| Molecule | Drug discovery | IP marketplace |
| EncryptGen | Genomics | Tokenized data marketplace |
| PsyDAO | Psychedelics | Research DAO |
| Phytocure | Cannabis medicine | Clinical + Research + AI protocol |

Phytocure is distinguished by its integration of clinical prescription infrastructure with research publication incentives — prior DeSci projects have focused on either funding or data, not the full clinical pathway.

---

## 3. Protocol Architecture

### 3.1 System Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         PHYTOCURE PROTOCOL v1.0                         │
├──────────────┬───────────────────┬────────────────────┬────────────────┤
│  MODULE 1    │     MODULE 2      │     MODULE 3       │   MODULE 4     │
│  CLINICAL    │  DESCI RESEARCH   │   AI ANALYSIS      │  ON-CHAIN      │
│  RX ENGINE   │  PUBLICATION      │   ENGINE           │  LEDGER        │
├──────────────┼───────────────────┼────────────────────┼────────────────┤
│ Practitioner │ IPFS publication  │ Strain fingerprint │ SOL / $PYCURE  │
│ credentialing│ Peer review DAG   │ Therapeutic score  │ tx settlement  │
│ Patient      │ Citation tracking │ Dosage model       │ Distributor    │
│ consent mgmt │ Token rewards     │ Risk stratification│ staking ledger │
│ Rx attestation│ Open access gate │ Drug interaction   │ Treasury mgmt  │
└──────────────┴───────────────────┴────────────────────┴────────────────┘
                                    ↓
         ┌──────────────────────────────────────────────┐
         │              SOLANA BLOCKCHAIN               │
         │  Program: PhytocureProtocol v1               │
         │  Treasury: 5BNvMkDC4eeNzxrUJjgeUU5eSJcSfw   │
         │  $PYCURE:  9jBbyCpEoWa9frvtAbq4xNQ8xoHPede  │
         └──────────────────────────────────────────────┘
```

### 3.2 Data Architecture

All clinical and research data follows a three-layer model:

**Layer 1 — On-Chain:** Cryptographic commitments (hashes), access control, ownership records, and token flows. Stored permanently on Solana.

**Layer 2 — IPFS/Arweave:** Full research papers, patient consent documents, strain analysis reports. Content-addressed, permissioned.

**Layer 3 — Application Layer:** Indexed and searchable via the Phytocure API. Cached for performance, always verifiable against Layer 1 commitments.

### 3.3 Smart Contract Architecture

The Phytocure Solana Program implements four program-derived address (PDA) namespaces:

```
PhytocureProtocol
├── prescriptions/[patient_pubkey]/[rx_id]
│   ├── practitioner_sig: Pubkey
│   ├── product_hash: [u8; 32]
│   ├── dosage_params: DosageConfig
│   ├── created_at: i64
│   └── status: RxStatus {Active, Expired, Revoked}
│
├── research/[author_pubkey]/[paper_id]
│   ├── ipfs_cid: String
│   ├── abstract_hash: [u8; 32]
│   ├── peer_reviews: Vec<ReviewRef>
│   ├── citation_count: u32
│   └── grant_id: Option<Pubkey>
│
├── distributors/[distributor_pubkey]
│   ├── stake_amount: u64
│   ├── trust_tier: u8
│   ├── product_count: u32
│   └── compliance_score: u16
│
└── governance/[proposal_id]
    ├── proposer: Pubkey
    ├── votes_for: u64
    ├── votes_against: u64
    ├── execution_time: i64
    └── state: ProposalState
```

---

## 4. Core Modules

### 4.1 Module 1: Clinical Prescription Engine

#### 4.1.1 Practitioner Credentialing

Practitioners are onboarded through a three-step verification process:
1. **ORCID verification** — Practitioner provides ORCID ID; Phytocure verifies publication history via ORCID API
2. **Credential attestation** — Medical registration number hashed and stored on-chain; physical credential verified by the Research & Clinical Committee
3. **Stake deposit** — Minimum 10,000 $PYCURE staked as quality bond

#### 4.1.2 Prescription Issuance

A valid Phytocure prescription consists of:
- Patient public key (wallet address)
- Product hash (verified cannabinoid profile)
- Dosage configuration: `{thc_mg_per_dose, cbd_mg_per_dose, frequency, duration}`
- Condition code (ICD-11 compliant)
- Practitioner signature

The Rx is committed on-chain with a validity window. Dispensing distributors verify the on-chain Rx before processing the transaction.

#### 4.1.3 Patient Privacy

Patient wallet addresses are pseudonymous. The protocol never stores personally identifiable information on-chain. Patient consent documents are encrypted with the patient's public key and stored on IPFS; only the content-hash is committed on-chain.

### 4.2 Module 2: DeSci Research Publication

#### 4.2.1 Publication Flow

```
Author deposits $PYCURE → Paper uploaded to IPFS →
Abstract + metadata committed on-chain →
Peer review period opens (14-30 days) →
≥3 reviews received → Community vote on acceptance →
Accepted: Author earns citation rewards →
Reviewer: Earns $PYCURE review bounty
```

#### 4.2.2 Peer Review Incentives

The peer review mechanism addresses the structural failure of unpaid academic peer review:
- Each paper specifies a review bounty (minimum 100 $PYCURE per accepted review)
- Reviewers stake 50 $PYCURE as quality bond; slashed for frivolous or plagiarised reviews
- Review quality is assessed by community vote; high-quality reviewers earn reputation NFTs that increase their bounty multiplier

#### 4.2.3 Citation Economy

Every on-chain paper tracks citations from subsequent Phytocure publications. Authors receive a 5 $PYCURE reward per citation, funded from the Protocol Treasury. This creates a long-term incentive for foundational research.

### 4.3 Module 3: AI Analysis Engine

The AI strain analysis engine synthesises three data sources:
1. **Cannabinoid lab data** — THC, CBD, CBG, CBC, CBN, THCV percentages
2. **Terpene profile** — Myrcene, limonene, caryophyllene, linalool, pinene, humulene
3. **Clinical outcome data** — Anonymised patient-reported outcomes from the prescription module

Outputs include:
- **Therapeutic Score** — Condition-specific efficacy prediction (0–100)
- **Dosage Recommendation** — Starting dose with titration schedule
- **Risk Profile** — Psychoactivity index, tolerance risk, drug interaction flags
- **Entourage Effect Index** — Synergy score between cannabinoids and terpenes

All analysis requests are logged on-chain (query hash + result hash) for auditability. The engine is open-source; the model weights are published to the research-data repository.

### 4.4 Module 4: On-Chain Ledger

All financial activity within the Phytocure ecosystem is recorded on Solana:
- Prescription fee payments (SOL or $PYCURE)
- Research publication deposits and review bounties
- Distributor staking and reward distributions
- Treasury inflows and disbursements
- Governance proposal deposits

The ledger is publicly queryable via the Phytocure API and browsable at [phytocure.xyz/transactions](https://phytocure.xyz/transactions).

---

## 5. Security Considerations

### 5.1 Smart Contract Security

- Program code will undergo two independent audits prior to mainnet launch
- Formal verification of core prescription and staking logic using the Certora Prover
- Bug bounty programme: up to 500,000 $PYCURE for critical vulnerabilities

### 5.2 Oracle Risk

Practitioner credential verification relies on external APIs (ORCID, national medical registries). These are mitigated by:
- Requiring multisig confirmation from the Research & Clinical Committee for initial credentialing
- On-chain slashing provides economic deterrent for fraudulent credential attestation

### 5.3 Privacy Threat Model

| Threat | Mitigation |
|--------|-----------|
| Patient deanonymisation | Pseudonymous wallet addresses; no PII on-chain |
| Rx data leakage | Patient documents encrypted client-side; key stored with patient |
| Distributor data breach | Product hashes only; no patient-distributor linkage on-chain |
| Governance attack (whale) | Quadratic voting for major proposals; time-lock delays |

---

## 6. Regulatory Strategy

Phytocure is designed for regulatory compatibility, not regulatory replacement:

1. **Supplementary layer:** On-chain records complement national prescription systems
2. **Auditability:** Law enforcement or regulators can verify supply chain provenance without accessing patient data
3. **Jurisdiction flags:** Prescriptions include jurisdiction metadata; non-compliant transactions are flagged by the distributor staking mechanism
4. **Engagement:** Active engagement with TGA (AU), Health Canada, and EMA policy teams is ongoing

---

## 7. Conclusion

Phytocure represents a necessary evolution in clinical cannabis medicine infrastructure. By combining on-chain attestation, DeSci publication incentives, AI-assisted analysis, and transparent ledger accounting, the protocol creates a system where patients, practitioners, researchers, and distributors are all credibly aligned around therapeutic outcomes and scientific integrity.

The $PYCURE token is not merely a speculative asset — it is the coordination mechanism that makes trustless clinical cannabis medicine possible at global scale.

---

## References

- Blount, B.C. et al. (2021). Vitamin E Acetate in Bronchoalveolar-Lavage Fluid Associated with EVALI. *NEJM*, 382(8).
- Pertwee, R.G. (2008). The diverse CB1 and CB2 receptor pharmacology of three plant cannabinoids. *British Journal of Pharmacology*, 153(2), 199–215.
- Russo, E.B. (2011). Taming THC: potential cannabis synergy and phytocannabinoid-terpenoid entourage effects. *British Journal of Pharmacology*, 163(7), 1344–1364.
- WHO Expert Committee on Drug Dependence. (2024). *Critical Review of Cannabis and Cannabis-Related Substances*. WHO Technical Report.
- VitaDAO. (2023). *Longevity Science IP-NFT Framework*. vitadao.com
- Molecule Protocol. (2024). *Decentralized IP and Funding for Early-Stage Drug Research*. molecule.to

---

*© 2025 Conor William. Published under Creative Commons Attribution 4.0 International (CC BY 4.0).*
*Cite as: William, C. (2025). Phytocure: A Decentralized Clinical Cannabis Medicine Protocol on the Solana Blockchain. DOI: 10.5281/zenodo.20143620*
