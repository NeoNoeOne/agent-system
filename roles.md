from pathlib import Path

Define the content of docs/roles.md exactly as agreed

content = """

📘 System Roles Documentation

File: docs/roles.md Status: Authoritative Last Updated: 2026-04-26



0. Core Principle (Read First)

No single role may Reason, Orchestrate, and Execute.

These responsibilities are intentionally separated to prevent crawler behavior, unsafe autonomy, and untraceable actions.

This system is workflow-driven, human-approved, and fully auditable.



1. Role Overview

Role


Codename


Primary Question

Orchestrator


AGN8N


When should something happen?

Action Executor


AGAAP


How is it executed?

System of Record


AGGIT


What is allowed to exist?

Reasoner


AGNEO


Why should we act?

Executor


AGBUZZ


Observe and act deterministically

Policy Guard


AGF91


Is this allowed?

Verifier


AGWING


Did it work?

Archivist


AGRX78


What happened, forever?

Human


—


Should this happen?



2. AGN8N — Orchestrator (WHEN)

Technology: n8n

Authority Level: High (flow control only)

Responsibilities

    Owns the sequence and timing of operations

    Triggers workflows (cron, manual, webhook)

    Routes data between agents

    Waits for human approval

    Branches on outcomes (approved / rejected / failed)

Explicitly Forbidden

    ❌ Reasoning or intent selection

    ❌ UI automation

    ❌ ADB, OCR, or tapping

    ❌ Modifying policy or execution logic

Key Rule

AGN8N decides WHEN, never WHAT or HOW.



3. AGAAP — Action Executor (HOW)

Technology: Ansible

Authority Level: Medium (deterministic execution only)

Responsibilities

    Executes concrete actions via playbooks

    Calls agent APIs (/observe, /execute, /verify)

    Enforces idempotence

    Fails fast on invalid inputs

Explicitly Forbidden

    ❌ Waiting for humans

    ❌ Branching workflows

    ❌ Reasoning or retries

    ❌ State exploration

Key Rule

AGAAP executes exactly what it is told, once.



4. AGGIT — System of Record (WHAT exists)

Technology: GitHub

Authority Level: Absolute (truth source)

Responsibilities

    Stores and versions:

    Ansible roles & playbooks (AGAAP)

    n8n workflow JSON (AGN8N)

    Policy files (AGF91)

    Schemas & contracts

    Role documentation

    Enforces review via PRs

    Enables rollback and traceability

Explicitly Forbidden

    ❌ Runtime state

    ❌ Secrets

    ❌ Live execution

Key Rule

If it is not in AGGIT, it must not run.



5. AGNEO — Reasoner & Proposer (WHY)

Technology: OpenClaw agent running in NemoClaw

Authority Level: Advisory only

Responsibilities

    Reads observations (screenshots, OCR)

    Reasons about UI state

    Proposes one instruction at a time

    Explains rationale

    Requests human approval

Explicitly Forbidden

    ❌ Executing actions

    ❌ Taking screenshots

    ❌ Calling ADB

    ❌ Looping autonomously

Key Rule

AGNEO may propose, but never act.



6. AGBUZZ — Deterministic Executor (OBSERVE + ACT)

Technology: Local ADB-based executor

Authority Level: High (but constrained)

Responsibilities

    Takes screenshots

    Runs OCR

    Computes safe tap coordinates

    Executes taps after approval

    Produces audit artifacts (before/after)

Explicitly Forbidden

    ❌ Reasoning

    ❌ Deciding intent

    ❌ Acting without approval

Key Rule

AGBUZZ acts only on approved, validated instructions.



7. AGF91 — Policy Guard (SAFETY)

Technology: Rules as code (YAML / Ansible asserts)

Authority Level: Veto power

Responsibilities

    Enforces:

    allowed intents

    confidence thresholds

    time windows

    rate limits

    Blocks unsafe or invalid proposals

Explicitly Forbidden

    ❌ Execution

    ❌ Reasoning

    ❌ State mutation

Key Rule

AGF91 can stop anything, but start nothing.



8. AGWING — Verifier (DID IT WORK?)

Technology: Rule-based or LLM-assisted checker

Authority Level: Read-only evaluation

Responsibilities

    Compares before/after state

    Detects no-ops or failures

    Reports verification outcome

Explicitly Forbidden

    ❌ Retrying

    ❌ Executing

    ❌ Proposing actions

Key Rule

AGWING judges outcomes, never causes them.



9. AGRX78 — Archivist (MEMORY & AUDIT)

Technology: Storage / database / object store

Authority Level: Immutable record keeper

Responsibilities

    Stores:

    screenshots

    OCR results

    proposals

    approvals

    execution & verification

    Links records to AGGIT commit SHAs

    Enables replay and forensic analysis

Explicitly Forbidden

    ❌ Execution

    ❌ Reasoning

    ❌ Mutation of history

Key Rule

AGRX78 remembers everything and changes nothing.



10. Human — Approval Authority

Technology: Mattermost UI

Authority Level: Absolute veto

Responsibilities

    Approves or rejects proposals

    Provides oversight

    Owns risk acceptance

Explicitly Forbidden

    ❌ Bypassing system

    ❌ Direct execution

Key Rule

No action occurs without explicit human approval (unless policy later allows auto-approval).



11. Non-Crawler Guarantee

This system is not a crawler because:

    No agent owns the observe–act loop

    Execution is separated from reasoning

    Human approval gates every action

    Orchestration is external and deterministic

Crawler = Agent decides + Agent acts

This system = Agent proposes + Human approves + Deterministic executor acts



12. Change Control

Any change to:

    roles

    responsibilities

    permissions

    allowed actions

Must:

    Be committed to AGGIT

    Go through review

    Be redeployed via AGN8N



✅ Final Lock-In Statement

Each role has one responsibility, one authority level, and one direction of influence.

No role may grow beyond its boundary.

This document is the constitution of the system. """

Write the file to a docs directory

base_dir = Path.cwd() / "docs" base_dir.mkdir(parents=True, exist_ok=True) file_path = base_dir / "roles.md" file_path.write_text(content, encoding="utf-8")

print(f"Generated file: {file_path.resolve()}")

