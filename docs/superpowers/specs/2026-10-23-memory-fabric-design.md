# Memory Fabric Design Draft

> Status: draft for user review. This document defines the first implementation target; it does not authorize runtime deployment yet.

**Goal:** Build a private-chat AstrBot plugin that autonomously forms and recalls human-like memories while preserving full evidence, auditability, and bounded proactive behavior.

**Architecture:** AstrBot remains the host. Memory Fabric owns the canonical memory model, evidence ledger, concept/association system, retrieval orchestration, lifecycle, and behavior gates. Existing plugins are research references or optional adapters rather than competing authorities.

**Tech Stack:** Python 3.12, AstrBot plugin APIs, SQLite-first canonical storage, replaceable lexical/vector/rerank backends, pytest, deterministic replay fixtures.

## User-visible behavior

The bot chats normally without per-message approval. It can remember facts, episodes, preferences, relationship experiences, fuzzy concepts, and associations. It may forget details naturally while preserving source evidence. A bounded proactive-care policy may create occasional messages based on activated associations and recent interaction.

The user can inspect, adjust, freeze, delete, restore, and replay memories after the fact. These controls govern the system; they are not inserted into every conversation turn.

## First-release scope

- Private chat and one primary user.
- Full raw event ledger.
- Autonomous extraction and memory formation.
- Episodic, semantic, fuzzy-concept, and weighted-association records.
- Observation time plus validity time for facts.
- Hybrid retrieval with evidence and reason traces.
- Decay, reinforcement, consolidation, archive, restore.
- Proactive candidates with conservative limits, cooldowns, quiet hours, deduplication, and fail-closed behavior.
- Replay and evaluation fixtures.

## Explicit non-goals

- Group chat.
- Model fine-tuning.
- Autonomous external actions beyond bounded QQ messages.
- Copying whole third-party plugins without license review.
- Treating every inferred association as a factual assertion.

## Data flow

```text
AstrBot event
  -> normalized event envelope
  -> append-only ledger
  -> asynchronous formation job
  -> canonical revisions + concepts + association updates
  -> indexes/projections

Current user turn
  -> query analysis
  -> lexical/vector/temporal/graph retrieval
  -> activation packet with evidence and token budget
  -> response guidance
  -> optional proactive candidate
  -> policy gate and audit
```

## Core contracts

- `EventEnvelope`: immutable normalized turn with source, actor, session, event time, content hash, and privacy flags.
- `EvidenceRef`: pointer from any derived object to one or more ledger events.
- `MemoryRevision`: canonical fact/episode with revision id, validity interval, confidence, importance, scope, status, and supersession.
- `FuzzyConcept`: uncertain abstraction with affective dimensions, evidence refs, activation and decay state.
- `AssociationEdge`: weighted typed edge with reinforcement and provenance.
- `ActivationPacket`: retrieved evidence, activated concepts/edges, reasons, scores, and token budget.
- `ProactiveCandidate`: proposed message with triggers, policy version, cooldown status, and decision outcome.

## Design risks

- LLM extraction may hallucinate or over-generalize; every derived item must retain evidence and confidence.
- Fuzzy concepts can become hidden stereotypes; they need provenance, decay, and inspectability.
- Self-reinforcing associations can create repetitive behavior; activation and proactive gates must be separately bounded.
- SQLite and indexes must be rebuildable from canonical records.
- Third-party licenses may restrict copied code and distribution.

## Verification strategy

Use deterministic replay fixtures to compare policy versions. Measure evidence attribution, fact revision correctness, recall precision, concept activation usefulness, proactive false positives, latency, and token cost. No release claim is made without actual test output.
