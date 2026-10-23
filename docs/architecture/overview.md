# Architecture Overview

## Product boundary

Memory Fabric is an AstrBot plugin. AstrBot remains responsible for platform adapters, provider calls, plugin lifecycle, command dispatch, and host WebUI. NapCat and OneBot remain outside this repository.

```text
QQ / NapCat / OneBot
          |
       AstrBot
          |
  memory-fabric plugin
  +---------------------------+
  | event adapter             |
  | raw conversation ledger   |
  | memory formation          |
  | canonical memory store   |
  | concepts and associations |
  | retrieval orchestration  |
  | consolidation/lifecycle  |
  | proactive candidate gate |
  | audit/replay API          |
  +---------------------------+
          |
   response context / bounded proactive candidate
```

## Behavioral model

The system distinguishes evidence, memories, concepts, associations, and current activation. A memory can influence a reply without being a hard fact. A proactive action is always a candidate first; it is sent only after timing, repetition, sensitivity, relationship, and cooldown gates.

## Layers

### 1. Host adapter

Converts AstrBot events into a stable internal event envelope and converts retrieval context or proactive decisions back to AstrBot operations. This layer must not own memory policy.

### 2. Ledger

Append-only raw private-chat events with stable ids, timestamps, actor roles, session id, content references, and provenance. The ledger is the source for replay and reprocessing.

### 3. Memory formation

Asynchronous policy that extracts candidate episodic memories, facts/preferences, fuzzy concepts, affective traces, and association updates. It records why each item was formed and the evidence ids used.

### 4. Canonical store

The authoritative mutable state. It stores revisions rather than destructive overwrites, including validity time, observation time, confidence, importance, activation, scope, and supersession links.

### 5. Retrieval and activation

Combines lexical, vector, temporal, graph, recency, importance, and optional rerank signals. It returns evidence-backed activation packets with token budgets and reasons.

### 6. Lifecycle

Reinforces used memories, decays unused details, consolidates related memories, preserves durable concepts, archives low-value items, and supports reversible restore.

### 7. Behavior gate

Maps activation packets into response guidance and proactive-care candidates. It cannot invent a fact without evidence and cannot send proactively without policy checks.

### 8. Audit and replay

Explains what was stored, why it was recalled, how it changed, and which evidence supported it. Replay runs a recorded conversation through a chosen policy version without mutating production state.

## Design invariants

1. Raw evidence is never silently rewritten.
2. Canonical state is versioned and reversible.
3. Facts have observation time and validity time; inferred concepts carry uncertainty.
4. Retrieval is evidence-first and token-budgeted.
5. Proactive behavior is bounded and fail-closed.
6. A single canonical memory model is shared by all future behavior modules.
7. The first release is private-chat only; group behavior is a later adapter.
