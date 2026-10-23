# Repository Layout

```text
astrbot-memory-fabric/
├─ src/astrbot_plugin_memory_fabric/
│  ├─ host/                 # AstrBot event and provider adapter
│  ├─ ledger/               # append-only conversation evidence
│  ├─ memory/               # canonical records and revisions
│  ├─ formation/            # extraction and write decisions
│  ├─ concepts/             # fuzzy concepts and affective traces
│  ├─ associations/         # weighted graph and activation
│  ├─ retrieval/            # lexical/vector/temporal/graph fusion
│  ├─ lifecycle/             # reinforcement, decay, consolidation
│  ├─ behavior/              # response context and proactive gates
│  ├─ audit/                 # audit views and replay
│  └─ plugin.py              # AstrBot plugin entry point
├─ tests/
│  ├─ unit/
│  ├─ contract/
│  ├─ integration/
│  └─ replay/
├─ docs/
│  ├─ architecture/
│  ├─ adr/
│  ├─ research/
│  ├─ agent-protocol/
│  └─ superpowers/
├─ research/                # local source snapshots or extracted notes only
├─ third_party/             # copied code with notices and provenance
├─ tools/                    # deterministic offline tooling
├─ pyproject.toml
├─ AGENTS.md
├─ NOTICE
└─ LICENSE
```

The initial implementation should keep modules small and behind interfaces. Storage, embedding, reranking, and LLM extraction must be replaceable without changing the canonical schema.
