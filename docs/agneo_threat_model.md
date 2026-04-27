# 🛡️ AGNEO Threat Model & Security Rules

**Component:** AGNEO (Reasoner & Proposer)  
**Status:** Authoritative Security Analysis  
**Last Updated:** 2026-04-28

---

## 1. Purpose

This document defines the **threat model, security risks, and mandatory safety rules** for **AGNEO**.

AGNEO is a **semi-trusted reasoning component** that may propose actions but never execute them.

---

## 2. System Boundary

AGNEO operates strictly within the following boundary:

- **Inputs (read-only):**
  - OCR results
  - Screenshot references
  - Execution history
  - Retrieved knowledge snippets

- **Outputs:**
  - Single proposed instruction **OR**
  - Explicit no-action decision

AGNEO never directly affects the external world.

---

## 3. Trust Zones

| Zone | Trust Level | Notes |
|----|------------|------|
| AGGIT (Code / Policy) | Highly trusted | Immutable at runtime |
| AGF91 (Policy Guard) | Highly trusted | Enforces safety |
| AGNEO | Semi-trusted | Reasoning only |
| KnowledgeFetcher | Semi-trusted | Read-only, filtered |
| Internet | Untrusted | Hostile by default |
| AGBUZZ | Trusted | Deterministic execution |

---

## 4. STRIDE Threat Analysis

### Spoofing
**Threat:** Malicious content masquerades as trusted guidance.  
**Mitigation:** No arbitrary browsing, allow-listed sources, human approval.

### Tampering
**Threat:** AGNEO modifies its own knowledge or constraints.  
**Mitigation:** No write access, no persistent memory, Git-only updates.

### Repudiation
**Threat:** Decisions cannot be explained.  
**Mitigation:** Explicit proposals, OCR evidence, audit logs.

### Information Disclosure
**Threat:** Internal UI state leaks externally.  
**Mitigation:** No direct internet access, context stripping.

### Denial of Service
**Threat:** Repeated or looping proposals.  
**Mitigation:** One proposal per cycle, rate limits.

### Elevation of Privilege
**Threat:** AGNEO gains execution or policy authority.  
**Mitigation:** No execution code, immutable policy, human approval.

---

## 5. Forbidden Capabilities

The following are **explicitly forbidden**:

- Arbitrary Internet browsing
- Writing to its own knowledge base
- Long-term memory without review
- Self fine-tuning
- Policy modification

Any of the above breaks the trust model.

---

## 6. Approved Learning Model

AGNEO may **retrieve** knowledge but never learn autonomously.

Approved mechanisms:
- Retrieval-Augmented Generation (RAG)
- Versioned documents from AGGIT
- Read-only KnowledgeFetcher
- Strategy profiles (YAML)

---

## 7. Residual Risks

| Risk | Mitigation |
|----|-----------|
| Reasoning errors | Confidence thresholds |
| Knowledge bias | Curated sources |
| Human error | Audit and replay |

---

## 8. Security Invariant

> **AGNEO may reason, but must never be allowed to change the system that constrains it.**

- Knowledge: read-only  
- Memory: external and auditable  
- Policy: immutable at runtime  

---

## 9. Enforcement

This model is enforced by:
- AGF91 (Policy Guard)
- AGGIT (Version Control)
- Human approval workflows

---

## ✅ Final Statement

AGNEO is a **controlled, semi-trusted advisor** operating under strict constraints.  
This threat model ensures AGNEO remains safe, explainable, and non-crawler by construction.
